---
name: Navigate the OASF skill and domain taxonomy
description: Resolve real OASF skill and domain identifiers by walking the hierarchical taxonomy on the live schema server, so an agent record is annotated with values that exist.
api: openapi/agntcy-oasf-schema-swagger.json
base_url: https://schema.oasf.outshift.com
auth: none
operations:
  - SchemaWeb.SchemaController.skill_categories
  - SchemaWeb.SchemaController.domain_categories
  - SchemaWeb.SchemaController.skills
  - SchemaWeb.SchemaController.domains
  - SchemaWeb.SchemaController.dictionary
generated: '2026-08-19'
method: generated
source: openapi/agntcy-oasf-schema-swagger.json (harvested verbatim from https://schema.oasf.outshift.com/doc)
---

# Navigate the OASF skill and domain taxonomy

OASF annotates a record with **skills** (what an agent can do) and **domains** (the subject area it
works in). Both are hierarchies, and both are closed vocabularies — a value you make up will fail
validation.

## Steps

1. **List the top of the tree.** `GET /api/{version}/skill_categories`
   (`SchemaWeb.SchemaController.skill_categories`) with no `id` or `name` returns the top-level
   skill categories. Same shape for `GET /api/{version}/domain_categories`
   (`SchemaWeb.SchemaController.domain_categories`).
2. **Walk down.** Re-call the same operation with `name` set to a parent to get only that parent's
   direct children. `name` accepts either hierarchical form
   (`natural_language_processing/natural_language_understanding/contextual_comprehension`) or the
   simple leaf form (`contextual_comprehension`). `id` (numeric) does the same job.
3. **Get the flat list when you need it.** `GET /api/{version}/skills`
   (`SchemaWeb.SchemaController.skills`) and `GET /api/{version}/domains`
   (`SchemaWeb.SchemaController.domains`) return the full sets.
4. **Look up attribute meanings.** `GET /api/{version}/dictionary`
   (`SchemaWeb.SchemaController.dictionary`) is the attribute dictionary behind every object.

## Rules

- **Never pass both `id` and `name` unless they refer to the same class** — the API returns `400`
  with "id and name parameters refer to different classes".
- A `404` here means the class does not exist at that version. Do not retry with a guessed spelling;
  walk the tree from step 1 instead.
- Pin `{version}`. The taxonomy grows between schema versions, so a skill resolved against `1.1.0`
  may not exist in `0.8.0`.
- `extensions` is an optional array query parameter on most of these operations; pass it only when
  you are working against a schema server that hosts private extensions.
