# SSA Dev Team — Memory System

This directory contains the development history and decisions for a feature built by the SSA Dev Team agent team.

## Files

| File | Owner | Contents |
|------|-------|----------|
| `project.md` | PM | Shared context: requirements, scope, phase transitions, blocker notes, and the open findings tracker |
| `architect.md` | Architect | Approved architecture baseline, remediation plans, and architecture review findings |
| `frontend-dev.md` | Frontend Dev | Frontend implementation notes, remediation rounds, integration points, and test coverage |
| `backend-dev.md` | Backend Dev | Backend implementation notes, remediation rounds, API contracts, migrations, and test coverage |
| `qa-reviewer.md` | QA Reviewer | Test results, coverage gaps, edge cases, regression findings, and review summaries |
| `security-reviewer.md` | Security Reviewer | OWASP audit findings, vulnerability assessments, dependency audit, and review summaries |
| `tech-writer.md` | Tech Writer | Documentation decisions, files created, style notes, and whether source files changed |

## Phase Status Markers

Each memory file uses phase status markers to track progress:

```markdown
## Phase N: IN_PROGRESS [2026-03-24 14:30]
## Phase N: COMPLETE [2026-03-24 15:45]
```

- **IN_PROGRESS** — work is underway for this phase
- **COMPLETE** — phase gate passed, work is done

Developer remediation work should also record remediation rounds:

```markdown
## Remediation Round 1: IN_PROGRESS [2026-03-24 16:00]
## Remediation Round 1: COMPLETE [2026-03-24 16:25]
```

## Decision Entry Format

Role memory files record decisions in this format:

```markdown
## Decision: [title]
**Rationale:** Why this choice was made
**Context:** What constraints or information informed the decision
**Alternatives considered:** What was rejected and why
```

## Open Findings Tracker

`project.md` should maintain a tracker like this whenever any review opens findings:

```markdown
## Open Findings Tracker

| ID | Source | Severity | Status | Owner | Reviewer | Remediation Plan | Notes |
|----|--------|----------|--------|-------|----------|------------------|-------|
| QA-001 | QA | FAIL | OPEN | frontend-dev | qa-reviewer | RP-001 | Missing loading-state test |
```

Every non-pass finding should appear in the tracker until the responsible reviewer verifies it as resolved.

## Review Findings Format

Reviewer memory files record findings in this format:

```markdown
### [PASS|WARN|FAIL]: [title]
**ID:** [QA-001 | SEC-001 | ARCH-001]
**Status:** [OPEN | RESOLVED]
**Location:** [file:line or component]
**Description:** What was found
**Impact/Risk:** What could go wrong
**Evidence:** [optional, except required for security FAIL]
**Fix:** How to fix
```

`WARN` is still an open finding by default. Only `PASS` is non-blocking.

## Review Summary Format

Every review file must end each review round with:

```markdown
## Review Summary
**Open findings:** 0
**Resolved findings verified:** 3
**Review status:** CLEAN
```

Allowed review statuses:
- `CLEAN`
- `REQUIRES_FIXES`

Phase 4 is not complete until every active review file reports `Open findings: 0` and `Review status: CLEAN`.

## Cross-Session Resume

If the team is restarted for the same feature:
1. PM reads all memory files
2. Checks for the earliest phase with `IN_PROGRESS`, no marker, or open findings
3. Resumes from that phase
4. Reports state to user before continuing

## Git Persistence

The PM commits memory files after each phase gate:

```text
ssa-devteam: Phase N complete — [brief summary]
```

This preserves the development history in the project's git log.
