---
name: Invoke a remote agent over the Agent Connect Protocol
description: Discover a remote agent, read its ACP descriptor, and run it statelessly — including the streaming and cancel paths.
api: openapi/agntcy-acp-openapi.json
base_url: null
auth: implementation-defined
operations:
  - search_agents
  - get_agent_by_id
  - get_acp_descriptor_by_id
  - create_stateless_run
  - create_and_wait_for_stateless_run_output
  - get_stateless_run
  - stream_stateless_run_output
  - cancel_stateless_run
  - delete_stateless_run
generated: '2026-08-19'
method: generated
source: openapi/agntcy-acp-openapi.json (harvested verbatim from https://spec.acp.agntcy.org/openapi.json)
---

# Invoke a remote agent over ACP

The Agent Connect Protocol is a **specification**, not a hosted service. AGNTCY publishes the
OpenAPI (3.1.1, version 0.2.3) and the spec declares **no `servers[]`** — the base URL is whatever
agent server you are pointed at, and its authentication is that server's choice. Resolve the base
before you start; do not assume one.

## Steps

1. **Find the agent.** `POST /agents/search` (`search_agents`) with your filter criteria, or go
   straight to `GET /agents/{agent_id}` (`get_agent_by_id`) if you already have the id.
2. **Read the contract before calling it.** `GET /agents/{agent_id}/descriptor`
   (`get_acp_descriptor_by_id`) returns the ACP descriptor: the input, output and config schemas
   this specific agent accepts. **Validate your payload against the descriptor, not against a
   guess.** Two ACP agents on the same server take different inputs.
3. **Run it.** Pick one:
   - `POST /runs/wait` (`create_and_wait_for_stateless_run_output`) — create and block for the
     result. Simplest, best for short runs.
   - `POST /runs/stream` (`create_and_stream_stateless_run_output`) — create and stream output.
   - `POST /runs` (`create_stateless_run`) — create and return immediately, then poll
     `GET /runs/{run_id}` (`get_stateless_run`), block on `GET /runs/{run_id}/wait`
     (`wait_for_stateless_run_output`), or attach with `GET /runs/{run_id}/stream`
     (`stream_stateless_run_output`).
4. **Cancel or clean up.** `POST /runs/{run_id}/cancel` (`cancel_stateless_run`) stops a run;
   `DELETE /runs/{run_id}` (`delete_stateless_run`) removes it.

## Rules

- **Stateless runs keep no conversation.** If the agent needs to remember earlier turns, use the
  `agntcy-run-stateful-acp-thread` skill instead.
- **Errors.** `422 Validation Error` means the body did not match the descriptor's schema — re-read
  the descriptor, do not retry unchanged. `404` means the agent or run id does not exist.
  `409 Conflict` appears on the create paths when the resource is already in an incompatible state.
  All bodies are plain `application/json`.
- **Pagination** on the search and list operations is `limit` / `offset`, with `before` for
  cursoring backwards.
- **Idempotency.** ACP defines no `Idempotency-Key` header. A retried `create_stateless_run` creates
  a second run. Prefer `create_and_wait_for_stateless_run_output` and treat a timeout as unknown, not
  as failed — reconcile with `get_stateless_run` before retrying.
