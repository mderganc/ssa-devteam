# SSA Dev Team — Memory System

This directory contains the shared memory files for an SSA Dev Team session.

## Files

| File | Owner | Purpose |
|------|-------|---------|
| `project.md` | PM | Shared context, stage markers, autonomy log, findings tracker, completion summary |
| `investigation.md` | Architect | Five-why analysis, findings, root causes with evidence |
| `solutions.md` | Architect | Solution options per root cause, scoring, recommendations |
| `plan.md` | Architect | Implementation plan, tasks, parallelization, branches |
| `backend-dev.md` | Backend Dev | Implementation notes, files changed, tests, deviations |
| `frontend-dev.md` | Frontend Dev | Implementation notes, files changed, tests, deviations |
| `qa-reviewer.md` | QA Reviewer | Test results, coverage, findings per review round |
| `security-reviewer.md` | Security Reviewer | OWASP audit findings, vulnerability assessments |
| `tech-writer.md` | Tech Writer | Documentation decisions, files created/modified |
| `critic.md` | Critic | Challenges raised per stage, assumptions tested |

## Conventions

- **Beads cross-references:** Every finding, root cause, solution, and task references its beads ID: `### Title [bd-xxx.N]`
- **Stage markers:** `## Stage N: IN_PROGRESS [timestamp]` / `## Stage N: COMPLETE [timestamp]`
- **Append-only:** Within a stage, append new sections — never overwrite previous rounds.
- **Ownership:** Agents write only to their own file. PM writes only to `project.md`.

## Resume

If the team is restarted:
1. PM reads all files, checks stage markers
2. Finds earliest incomplete stage
3. Reports state and resumes

See `templates/memory-protocol.md` for full conventions.
