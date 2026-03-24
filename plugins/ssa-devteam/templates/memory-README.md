# SSA Dev Team — Memory System

This directory contains the development history and decisions for a feature built by the SSA Dev Team agent team.

## Files

| File | Owner | Contents |
|------|-------|----------|
| `project.md` | PM | Shared context: requirements, scope, phase transitions, completion summary |
| `architect.md` | Architect | Architecture design, component specs, and architecture review findings |
| `frontend-dev.md` | Frontend Dev | Frontend implementation notes, patterns, test coverage |
| `backend-dev.md` | Backend Dev | Backend implementation notes, API contracts, migrations |
| `qa-reviewer.md` | QA Reviewer | Test results, coverage gaps, edge cases, regression findings |
| `security-reviewer.md` | Security Reviewer | OWASP audit findings, vulnerability assessments, dependency audit |
| `tech-writer.md` | Tech Writer | Documentation decisions, files created, style notes |

## Phase Status Markers

Each memory file uses phase status markers to track progress:

```markdown
## Phase N: IN_PROGRESS [2026-03-24 14:30]
## Phase N: COMPLETE [2026-03-24 15:45]
```

- **IN_PROGRESS** — work is underway for this phase
- **COMPLETE** — phase gate passed, work is done

## Decision Entry Format

Role memory files record decisions in this format:

```markdown
## Decision: [title]
**Rationale:** Why this choice was made
**Context:** What constraints or information informed the decision
**Alternatives considered:** What was rejected and why
```

## Review Findings Format

Reviewer memory files record findings:

```markdown
### [PASS|WARN|FAIL]: [title]
**Location:** [file:line or component]
**Description:** What was found
**Impact:** What could go wrong
**Fix:** How to fix (for WARN and FAIL)
```

## Cross-Session Resume

If the team is restarted for the same feature:
1. PM reads all memory files
2. Checks for the earliest phase with `IN_PROGRESS` or no marker
3. Resumes from that phase
4. Reports state to user before continuing

## Git Persistence

The PM commits memory files after each phase gate:
```
ssa-devteam: Phase N complete — [brief summary]
```

This preserves the development history in the project's git log.
