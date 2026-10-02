# Configurable Instagram agent

## Objective and authorized scope
Extend the existing instruction-driven Instagram terminal workflow so any agent in the folder can configure multiple publications, normalized keywords, shared or different resources, variable schedules, and persistent pending work. Resource links must be buttons, never bare URLs. The user authorized local preparation and controlled tests on their accounts, including the existing `agente-ig-prueba` task. No audience campaign or recurring schedule is activated by this preparation.

## Design and constraints
- Keep permanent safety/routing in the department AGENTS.md; extend the existing skill rather than add another agent/application.
- Separate campaign definitions from operational state; interval changes must preserve delivery identity and history.
- No scripts, service, daemon, new app, credential changes, or deployment. Existing policy prohibits scripts/apps.
- A documented queue is an agent-operated record, not a deterministic executable engine or delivery guarantee.
- Preserve pre-existing untracked skill/registry content. No secrets or recipient records committed.
- Buttons in the initial private reply remain unverified for the current integration. Never fall back to a naked link.
- Public acknowledgment requires confirmed private send; API acceptance is not proof of recipient receipt/read.

## Tasks
- [x] T1 — Extend skill, local routing, campaign template and state procedure (delegated: multiple non-trivial instruction/config files). Include normalized matching, overlap resolution, complete pagination, durable separate action states, concurrent-run exclusion and uncertain-outcome reconciliation.
- [ ] T2 — Independently exercise changed instructions with the existing test task and structural checks; correct concrete findings (delegated verification).
- [ ] T3 — Check live prerequisites and conduct a single eligible controlled button test if possible; otherwise preserve exact blocker without audience sends (parent browser/API owner).

## Acceptance and checks
- Agent can explain/configure multi-post rules and update 20/30-minute intervals without resending.
- No keyword match based solely on case enumeration; no ambiguous multi-resource sends.
- No resource URLs in message bodies; missing button evidence blocks activation.
- No sending from incomplete reads or uncertain prior states; no stale-lock bypass.
- Skill validator, JSON parse, local reference existence and `git diff --check` pass.
- Independent scenario run distinguishes instructions from implementation and API acceptance from delivery.
- Live success requires evidence of the correct button, recipient and destination; report unavailable checks explicitly.

## Verification configuration
Strict TDD: enabled by project instructions. This unit changes instructions/configuration only; no executable code or existing test runner. Use baseline and post-change behavioral scenario evaluations plus structural checks; do not claim runtime TDD or an implemented queue engine. Receipt-driven development: off (global, verified 2026-10-02). Native risk assessment still informs independent verification; no RDD lifecycle.

## Delivery
Existing feature branch: `policy/instagram-response-automation`. Start boundary: `b31f51c`.
Forecast: approximately 250–350 authored lines including the existing untracked skill when added. Strategy: ask-on-risk. No push or PR.
Rollback: revert this unit's skill/routing/template/procedure edits, preserving any future local operational data.

## Evidence and progress
- Baseline test task confirmed no reusable registry/queue or scheduler exists; first private-reply buttons unverified.
- Read-only map found no executable runtime; existing .agents/.atl and root .codegraph are pre-existing untracked files.
- T1 evidence: added campaign/state JSON templates, campaign workflow reference, runtime-data ignore rule, and Spanish routing in the Instagram instructions. Structural checks passed: skill quick validator, both JSON parses, local reference existence, and `git diff --check`.
- T1 scenario readback: case/space variants normalize to one exact phrase; overlapping action matches block; incomplete or conflicting pagination preserves backlog and blocks sends; existing manual/native responses are checked; stale locks are not auto-broken; private/public intent records remain separate and durable before writes; unknown outcomes do not retry; interval updates preserve state; accepted/queued status does not prove delivery or permit a public receipt.
- Live read-only evidence for T3 (not a completion): authorized account identity checks matched, but known post metadata indicated comments while the documented comment scan returned no rows across all cursor pages without an API error. The app dashboard reports unpublished status. Treat readiness as blocked and the scan as inconsistent/incomplete; preserve pending state and watermark, and stop dependent sends. The cause of the empty scan is not established. No sends or app/access changes were made; first-reply buttons remain unverified.
- Next: T2 independent instruction exercise and T3 authorized controlled prerequisite/test review; do not activate a campaign from T1 artifacts.
