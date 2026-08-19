---
name: Run a stateful ACP conversation on a thread
description: Create an ACP thread, run an agent inside it across turns, resume an interrupted run, and read the thread history.
api: openapi/agntcy-acp-openapi.json
base_url: null
auth: implementation-defined
operations:
  - create_thread
  - search_threads
  - get_thread
  - patch_thread
  - copy_thread
  - get_thread_history
  - create_thread_run
  - create_and_wait_for_thread_run_output
  - wait_for_thread_run_output
  - get_thread_run
  - resume_thread_run
  - cancel_thread_run
  - delete_thread
generated: '2026-08-19'
method: generated
source: openapi/agntcy-acp-openapi.json (harvested verbatim from https://spec.acp.agntcy.org/openapi.json)
---

# Run a stateful ACP conversation on a thread

A **thread** is ACP's unit of conversational state. Runs inside a thread see the thread's history;
stateless runs do not.

## Steps

1. **Create the thread.** `POST /threads` (`create_thread`). Reuse an existing one with
   `POST /threads/search` (`search_threads`) or `GET /threads/{thread_id}` (`get_thread`).
2. **Run the agent in it.** `POST /threads/{thread_id}/runs/wait`
   (`create_and_wait_for_thread_run_output`) for the blocking path, `POST /threads/{thread_id}/runs/stream`
   (`create_and_stream_thread_run_output`) to stream, or `POST /threads/{thread_id}/runs`
   (`create_thread_run`) to fire and poll with `GET /threads/{thread_id}/runs/{run_id}`
   (`get_thread_run`).
3. **Handle an interrupt.** When a run stops for input, `POST /threads/{thread_id}/runs/{run_id}`
   (`resume_thread_run`) continues it with the payload it asked for. This is the operation that makes
   human-in-the-loop work; do not create a new run instead.
4. **Read what happened.** `GET /threads/{thread_id}/history` (`get_thread_history`) returns the
   conversation. `GET /threads/{thread_id}/runs` (`list_thread_runs`) lists the runs on it.
5. **Fork or amend.** `POST /threads/{thread_id}/copy` (`copy_thread`) branches a thread —
   the right move before a destructive experiment. `PATCH /threads/{thread_id}` (`patch_thread`)
   updates thread metadata.
6. **Clean up.** `POST /threads/{thread_id}/runs/{run_id}/cancel` (`cancel_thread_run`),
   `DELETE /threads/{thread_id}/runs/{run_id}` (`delete_thread_run`), then
   `DELETE /threads/{thread_id}` (`delete_thread`).

## Rules

- **Copy before you destroy.** `copy_thread` is cheap; a deleted thread's history is gone.
- **`409 Conflict`** on `create_thread_run` normally means a run is already active on that thread.
  Poll `get_thread_run` or cancel the existing run rather than retrying blind.
- **`422 Validation Error`** means the input did not match the agent's ACP descriptor
  (`get_acp_descriptor_by_id`). Re-read the descriptor.
- **No idempotency key exists.** A retried `create_thread` makes a second thread. Search first.
- The base URL and auth scheme belong to the agent server implementing ACP, not to AGNTCY.
