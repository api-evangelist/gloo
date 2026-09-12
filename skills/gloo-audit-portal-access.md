---
name: gloo-audit-portal-access
description: Audit who can call what in a Gloo Portal — walk teams, members, applications, subscriptions and credentials to produce an access picture, using only read operations.
api: gloo:gloo-portal
spec: openapi/gloo-portal-server-openapi.yaml
operations:
  - GetCurrentUser
  - ListTeams
  - GetTeamById
  - ListTeamMembers
  - ListTeamApplications
  - GetApplicationById
  - ListApplicationAPIKeys
  - GetApplicationOAuthCredential
  - ListApplicationProductSubscriptions
  - ListSubscriptionsByStatus
  - ListApiProducts
generated: '2026-09-12'
method: generated
source: openapi/gloo-portal-server-openapi.yaml, data-model/gloo-data-model.yml, conventions/gloo-conventions.yml
---

# Audit access in a Gloo Portal

Every operation in this skill is a **read**. Nothing here changes state, so it is safe to run
unattended.

## Confirm who you are first

`GetCurrentUser` on `/me`. This operation permits anonymous access (`security: [{identityToken:
[]}, {}]`), so a `200` does **not** prove you are authenticated — read the body. A `404 "User
not found"` means the token's subject has never been provisioned into this portal.

## The walk

1. `ListTeams` → for each team id:
2. `GetTeamById` → the team record.
3. `ListTeamMembers` on `/teams/{teamId}/members` → who is in it.
4. `ListTeamApplications` on `/teams/{teamId}/apps` → for each app id:
5. `GetApplicationById`, then
   - `ListApplicationAPIKeys` on `/apps/{appId}/api-keys` — key **metadata** only; the key values
     are not readable and never will be.
   - `GetApplicationOAuthCredential` on `/apps/{appId}/oauth-credentials` — credential record,
     not the secret.
   - `ListApplicationProductSubscriptions` on `/apps/{appId}/subscriptions` — what this app may
     actually call.
6. Cross-check with `ListSubscriptionsByStatus` on `/subscriptions?status=...`, which gives the
   portal-wide view. An unrecognised status value returns `400 "Invalid status parameter."`
7. `ListApiProducts` gives the catalog side of the join, and `GetApiProductById` the detail.

## Three traps that will corrupt the audit

- **Empty is 404, not 200.** `ListApiProducts` returns `404 "No API Products found"` and
  `ListTeams` returns `404 "Teams not found"` when the collection is empty. Count these as zero,
  not as an error, or a fresh portal will read as a broken one.
- **There is no pagination.** No `limit`, `offset`, `page` or `cursor` exists on any operation
  in this API. Every list returns the whole collection in one unbounded response. On a large
  portal, size your client's timeouts and response-body limits accordingly — there is no way to
  chunk the request.
- **`approved` is not a status field.** A subscription's state lives in flat booleans plus
  timestamps (`approved`, `approvedAt`, `rejected`) on the resource; the status *enum* exists
  only as a query parameter on `ListSubscriptionsByStatus`. Read the booleans on the record.

## What this audit cannot tell you

The rate limits and auth policies actually enforced on a call are attached by the operator to
the gateway, not exposed on these resources. On a Gloo **Platform** portal, `GetUsagePlans`
(`openapi/gloo-platform-portal-openapi.yaml`) returns `UsagePlan` objects carrying
`rateLimitPolicy` and `authPolicies` — the newer Gloo Portal Server contract dropped that
operation, so on Gloo Gateway portals you must ask the operator.
