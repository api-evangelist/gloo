---
name: gloo-rotate-portal-credentials
description: Rotate or revoke a Gloo Portal application's credentials — API keys and OAuth client credentials — knowing which secret values are recoverable and which are gone forever once issued.
api: gloo:gloo-portal
spec: openapi/gloo-portal-server-openapi.yaml
operations:
  - ListApplicationAPIKeys
  - CreateApplicationAPIKey
  - DeleteAPIKey
  - GetApplicationOAuthCredential
  - GenerateApplicationOAuthCredential
  - DeleteOAuthCredential
  - CreateOAuthApplication
  - DeleteOAuthApplication
generated: '2026-09-12'
method: generated
source: openapi/gloo-portal-server-openapi.yaml, openapi/gloo-portal-idp-connect-openapi.yaml, authentication/gloo-authentication.yml
---

# Rotate or revoke Gloo Portal application credentials

## The one thing to get right

**Secret material is shown once and is never recoverable from the Portal.**

- `APIKey.apiKey` — "Is returned only once when the API key is created". There is no
  read-key-again operation.
- OAuth client secret — not stored in the Portal database at all. Solo's own documentation
  directs an administrator to the OIDC provider to recover a lost one.

So a rotation is always *create-then-delete*, never *delete-then-create*: if you delete first
and the create fails, the consumer is down with nothing to fall back to.

## Rotate an API key (zero-downtime order)

1. `ListApplicationAPIKeys` on `/apps/{appId}/api-keys` — record the existing key ids and names.
2. `CreateApplicationAPIKey` with a NEW name (reusing a name returns `409 "An API key with the
   same name already exists in the application"`). Capture the returned `apiKey` value now.
3. Deploy the new key to the consumer and confirm it works against the gateway.
4. Only then `DeleteAPIKey` on `/api-keys/{keyId}` for the old key.

`DeleteAPIKey` returns `403` when the caller's token is valid but lacks the required claims, and
`404` when the key UUID or the user does not exist. Both are terminal — do not retry.

## Rotate an OAuth client credential

1. `GetApplicationOAuthCredential` on `/apps/{appId}/oauth-credentials` to see what exists.
2. `GenerateApplicationOAuthCredential` returns `409 "Application credentials already exist"` if
   one is already present — so unlike the API-key path, this rotation **cannot** be
   create-then-delete. You must `DeleteOAuthCredential` on `/oauth-credentials/{credentialId}`
   first and accept a gap, or coordinate the cutover with the operator.
3. Re-run `GenerateApplicationOAuthCredential` and capture the secret from that response.

Plan the outage window before you start. This is the one credential path in Gloo Portal with an
unavoidable gap.

## The IdP Connect layer

`CreateOAuthApplication` and `DeleteOAuthApplication` (`openapi/gloo-portal-idp-connect-openapi.yaml`)
act on the OAuth2 client **in the OIDC provider itself**, not on the Portal's record of it. They
take an optional `token` header naming the originating user, and they are the only two
operations in the Gloo surface that return a structured error body (`Error` with required
`code`, `message`, `reason`). If the portal record and the IdP client have drifted apart, this is
the layer to reconcile at — but deleting the IdP client will break every credential the Portal
still believes is valid.

## Auditing before you rotate

`ListApplicationProductSubscriptions` on `/apps/{appId}/subscriptions` tells you what the
application is actually entitled to call, so you know what a bad rotation would break.
