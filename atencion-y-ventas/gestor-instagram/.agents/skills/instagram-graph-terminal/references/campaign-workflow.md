# Campaign preparation and resumable processing

This describes agent-operated preparation and bookkeeping, not an executable queue, listener, scheduler, or exactly-once delivery system. Keep campaign definitions separate from account-global operational state. Copy the campaign and state templates to a private location under `.local/instagram-agent/`; never commit credentials, recipient records, or live state. All campaigns and transports for one account share one canonical state file and one account lock, for example `.local/instagram-agent/accounts/<account-id>/state.json` and `run.lock`.

## Explicit mode and readiness

Set exactly one mode before processing: `one_off`, `periodic`, or `continuous_drain`. Also establish applicable authorization and readiness for each action/transport; template status, test permission, scheduler presence, or a filled resource URL alone grants none.

| Mode | Bounded meaning |
|---|---|
| `one_off` | Complete an audit of every configured post, drain individually eligible actions, then do a final arrivals check. Process newly found arrivals only within this run's scope; report remaining work, incomplete posts, unresolved interactions, or uncertain actions instead of claiming completion. |
| `periodic` | Perform one bounded fair scan/drain cycle per already-authorized schedule occurrence. Changing an interval later updates that same schedule ID only through an authorized available tool; do not create a schedule here. |
| `continuous_drain` | During the current authorized run, scan/drain fairly until verified empty after a final arrivals check, stopped, deadline reached, or blocked. This is best-effort—not an always-on listener, an instant response promise, or endless monitoring. |

`interval_minutes: null` means no periodic interval is configured. It never means “run now,” grants authorization, or changes a draft to active. One-off/continuous modes still require an explicit mode and separate run authorization. Do not infer a default interval or timezone. A controlled test is not audience activation. Check readiness by action and transport: an unpublished app can block API operations that depend on publication, but does not by itself prohibit an independently authorized routine browser action. Never alter app publication/access/permissions here.

Prefer the official API when the exact endpoint, permission, publication state, and response semantics are verified. Use an integrated browser, or an external browser only when explicitly authorized, if the current runtime can inspect the correct account, full thread, action result, stable source interaction ID, and evidence reference. Never infer browser capability for another agent/runtime. API permission errors, limits, restrictions, or warnings are stop conditions, not a reason to switch transports or bypass controls. API/browser handoff must reconcile the account-global ledger before acting; both use the same interaction/action identity and preserve transport-specific evidence.

## Campaign and action identity

Assign every trigger a stable `trigger_id`; every approved message/resource mapping has an explicit `response_version_id` and, where relevant, `resource_version_id`. Do not silently change the meaning of an existing trigger or alter the content/destination behind an approved version. A changed mapping requires a new reviewed version and does not reset prior action history.

Normalize configured trigger phrases and incoming text by Unicode case-folding, trimming outer whitespace, and collapsing internal whitespace. Match an exact complete phrase, not a substring, punctuation-stripped approximation, or hand-enumerated capitalization. If one interaction maps to conflicting triggers, campaigns, response versions, or resources, mark it `ambiguous` and route it to the responsible human/agent without sending.

The account-global action key is `(account_id, source_interaction_id, action_kind)`, where `action_kind` is independently `public_reply` or `private_reply`. It is not campaign- or transport-scoped: one comment matching the same action through two campaigns or after an API/browser handoff remains one action. Preserve `post_id`, candidate campaign IDs, matched stable trigger IDs, approved version IDs, and a stable source interaction ID. If the stable source ID or canonical account identity cannot be verified, do not send. Keep public and private statuses independent; a private reply must not hide an unanswered public action and vice versa.

## Scan, fair backlog, and resume

1. Before acting, verify the authorized account identity and inspect existing manual/native-automation responses for each complete thread. Also verify app/transport prerequisites and relevant platform windows.
2. Acquire one account-level lock by atomic directory creation before any state mutation or send. Record owner/run identity. Every campaign and transport for that account uses this same lock. Never automatically age out, remove, or steal a lock; a stale-looking lock needs human inspection and state reconciliation.
3. Keep exactly one independent scan record per unique `post_id`, with cursor, pages/items observed, metadata count when available, incomplete/complete status, backlog IDs, and last complete coverage watermark. A numeric comment count is metadata, never an error code or proof returned rows are complete. Follow only documented pagination cursors; never infer newest-first or timestamp order. If the cursor lacks a stable post association, query/track each post separately rather than sharing a cursor.
4. Establish a complete initial coverage audit for each post. Process safe eligible interactions from a post as soon as that post's complete thread is known; do not hold all useful work until every unrelated post is loaded. Keep interactions from unfinished posts pending. Interleave recent overlap/head scans fairly with older backlog so arrivals during a long drain are not starved; only advance per-post coverage after every page/thread required for that coverage is read and reconciled.
5. If metadata or an authorized UI indicates comments but the API scan is empty/inconsistent, mark that post `incomplete`, minimally record counts and cursors, preserve backlog and prior watermark, and stop sends dependent on that scan. Do not guess the cause. Store checkpoints/backlog before yielding so the next run can resume without treating partial reads as full coverage.
6. For a candidate action, resolve exact trigger/version, route uncovered contextual questions to a human/agent, and check existing manual/native replies again before writing. Process one public/private mutation at a time; do not assume batch support. Persist `intent_recorded` durably before each network write, keyed globally as above. After the individual result, record transport, platform result/object ID when available, evidence reference, and state before considering another action.
7. On timeout, disconnect, handoff, or ambiguous result, mark that exact action `unknown` and reconcile by reading the same source/action via an authorized path. Never reset intent/history or retry unless authoritative evidence proves the action did not occur. `api_accepted` is not delivered/read; queued status is not acceptance. If no suitable evidence can resolve the state, stop and escalate.
8. Release the account lock only after checkpoints, backlog and action outcomes are durably saved. If lock release or persistence is uncertain, do not start another writer.

## Individual mutations and evidence

Record each attempt under its public or private action with a unique attempt ID, transport (`api` or `browser`), intent/evidence reference, platform result/object ID when available, and observation time. Keep secrets and unnecessary personal data out of state. Stable platform IDs and read-back/evidence references are required to verify the source and outcome; without them, report the limitation and stop rather than claim success. A cross-transport retry is still a retry of the same global action.

Resource URLs belong only in a verified eligible button destination, never naked message text or fallback. First-private-reply buttons remain unverified for this integration: keep resource delivery blocked until a controlled end-to-end test confirms the exact button, recipient, action, and destination. If unavailable in API or browser, do not substitute a text URL. Follow the documented private-reply contract, including eligibility window and response gating for any follow-up; support for one message type does not establish button support for another. Public acknowledgement is considered only after private action confirmation by suitable read-back, and never claims recipient receipt/read.

## State meanings

- `pending`: no network intent for this global action key.
- `intent_recorded`: durable pre-send intent exists; reconcile after restart before any next attempt.
- `api_accepted`: API accepted the request; delivery is not established.
- `confirmed`: suitable read-back/evidence establishes that the specific action exists.
- `unknown`: outcome cannot be established; no retry without proof of absence.
- `incomplete`: post scan/pagination/context is partial or inconsistent; preserve prior coverage and backlog.
- `ambiguous` / `blocked`: conflicting mapping, missing stable identity/capability, or unresolved prerequisite; route or stop without sending.

Templates define a useful record shape only. They do not enforce locking, atomic writes, scheduling, deduplication, or queue draining; never represent these procedures as runtime guarantees.
