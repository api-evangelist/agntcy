---
name: Issue and verify an AGNTCY Identity badge
description: Register an agent or MCP server as an app in the AGNTCY Identity Service, issue it a Verifiable Credential badge, and verify a badge presented by someone else.
api: openapi/agntcy-identity-service-openapi.yaml
base_url: null
auth: bearer-jwt or x-id-api-key
operations:
  - AuthService_Authorize
  - AuthService_Token
  - AppService_CreateApp
  - AppService_CreateOasfApp
  - AppService_ListApps
  - AppService_GetApp
  - BadgeService_IssueBadge
  - AppService_GetBadge
  - BadgeService_VerifyBadge
  - AppService_RefreshAppApiKey
generated: '2026-08-19'
method: generated
source: openapi/agntcy-identity-service-openapi.yaml (harvested verbatim from https://identity-docs.outshift.com/api/openapi/service/v1alpha1/openapi.yaml)
---

# Issue and verify an AGNTCY Identity badge

AGNTCY Identity answers "is this agent who it claims to be". An **app** is a registered agent, MCP
server or tool; a **badge** is a W3C Verifiable Credential asserting that app's identity.

**The Identity Service is self-hosted.** The published OpenAPI declares
`servers: [http://localhost:4000]` — there is no AGNTCY-operated instance to call. Point the base
URL at your own deployment.

## Authentication

Two schemes, both declared in the spec (see `authentication/agntcy-authentication.yml`):

- `AccessToken` — `Authorization: Bearer <jwt>`, an IAM JWT issued to a user during an OIDC flow.
  Get one via `POST /v1alpha1/auth/authorize` (`AuthService_Authorize`) then
  `POST /v1alpha1/auth/token` (`AuthService_Token`).
- `ApiKey` — `x-id-api-key: <key>` header, an IAM API key. Rotate with
  `GET /v1alpha1/apps/{appId}/api-key/refresh` (`AppService_RefreshAppApiKey`).

## Steps

1. **Check the app does not already exist.** `GET /v1alpha1/apps` (`AppService_ListApps`) — this is
   `page`/`size` paginated. There is no idempotency key, so a blind `CreateApp` retry produces a
   duplicate app.
2. **Register the app.** `POST /v1alpha1/apps` (`AppService_CreateApp`) for a plain app, or
   `POST /v1alpha1/apps/oasf` (`AppService_CreateOasfApp`) when you already have an OASF record and
   want the app derived from it. The second is the join between Identity and the Agent Directory —
   prefer it when the agent is published in DIR.
3. **Issue the badge.** `POST /v1alpha1/apps/{appId}/badges` (`BadgeService_IssueBadge`).
4. **Read it back.** `GET /v1alpha1/apps/{appId}/badge` (`AppService_GetBadge`).
5. **Verify a badge you received.** `POST /v1alpha1/badges/verify` (`BadgeService_VerifyBadge`).
   Verify before you trust — an unverified badge is just JSON.

## Rules

- **Errors are gRPC-shaped.** Every operation declares a single `default` response carrying
  `google.rpc.Status` (`code`, `message`, `details[]`), plus an
  `agntcy.identity.core.v1alpha1.ErrorInfo` with a stable `reason` enum. Branch on `reason`, never on
  the human-readable `message`. `ERROR_REASON_VERIFIABLE_CREDENTIAL_REVOKED`,
  `ERROR_REASON_INVALID_PROOF`, `ERROR_REASON_ISSUER_NOT_REGISTERED` and
  `ERROR_REASON_ID_ALREADY_REGISTERED` are the ones this flow hits — full list in
  `errors/agntcy-problem-types.yml`.
- `ERROR_REASON_ID_ALREADY_REGISTERED` on create means step 1 was skipped. Fetch the existing app
  with `GET /v1alpha1/apps/{appId}` (`AppService_GetApp`) rather than retrying.
- **Revocation is real.** A badge that verified yesterday can be revoked. Verify on use, not once at
  onboarding, and treat `ERROR_REASON_VERIFIABLE_CREDENTIAL_REVOKED` as a hard stop.
- The API is `v1alpha1`. Expect breaking changes and pin your client.
