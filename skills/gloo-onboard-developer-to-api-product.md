---
name: gloo-onboard-developer-to-api-product
description: Onboard a developer team onto a published API product in a Gloo Portal — create the team, create its application, subscribe the application to the API product, and issue the API key the developer will call with.
api: gloo:gloo-portal
spec: openapi/gloo-portal-server-openapi.yaml
operations:
  - CreateTeam
  - CreateTeamApplication
  - ListApiProducts
  - GetApiProductById
  - SubscribeToApiProduct
  - CreateApplicationAPIKey
  - ListApplicationAPIKeys
generated: '2026-09-12'
method: generated
source: openapi/gloo-portal-server-openapi.yaml, conventions/gloo-conventions.yml, errors/gloo-problem-types.yml
---

# Onboard a developer team onto a Gloo API product

Gloo Portal's object model is `Team → Application → Subscription → APIProduct`, and credentials
hang off the **Application**, never off the user. This is the full onboarding path.

## Before you start

- **Base URL.** There is no vendor base URL. The Portal server runs in the operator's cluster;
  Solo's own spec uses `http://portal.example.com/v1` as a placeholder. Ask the operator for the
  host they exposed the backend portal server on.
- **Authentication.** Every call carries an `id_token` cookie issued by the portal's OIDC
  identity provider. There is no bearer API key for this API. A `401` means the token is
  invalid; a `403` means the token is fine but the caller lacks claims or the portal RBAC grant.
- **No idempotency.** There is no `Idempotency-Key` header. Treat every POST below as
  at-most-once and follow the retry rule in step 6.

## Steps

1. **Find the API product.** Call `ListApiProducts`. Note that an EMPTY catalog returns `404
   "No API Products found"`, not an empty `200` — do not report that as a failure. Take the
   product's `id` from the `APIProductSummary`, then call `GetApiProductById` to read the full
   record, and `ListProductVersions` if the consumer needs a specific version.

2. **Create the team.** `CreateTeam` with the team name. A `409 "User belongs to a team with the
   same name"` means it already exists — call `ListTeams` and reuse the existing `id` rather
   than retrying with the same body. A `404 "User not found"` means the calling user has never
   been provisioned; run `UpsertCurrentUser` first.

3. **Create the application.** `CreateTeamApplication` on `/teams/{teamId}/apps`. A `409
   "Application with the same name already exists in the team"` means it already exists — call
   `ListTeamApplications` and reuse it.

4. **Subscribe the application to the product.** `SubscribeToApiProduct` on
   `/apps/{appId}/subscriptions` with the `apiProductId`. A `409 "Subscription already exists"`
   is a success-equivalent. **The subscription may not be live yet:** the `Subscription` schema
   carries `approved`, `approvedAt` and `rejected`, so a portal configured for approval will
   return an unapproved subscription. Check `approved` before promising the developer access,
   and poll `ListApplicationProductSubscriptions` rather than assuming.

5. **Issue the API key.** `CreateApplicationAPIKey` on `/apps/{appId}/api-keys`.
   **The plaintext key is returned exactly once, in this response, and is never retrievable
   again** — the `APIKey` schema says so. Hand it to the developer or store it now. If it is
   lost, the only remedy is `DeleteAPIKey` and re-issue.
   A `409` means a key with that name already exists on the application; choose another name.

6. **If a step returns 5xx, do not blind-retry a create.** None of these operations is
   idempotent. List the parent collection first (`ListTeams`, `ListTeamApplications`,
   `ListApplicationProductSubscriptions`, `ListApplicationAPIKeys`) and check whether the
   resource actually landed. A retry that succeeds where the first call also succeeded gives you
   a duplicate or a confusing `409`.

## If the consumer needs OAuth instead of an API key

Use `GenerateApplicationOAuthCredential` on `/apps/{appId}/oauth-credentials` instead of step 5.
The client secret is **not stored in the Portal database** — if it is lost, an administrator has
to retrieve it from the OIDC provider. `GetApplicationOAuthCredential` returns the credential
record but not the secret. See `gloo-rotate-portal-credentials`.

## Reversing this

Every step has a reversal and none of them has a stated window:
`DeleteAPIKey` → `DeleteApplicationProductSubscription` → `DeleteApplication` → `DeleteTeam`.
Run them in that order: `DeleteTeam` returns `400 "The team has users or apps associated with
it"` until the team is empty.
