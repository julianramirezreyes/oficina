# Reusable Instagram response-automation policy

## Objective
Allow authorized Instagram community managers to edit existing organic comment/DM response automations on expressly authorized Instagram accounts or sessions without a separate configured authorization row, while keeping operational and platform-safety boundaries explicit.

## Problem and rationale
Current policy allows routine organic responses but treats automation edits as account-setting changes that require a configured authorization row. A narrowly scoped exception is needed so response automation can be maintained without opening broader account administration.

## Scope
- Update root office, customer-service department, and Instagram specialist policy documents coherently.
- Permit editing existing organic comment/DM response automations only on expressly authorized Instagram accounts/sessions.
- Preserve safeguards: one response per thread, inspect the complete context, verify the resulting configuration, no unsolicited/mass messaging, no unverified commercial claims, and stop on platform limits/notices.
- Explicitly exclude ads, spend, paid services, access/permissions, unrelated account settings, deletion, and bypassing platform limits.
- Keep the new policy generic and reusable; do not add personal names or specific account handles.

## Constraints
- Local policy documents only; the separate Meta rule change is out of scope.
- Preserve unrelated edits and pre-existing untracked `.codegraph/`, `.agents/`, and `.atl/` content.
- Stage only the task tracker and relevant policy files.
- Do not run native RDD review; parent orchestrator owns it.
- No executable behavior changes; strict TDD is not applicable. Record documentation consistency checks, not a test runner.
- No push or pull request.

## Authorized scope
- Repository: `oficina`
- Route: delegated direct; writer trigger applies because three non-trivial policy documents will be coordinated; preparation/read of source docs is part of this bounded write.
- Branch: `policy/instagram-response-automation`

## Checklist and acceptance criteria
- [x] Update root policy with a precise exception for editing existing organic Instagram comment/DM response automations.
- [x] Update customer-service department policy so its role/operation summary reflects the narrow exception.
- [x] Update Instagram specialist policy with actionable scope, verification, and safety conditions.
- [x] Confirm ads, spend, paid services, access/permissions, unrelated settings, deletion, and limit evasion remain excluded.
- [x] Confirm new policy wording is generic and contains no added personal names or specific handles.
- [x] Read back task tracker and Engram mirror.
- [x] Check policy consistency and run `git diff --check` before commit.
- [x] Commit only tracker and policy files using a Conventional Commit; verify with `git show --check --oneline HEAD`.

## Verification
- Documentation-only structural readback: inspect all changed policy sections for consistent scope and exclusions.
- `git diff --check`: run before commit.
- `git show --check --oneline HEAD`: run after commit.
- Test runner: N/A — no executable behavior changes.

## Progress
- [x] Confirmed clean tracked worktree on `main`; existing untracked support directories are preserved.
- [x] Created feature branch before edits.
- [x] Updated all three policy documents coherently.
- [x] Read back policy wording and confirmed the narrow scope/exclusions.
- [x] `git diff --check` passed before commit.
- [x] Committed the verified documentation work unit; commit message: `policy(instagram): allow scoped response automation edits` (verified at `HEAD`).

## Next step
No additional work remains. The final commit SHA is included in the delivery report.
