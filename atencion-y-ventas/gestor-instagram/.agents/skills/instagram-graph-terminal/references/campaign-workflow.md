# Campaign preparation and resumable processing

Use this reference only for multi-publication keyword campaigns or recurring checks. These instructions describe agent-operated preparation and bookkeeping; they do not create a scheduler, listener, deterministic queue, or exactly-once delivery guarantee.

## Configuration

Keep campaign definitions separate from runtime state. Copy `assets/campaign.template.json` and `assets/state.template.json` to a private local location under `.local/instagram-agent/`; do not put credentials, real recipient data, or live campaign records in the repository. The local ignore rule excludes `.local/instagram-agent/`. Use generic IDs and placeholders until the user supplies verified details. Preserve confirmed account/post/resource identities, exact trigger phrases, response text, button label/action/destination, interval, timezone, and activation evidence. Multiple posts may share a resource or have distinct resources. Never invent missing values.

Before processing, verify the app's publication/availability status and the required access in the authorized dashboard and current documentation. If unpublished or unverified, mark work blocked; do not publish the app, change access, or permissions as part of this workflow. Missing comment rows may have multiple causes: do not infer a cause from an empty response alone.

An interval change updates the existing authorized scheduler entry by its stable scheduler ID when the user later authorizes that operation; retain campaign identity, state, send history, and checkpoints. Do not create or delete schedules as part of preparation. A null interval means process now, not a guessed recurring schedule. Never infer timezone or timing from machine defaults.

Normalize configured trigger phrases and incoming text by Unicode case-folding, trimming outer whitespace, and collapsing internal whitespace. Match an exact complete phrase, not a substring, punctuation-stripped approximation, or hand-enumerated capitalization. If normalization makes duplicate phrases map to different actions, or one interaction matches overlapping rules/resources, mark it ambiguous and route for human/agent resolution without sending.

## Safe scan and resume

1. Acquire the account's single-writer lock by atomic directory creation before reading or changing state. Record owner/run identity and acquisition time. Never automatically break, age out, or steal a lock; an apparently stale lock requires a human to inspect the owner and reconcile state.
2. Read every page of eligible comments and each complete reply thread. Compare returned rows/pages with available post metadata and UI evidence. If metadata or another authorized view indicates comments but the API scan is empty or inconsistent, mark the scan `incomplete`, record counts/cursors minimally, retain pending state, do not advance the full-coverage watermark, and stop dependent sends. Persist the current page/cursor checkpoint and any unprocessed backlog so a later run resumes without treating partial reads as complete. Do not act on a thread whose complete context could not be read.
3. For each interaction, check existing manual and native-automation responses before deciding. Route contextual questions not covered by an explicit button choice to the responsible human/agent. Do not send multiple matching resource responses.
4. Use stable source interaction IDs and distinct action keys for public reply and private reply. Before each network write, persist a durable `intent_recorded` state for that exact action. After confirmed API acceptance, record `api_accepted`; this is not proof of delivery/read. Keep public and private outcomes independent.
5. On timeout, disconnect, lock uncertainty, or any unclear result, persist `unknown` and reconcile with a read before considering another attempt. Never reset `intent_recorded`/`unknown`, clear history, or retry unless authoritative state proves the action did not occur. If state remains uncertain, stop and escalate.
6. A public acknowledgement may be considered only after the private action is confirmed by a suitable read-back; queueing or API acceptance alone is insufficient. Do not claim receipt/read. The state record reduces duplicate work but cannot guarantee exactly-once effects across network failures.
7. Release the lock only after checkpoint, backlog, and action states are durably saved. If release is uncertain, stop rather than start another writer.

Resource URLs belong only in an eligible button destination, never as naked message text or fallback. Support for buttons in the first private reply is unverified for this integration. Keep the campaign inactive until a controlled end-to-end test confirms the exact button, recipient, action and destination. If unsupported or unclear, do not substitute a text URL; stop and ask for a decision.

Follow the currently documented private-reply contract for the integration: address the reply to the eligible comment, use the supported text body, respect its seven-day eligibility window, and send a follow-up only after the recipient responds and within the documented 24-hour window. Do not infer that these constraints establish support for buttons in the first reply.

## State meanings

- `pending`: eligible interaction, no network intent recorded.
- `incomplete`: scan evidence conflicts or pagination/context is incomplete; preserve backlog and do not process dependent sends.
- `intent_recorded`: durable pre-send intent exists; after a crash, reconcile before any further action.
- `api_accepted`: API accepted the request; delivery is not established.
- `confirmed`: read-back provides evidence the action exists.
- `unknown`: outcome cannot be established; do not retry without proof of absence.
- `ambiguous` / `blocked`: conflicting triggers, incomplete context, missing capability, or unresolved prerequisite; route to a human/agent.

The state template is a shape for agent-operated records, not executable queue configuration. Keep recipient-specific data out of committed templates and logs.
