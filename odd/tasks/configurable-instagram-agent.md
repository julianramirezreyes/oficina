# Configurable Instagram agent

## Objective and authorized scope
Extend the existing instruction-driven Instagram workflow so any agent in the folder can configure multiple publications, normalized keywords, shared or different resources, and durable pending work. Support one-off scans, periodic runs, and best-effort continuous draining; prefer supported official API operations and permit an integrated/authorized browser path only when capable. Resource links must be buttons, never bare URLs. The user authorized local preparation and controlled tests on their accounts, including the existing `agente-ig-prueba` task. No audience campaign or recurring schedule is activated by this preparation.

## Design and constraints
- Keep permanent safety/routing in the department AGENTS.md; extend the existing skill rather than add another agent/application.
- Separate campaign definitions from operational state; interval changes must preserve delivery identity and history.
- No scripts, service, daemon, new app, credential changes, or deployment. Existing policy prohibits scripts/apps.
- A documented queue is an agent-operated record, not a deterministic executable engine or delivery guarantee.
- Preserve pre-existing untracked skill/registry content. No secrets or recipient records committed.
- Buttons in the initial private reply remain unverified for the current integration. Never fall back to a naked link.
- Public acknowledgment requires confirmed private send; API acceptance is not proof of recipient receipt/read.
- Each post has independent pagination/checkpoint/coverage; interleave recent overlap scans fairly with older backlog without inferring newest-first ordering.
- Use an account-global lock and action ledger shared across campaigns and transports; action identity is `(account, source interaction, action kind)`, with stable trigger IDs and approved response/resource version IDs.
- Require explicit processing mode, authorization and per-action readiness. A null interval is not execution or activation permission.
- Mutations are sequential individual actions, each reconciled separately; never assume batch support or exactly-once delivery.
- One-off means complete scan, eligible drain, and final-arrivals check; periodic means one bounded cycle; continuous means best-effort until verified drained, stopped, deadline, or blocker—not endless/instant monitoring.

## Tasks
- [x] T1 — Extend skill, local routing, campaign template and state procedure (delegated: multiple non-trivial instruction/config files). Include normalized matching, overlap resolution, complete pagination, durable separate action states, concurrent-run exclusion and uncertain-outcome reconciliation.
- [x] T2 — Correct instructions/templates using the independent scenario findings: per-post scans/evidence, stable trigger IDs, cross-campaign/transport deduplication, explicit modes/readiness, and fair backlog behavior (bounded writer).
- [ ] T3 — Check live prerequisites and conduct a single eligible controlled button test if possible; otherwise preserve exact blocker without audience sends (parent browser/API owner).
- [x] T4 — Independently verify corrected instructions/templates against timeout, concurrent agents, multi-campaign matches, transport handoff, null draft, and arrivals during scans; keep executable/runtime behavior explicitly unimplemented.

## Acceptance and checks
- Agent can explain/configure multi-post rules and update 20/30-minute intervals without resending.
- No keyword match based solely on case enumeration; no ambiguous multi-resource sends.
- No resource URLs in message bodies; missing button evidence blocks activation.
- No sending from incomplete reads or uncertain prior states; no stale-lock bypass.
- Skill validator, JSON parse, local reference existence and `git diff --check` pass.
- Independent scenario run distinguishes instructions from implementation and API acceptance from delivery.
- Timeout, lock contention, overlapping campaigns, and transport handoff never create a second action without proof of absence.
- Draft/null schedule state never starts work; each run mode has a bounded, explicit completion condition.
- Live success requires evidence of the correct button, recipient and destination; report unavailable checks explicitly.

## Verification configuration
Strict TDD: enabled by project instructions. This unit changes instructions/configuration only; no executable code or existing test runner. Use baseline and post-change behavioral scenario evaluations plus structural checks; do not claim runtime TDD or an implemented queue engine. Receipt-driven development: off (global, verified 2026-10-02). Native risk assessment still informs independent verification; no RDD lifecycle.

## Delivery
Existing feature branch: `policy/instagram-response-automation`. Start boundary: `b31f51c`.
T1 authored 201 lines; T2 correction adds 170 lines (371 total from the start boundary, below the 400-line review budget). T2 commit: `02f21a069fbc81d99a9cc8b449403e8a564ce587`. Strategy: ask-on-risk. No push or PR.
Rollback: revert this unit's skill/routing/template/procedure edits, preserving any future local operational data.

## Evidence and progress
- Baseline test task confirmed no reusable registry/queue or scheduler exists; first private-reply buttons unverified.
- Read-only map found no executable runtime; existing .agents/.atl and root .codegraph are pre-existing untracked files.
- T1 evidence: commit `d2c9cca` added campaign/state JSON templates, campaign workflow reference, runtime-data ignore rule, and Spanish routing in the Instagram instructions. Structural checks passed: skill quick validator, both JSON parses, local reference existence, and `git diff --check`.
- T1 scenario readback: case/space variants normalize to one exact phrase; overlapping action matches block; incomplete or conflicting pagination preserves backlog and blocks sends; existing manual/native responses are checked; stale locks are not auto-broken; private/public intent records remain separate and durable before writes; unknown outcomes do not retry; interval updates preserve state; accepted/queued status does not prove delivery or permit a public receipt.
- Live read-only evidence for T3 (not a completion): authorized account identity checks matched, but known post metadata indicated comments while the documented comment scan returned no rows across all cursor pages without an API error. The app dashboard reports unpublished status, and the cause of the empty scan is not established. Preserve pending state/watermark and stop sends dependent on the inconsistent scan. API readiness is blocked where app publication is required; any routine browser action needs a separate capability/authorization/readiness check. No sends or app/access changes were made; first-reply buttons remain unverified.
- Independent read-test finding for T2: current state had one cursor/backlog for all posts, interaction records omitted post ID, campaign triggers lacked stable IDs, cross-campaign dedupe was undefined, and null-interval wording risked draft execution. Corrections remain instructional/templates only; no executable runtime is authorized.
- T2 scenario readback: timeout -> unknown/reconcile/no blind retry; second writer -> shared account lock stops it, with no stale-lock takeover; same interaction across campaigns/transports -> one global public/private action key, conflicting mappings -> ambiguous/no send; uncertain transport handoff -> read/reconcile under same key and API permission/limit failures stay stopped; draft/null mode -> no work until explicit mode, authorization, and per-action readiness; arrivals during post scans -> fair per-post overlap/backlog handling and a final-arrivals pass, with no “drained” claim when rows remain or scan completeness is uncertain.
- T2 structural verification: skill quick validator, both JSON parses, local reference existence, and `git diff --check` passed on the committed source candidate. One initial JSON command had a mistyped state-template path; the corrected exact command passed. No live API/browser/schedule/app operation was run for this correction.
- T4 evidence: `agente-ig-prueba` independently returned PASS for instructions and state representation at `c7c6672`; skill validator, both JSON parses, linked references, and `git show --check 02f21a0` passed. Parent spot checks of `02f21a0` and `c7c6672` also passed. This is not runtime or live-delivery proof.
- Next: resolve the inconsistent live comment read and verify a single eligible initial DM button end to end. T3 remains pending/blocked; no audience sends, schedule activation, or app publication/access changes were performed. The app publication screen also showed a missing privacy-policy URL and disabled publish control; its causal connection to empty comment pages is unproven.
