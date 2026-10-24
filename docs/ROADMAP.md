# Agent Toolchain Canary — Roadmap

_Added October 23, 2026, following Tucker's request to move Canary work out of
the portfolio project._

## Ownership and current state

This repository and the Canary project brain own Canary planning, diagnostic
execution, product changes and independent review. The illustrated portfolio owns
storytelling, media acceptance and site integration. A Dashboarda view may consume
Canary output later, but the diagnostic/report contract stays here; do not couple
Canary's engine to portfolio code.

Current inspected main: `ed9703c7ead7c36ecf4b5554d56fa9cfc88501aa`.
The CLI and operating documentation exist. This planning pass did not execute probes,
verify current auth, install schedules or establish continuous uptime. No new
capability below is implemented or dispatched by this document.

## Sequence and slices

| Slice | Outcome | State |
| --- | --- | --- |
| CAN-01 | Public-safe CLI execution evidence for the portfolio | Next candidate for the Canary brain to assign |
| CAN-02 | Read-only status/history view contract and implementation | Parked; separately approved scope required |
| CAN-03 | Authenticated Check now executor | Parked; depends on an accepted execution/security boundary |
| CAN-04 | Owner-guided provider re-authentication | Parked; provider-specific design required |

CAN-01 is the portfolio media dependency. CAN-02–04 are product backlog items and
do not block portfolio publication.

### CAN-01 — CLI execution evidence export

**Goal:** Supply authentic terminal media and accurate execution context without
turning repository/documentation screenshots into claimed runtime proof.

**Scope:** Follow AGENTS.md, CONTRIBUTING.md and SECURITY.md. Use Node 20+ and the
existing bounded, read-only diagnostics in an authorized environment. Inspect existing
commands before choosing a run. Record actual success/failure/skipped/inconclusive
states; missing prerequisites remain explicit. A deliberately induced failure or
fixture must be labeled as a demonstration with its setup.

**Deliverable to the portfolio:** Reviewed, sanitized terminal images and a neutral
caption/alt-text manifest recording command, revision, date, environment class,
observed outcome and live-versus-fixture status. The portfolio may receive approved
public media; local reports, machine-specific paths, account identifiers, tokens,
local config/state and logs remain untracked in the Canary workspace. Do not add
raw or redacted local reports to this repository. Use a neutral authored summary
for provenance, and inspect exported image pixels before release.

**Done when:** At least one actual execution is documented; a separate temporary
reviewer checks the output and every exported image/caption; the portfolio receives
only approved media with an exact revision reference. Document outcomes that could
not be observed. Do not invent a passing result to complete the slice.

**Exclude:** Engine changes, new probes, schedule installation, credential changes,
status dashboard implementation, re-authentication or portfolio website edits.

### CAN-02 — Read-only status and history

**Goal:** Show last check, freshness, per-probe outcomes and observed history.

**Before dispatch:** The Canary brain must inspect the current report schema and
choose the smallest implementation: local report viewer or separately integrated
Dashboarda consumer. Name the owning repo(s), bounded files and acceptance criteria.
Define sanitized export, retention, failure/skip/inconclusive treatment and what
happens when reports are missing, late or checks have gaps.

**Acceptance boundary:** Status matches source observations; observed passing/failing
streaks and their longest recorded values do not imply continuous uptime. Gaps are
unknown. The view is read-only and exposes no credential or local-report details.

**Exclude:** Check now, silent reconnect, auth or schedule changes.

### CAN-03 — Check now

**Before dispatch:** Identify an authenticated executor in the actual environment
being diagnosed. Specify allowlisted commands, timeout, overlap control, result
redaction and who may trigger a check. Inspect the existing engine before adding
any runner. A hosted Dashboarda page alone cannot run a user's local CLI.

**Acceptance boundary:** An authorized request runs only the agreed diagnostic
contract; unauthorized requests fail; results distinguish completed, failed,
skipped and inconclusive work. No arbitrary command execution, deployment,
schedule installation or credential mutation.

### CAN-04 — Guided re-authentication

**Before dispatch:** Inspect the specific provider and credential host. Scope an
owner-only handoff to its supported secure login/refresh flow, followed by a
read-only recheck. Automatic refresh is an investigation, not a promised feature.

**Acceptance boundary:** No embedded credentials, secret collection, permission
widening or automatic rotation/provisioning. Preserve the repository's current
read-only probe and credential boundaries. Any required policy/architecture change
must be proposed explicitly before implementation.

## Temporary-agent workflow and return contract

The Canary brain fills the chosen contract with exact workspace, branch/base/head,
allowed changes, acceptance checks and exclusions. Assign one temporary
`d — CAN-xx`; commit meaningful work on `feat/*` before handing to a separate
`r — CAN-xx`. The reviewer inspects the actual commit and outputs independently.
Return precise rework when needed; optional enhancements do not block the contract.
Keep only one implementation slice active. Tucker accepts merge/publication.

For CAN-01, return the approved media and caption manifest to
[jtwray/portfolio-illustrated](https://github.com/jtwray/portfolio-illustrated),
portfolio slice ILL-06. That slice imports evidence; it does not direct Canary runs.
Later product work remains here even after the portfolio evidence is accepted.
