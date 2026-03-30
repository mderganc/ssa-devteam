# Memory Protocol

Defines conventions for the `.ssa-devteam/memory/` directory used by all agents.

## Memory Files

| File | Owner | Content |
|------|-------|---------|
| project.md | PM | Shared context: feature name, timestamps, dependency status, autonomy level/changes, task type, scope, team composition, open findings tracker, stage markers, completion summary |
| investigation.md | Architect | Five-why analysis per finding, root causes with evidence chains |
| solutions.md | Architect | Solution options per root cause, scoring, recommendations, cross-solution analysis |
| plan.md | Architect | Implementation plan, task breakdown, parallelization map, branch strategy |
| backend-dev.md | Backend Dev | Implementation notes, files changed, tests written, deviations, blockers |
| frontend-dev.md | Frontend Dev | Implementation notes, files changed, tests written, deviations, blockers |
| qa-reviewer.md | QA Reviewer | Test results, coverage analysis, findings per review round |
| security-reviewer.md | Security Reviewer | OWASP audit findings, vulnerability assessments per round |
| tech-writer.md | Tech Writer | Documentation decisions, files created, whether source files edited |
| critic.md | Critic | Challenges raised per stage, assumptions tested, findings |

## Beads ID Cross-References

Every finding, root cause, solution, and task in memory files MUST reference its beads issue ID:

### Finding: Session tokens stored in plaintext [bd-xxx.1]
### Root Cause: No encryption layer in token service [bd-xxx.2]
### Solution A: Add AES-256 encryption wrapper [bd-xxx.3]
### Task 1: Implement encryption wrapper [bd-xxx.T1]

If beads is unavailable, use sequential IDs with the same format:
### Finding: Session tokens stored in plaintext [F-001]
### Root Cause: No encryption layer [RC-001]

## Stage Markers

Each memory file records stage transitions:

## Stage N: IN_PROGRESS [2026-03-30 14:30]
[... stage content ...]
## Stage N: COMPLETE [2026-03-30 15:45]

## Append-Only Rule

Within a stage, memory files are append-only. New review rounds, remediation batches, and findings are appended as new sections — never overwrite previous rounds. This preserves the full audit trail.

## Reading Convention

Agents read memory files in this order:
1. project.md first (shared context, current state)
2. Upstream stage files (e.g., implementation agents read plan.md before starting)
3. Peer memory files when needed for cross-review

## Writing Convention

Agents write ONLY to their own memory file. The PM is the only role that writes to project.md. If an agent needs to communicate something to another agent, it writes to its own file and the PM relays or the other agent reads it.
