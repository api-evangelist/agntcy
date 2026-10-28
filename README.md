# AGNTCY

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

AGNTCY is the open collective for agent interoperability, initiated by Outshift — Cisco's incubation group — and governed under the Linux Foundation (LF Projects, LLC), developed in the open across 52 public repositories. It publishes specifications rather than a product API: OASF (Open Agentic Schema Framework) for describing agents with a versioned record schema and skill/domain taxonomies, the Agent Directory (DIR) for announcing and discovering multi-agent systems over gRPC, SLIM (Secure Low-Latency Interactive Messaging) as a transport, the Agent Connect Protocol (ACP) as a REST interface for invoking remote agents, and an Identity layer that issues and verifies W3C Verifiable Credential badges for agents, MCP servers and tools. One AGNTCY-operated API exists — the OASF Schema Server at schema.oasf.outshift.com, unauthenticated and callable by anyone; everything else is a specification you implement or software you deploy yourself. It ships SDKs in Python, JavaScript, Go, Rust and .NET, a local-stdio MCP server for the Agent Directory, and SLIMRPC transports for the A2A SDKs in five languages. Everything is Apache-2.0; there is no pricing, no paid tier and no commercial plan.

**Areas:** AI Agents · Interoperability · Specification · Open Source · Agent Discovery · Identity · Agent Directory · MCP · A2A · OpenAPI · gRPC · Protocol Buffers

## AGNTCY on APIs.io

Everything profiled for AGNTCY is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/agntcy/](https://apis.io/providers/agntcy/)** — or go straight to one of the APIs or properties below.

### APIs (21)

- [Agent Directory (DIR)](https://apis.io/apis/agntcy/agent-directory-dir/) — Distributed announce and discovery of multi-agent systems. gRPC-first, with services for storage (content-addressed by CID), routing over a DHT, structured…
- [AGNTCY Agents API](https://apis.io/apis/agntcy/agntcy-agents-api/) — Agents are AI workflows that can be configured and/or executed on this server. This means that a client of this server can start a Run on any of the Agents…
- [AGNTCY App Service API](https://apis.io/apis/agntcy/agntcy-appservice-api/) — AppService manages apps.
- [AGNTCY Badge Service API](https://apis.io/apis/agntcy/agntcy-badgeservice-api/) — BadgeService manages badges.
- [AGNTCY Classes and Objects API](https://apis.io/apis/agntcy/agntcy-classes-and-objects-api/) — The Classes and Objects API from AGNTCY — 4 operation(s) for classes and objects.
- [AGNTCY Device Service API](https://apis.io/apis/agntcy/agntcy-deviceservice-api/) — DeviceService manages device.
- [AGNTCY ID Service API](https://apis.io/apis/agntcy/agntcy-idservice-api/) — IdService is the service that provides ID operations.
- [AGNTCY Issuer Service API](https://apis.io/apis/agntcy/agntcy-issuerservice-api/) — IssuerService is the service that provides ISSUER node operations.
- [AGNTCY JSON Schema API](https://apis.io/apis/agntcy/agntcy-json-schema-api/) — The JSON Schema API from AGNTCY — 4 operation(s) for json schema.
- [AGNTCY Policy Service API](https://apis.io/apis/agntcy/agntcy-policyservice-api/) — PolicyService manages policy.
- [AGNTCY Sample Data API](https://apis.io/apis/agntcy/agntcy-sample-data-api/) — The Sample Data API from AGNTCY — 4 operation(s) for sample data.
- [AGNTCY Schema API](https://apis.io/apis/agntcy/agntcy-schema-api/) — The Schema API from AGNTCY — 8 operation(s) for schema.
- [AGNTCY Settings Service API](https://apis.io/apis/agntcy/agntcy-settingsservice-api/) — SettingsService manages settings.
- [AGNTCY Stateless Runs API](https://apis.io/apis/agntcy/agntcy-stateless-runs-api/) — A Run represents an execution of an agent. The output of a Run can be a final result or an interrupt. Result from a run can be retrieved by polling or by…
- [AGNTCY Taxonomy API](https://apis.io/apis/agntcy/agntcy-taxonomy-api/) — The Taxonomy API from AGNTCY — 3 operation(s) for taxonomy.
- [AGNTCY Thread Runs API](https://apis.io/apis/agntcy/agntcy-thread-runs-api/) — Thread Runs are runs created on a thread. A Thread Run can be created on a thread **only** if there is no run in the `pending` status on the same thread,…
- [AGNTCY Threads API](https://apis.io/apis/agntcy/agntcy-threads-api/) — If supported by the involved agents, Run can be grouped in Threads. When a run is executed on a thread is called Thread Run. At the end of a Thread Run, the…
- [AGNTCY Translation API](https://apis.io/apis/agntcy/agntcy-translation-api/) — The Translation API from AGNTCY — 4 operation(s) for translation.
- [AGNTCY Validation API](https://apis.io/apis/agntcy/agntcy-validation-api/) — The Validation API from AGNTCY — 4 operation(s) for validation.
- [AGNTCY Vc Service API](https://apis.io/apis/agntcy/agntcy-vcservice-api/) — VC is the service that provides VC operations.
- [AGNTCY Auth Service API](https://apis.io/apis/agntcy/agntcy-auth-service-api/) — AuthService manages auth.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Agntcy Events](https://apis.io/asyncapis/agntcy/agntcy-events/)

#### MCP servers (2)

Model Context Protocol servers that expose the API to agents.

- [dir-mcp](https://apis.io/servers/agntcy/dir-mcp/)
- [dir-mcp-server](https://apis.io/servers/agntcy/dir-mcp-server/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Agntcy Agentic Access](https://apis.io/agentic-access/agntcy/agntcy-agentic-access/)

#### JSON Schema (7)

The data models the API reads and writes.

- [Agntcy Identity Badge Claims.Jsonschema](https://apis.io/schemas/agntcy/agntcy-identity-badge-claims.jsonschema/)
- [Agntcy Identity Credential Content.Jsonschema](https://apis.io/schemas/agntcy/agntcy-identity-credential-content.jsonschema/)
- [Agntcy Oasf Dictionary](https://apis.io/schemas/agntcy/agntcy-oasf-dictionary/)
- [Agntcy Oasf Locator](https://apis.io/schemas/agntcy/agntcy-oasf-locator/)
- [Agntcy Oasf Record](https://apis.io/schemas/agntcy/agntcy-oasf-record/)
- [ClientConfig](https://apis.io/schemas/agntcy/agntcy-slim-client-config.schema/)
- [ServerConfig](https://apis.io/schemas/agntcy/agntcy-slim-server-config.schema/)

#### Overlays (4)

OpenAPI overlays, including conversational phrasing for each operation.

- [Agntcy Acp Overlay](https://apis.io/overlays/agntcy/agntcy-acp-overlay/)
- [Agntcy Identity Node Overlay](https://apis.io/overlays/agntcy/agntcy-identity-node-overlay/)
- [Agntcy Identity Service Overlay](https://apis.io/overlays/agntcy/agntcy-identity-service-overlay/)
- [Agntcy Oasf Schema Overlay](https://apis.io/overlays/agntcy/agntcy-oasf-schema-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Agntcy Authentication](https://apis.io/security/agntcy/agntcy-authentication/)
- [Agntcy Domain Security](https://apis.io/security/agntcy/agntcy-domain-security/)
- [Agntcy Vulnerability Disclosure](https://apis.io/security/agntcy/agntcy-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Agntcy Plans Pricing](https://apis.io/plans/agntcy/agntcy-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Agntcy Rate Limits](https://apis.io/rate-limits/agntcy/agntcy-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://outshift.cisco.com/)
- [Documentation](https://docs.agntcy.org/)
- [Getting started](https://dir.agntcy.org/latest/dir/dir-quickstart/)
- [API reference](https://docs.agntcy.org/)
- [Support](https://github.com/orgs/agntcy/discussions)
- [Changelog](https://agntcy.org/changelog)
- [Blog](https://agntcy.org/articles)
- [Security](https://github.com/agntcy/dir/blob/main/SECURITY.md)
- [Terms of service](https://lfprojects.org/policies/terms-of-use/)
- [Privacy policy](https://lfprojects.org/policies/privacy-policy/)
- [GitHub](https://github.com/agntcy)

## API Evangelist rating

**Kin Score 49.0** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 68.3 |
| Contract quality | 59.3 |
| Contract governance | 4.5 |
| Operational transparency | 28.9 |
| Developer ergonomics | 80.4 |
| Access clarity | 21.1 |

**Agent readiness 42.5** — agent-native

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | documented (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | documented (partial credit) |
| Error Semantics | verified |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | paginated |
| Operation Distinctiveness | distinct |

**Regulatory alignment 30.4** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/agntcy/](https://apis.io/providers/agntcy/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for AGNTCY: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/agntcy/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
