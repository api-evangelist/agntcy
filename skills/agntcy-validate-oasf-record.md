---
name: Validate an OASF agent record
description: Validate an agent record against the live Open Agentic Schema Framework schema server before publishing it, and pick the right schema version.
api: openapi/agntcy-oasf-schema-swagger.json
base_url: https://schema.oasf.outshift.com
auth: none
operations:
  - SchemaWeb.SchemaController.versions
  - SchemaWeb.SchemaController.json_object
  - SchemaWeb.SchemaController.sample_object
  - SchemaWeb.SchemaController.validate_object
generated: '2026-08-19'
method: generated
source: openapi/agntcy-oasf-schema-swagger.json (harvested verbatim from https://schema.oasf.outshift.com/doc)
---

# Validate an OASF agent record

The OASF Schema API is served at `https://schema.oasf.outshift.com` by Outshift by Cisco and
takes **no authentication**. Every path is version-addressed, so the first decision is which
schema version you are validating against.

## Steps

1. **Pick the schema version.** `GET /api/{version}/versions` (`SchemaWeb.SchemaController.versions`)
   returns the `default` version plus every version still addressable. As of 2026-08-19 that is
   `0.7.0`, `0.8.0`, `1.0.0` and `1.1.0`, with `1.1.0` as default. Released versions are immutable —
   pin one rather than tracking the default, because the default moves.
2. **Read the object schema.** `GET /schema/{version}/objects/{name}`
   (`SchemaWeb.SchemaController.json_object`) with `name=record` returns the JSON Schema your
   record must satisfy. Required attributes on `record` are `name`, `version`, `schema_version`,
   `description`, `authors` and `created_at`; `annotations` is optional. `created_at` MUST be
   RFC 3339.
3. **Get a worked example if you need one.** `GET /sample/{version}/objects/{name}`
   (`SchemaWeb.SchemaController.sample_object`) returns a generated sample of that object.
4. **Validate.** `POST /api/{version}/validate/object/{name}` with `name=record` and the record as
   the JSON body (`SchemaWeb.SchemaController.validate_object`). Fix and re-post until clean.

## Rules

- **Do not invent taxonomy values.** `skills` and `domains` must come from the OASF taxonomy —
  use the `agntcy-navigate-oasf-taxonomy` skill to resolve them before validating.
- `schema_version` in the record must match the `{version}` you validate against, or you will get
  errors that look like missing attributes.
- **Errors.** `400` means your `id` and `name` query parameters refer to different classes.
  `404` means no class exists with that id or name. Bodies are plain `application/json`; this API
  does not use RFC 9457 problem+json (see `errors/agntcy-problem-types.yml`).
- No rate limits are documented and no `RateLimit-*` headers are returned, but this is a community
  convenience instance with no SLA — back off on failure rather than hammering it.
- Prefer the MCP route when you have it: `agntcy_oasf_validate_record` wraps step 4 and
  `agntcy_dir_push_record` validates before it writes (see `mcp/agntcy-mcp.yml`).
