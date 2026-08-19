---
name: Publish and discover an agent in the Agent Directory
description: Validate an OASF record, push it to a Directory server, announce it to the routing network, and find and verify other agents — through the dir-mcp tools or dirctl.
api: mcp/agntcy-mcp.yml
base_url: null
auth: oidc
operations:
  - agntcy_oasf_validate_record
  - agntcy_dir_push_record
  - agntcy_dir_search_local
  - agntcy_dir_pull_record
  - agntcy_dir_verify_record
  - agntcy_dir_verify_name
  - agntcy_oasf_import_record
  - agntcy_oasf_export_record
generated: '2026-08-19'
method: generated
source: https://github.com/agntcy/dir-mcp/blob/main/docs/directory-mcp.md and grpc/ in this repo
---

# Publish and discover an agent in the Agent Directory

The Agent Directory (DIR) is **gRPC-first** and has no published OpenAPI. The two supported client
paths are the `dirctl` CLI and the local-stdio MCP server it hosts (`dirctl mcp serve`). The tool
names below are MCP tools, not REST operations.

**There is no AGNTCY-hosted Directory you can just call.** You point a client at a Directory server —
your own local node (`0.0.0.0:8888` by default) or a gateway your organization runs. Authenticate
first: `dirctl auth login --oidc-issuer <issuer> --oidc-client-id dirctl`, or set
`DIRECTORY_CLIENT_AUTH_MODE=oidc` with `DIRECTORY_CLIENT_AUTH_TOKEN`.

## Steps — publishing

1. **Validate first.** `agntcy_oasf_validate_record` with the record JSON. Do not push an invalid
   record; the push will validate anyway and you will have burned a round trip.
2. **Push.** `agntcy_dir_push_record` returns a **CID** — a multiformats content identifier derived
   from the artifact digest — plus the server address it landed on. **Keep the CID.** It is the
   record's identity everywhere else in DIR.
3. **Announce it.** Pushing stores; it does not advertise. Use `dirctl routing publish` to announce
   the record's labels (skills, domains, modules, locators) to the DHT so other nodes can find it.

## Steps — discovering

4. **Search.** `agntcy_dir_search_local` takes structured filters: `names`, `versions`, `skill_ids`,
   `skill_names`, `locators`, `module_names`, `module_ids`, `domain_ids`, `domain_names`, `authors`,
   `created_ats`, `schema_versions`. Wildcards are `*` (zero or more), `?` (exactly one) and
   `[abc]` (character class). **Multiple filters combine with OR, not AND** — this surprises people.
   Pagination is `limit` (default 100, max 1000) and `offset`; the response carries `count` and
   `has_more`. Read every CID out of `record_cids`.
5. **Pull.** `agntcy_dir_pull_record` with the CID returns the record. It is content-addressed, so
   you can re-hash and confirm you got what you asked for.
6. **Verify before you trust.** `agntcy_dir_verify_record` checks the record's signature.
   `agntcy_dir_verify_name` checks that a URL-shaped record name is actually owned by that domain,
   by matching the signing key against the domain's `/.well-known/jwks.json`. **Discovery is not
   trust — an unverified record is an unverified claim.**

## Rules

- **Push is idempotent by construction.** The same bytes produce the same CID, so re-pushing does not
  duplicate. There is no `Idempotency-Key` header anywhere in AGNTCY — content addressing is the
  mechanism (see `conventions/agntcy-conventions.yml`).
- **Records are immutable.** A change is a new record with a new CID, not an edit.
- **Errors are gRPC status codes:** `InvalidArgument`, `NotFound`, `FailedPrecondition`, `Internal`,
  `Canceled`, `Unauthenticated`, `PermissionDenied`. `Unauthenticated` almost always means an expired
  OIDC token — re-run `dirctl auth login --force` and restart the MCP server so the cached token is
  reloaded.
- **Name verification only works on URL-based names** (`https://example.com/my-agent`). A bare name
  cannot be domain-verified.
- **Interop:** `agntcy_oasf_import_record` converts an MCP server manifest, an A2A agent card or an
  Agent Skills `SKILL.md` into an OASF record; `agntcy_oasf_export_record` goes the other way to
  `a2a`, `ghcopilot` or `agentskills`. Use these rather than hand-mapping fields.
