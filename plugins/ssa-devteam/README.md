# ssa-devteam

A Claude Code plugin that spawns an agent team for end-to-end feature development.

## What It Does

`/ssa-devteam` creates a full development team with a Project Manager orchestrating specialized teammates through five phases:

1. **Brainstorm** — PM explores requirements with you
2. **Architecture** — Architect designs the approved implementation approach
3. **Implementation** — Frontend + Backend developers build against the approved baseline
4. **Reviews and Remediation** — Architect, QA, and Security reviewers validate the work, then remediation loops continue until there are zero open findings
5. **Documentation** — Tech Writer documents what was built without bypassing the clean review gate

Each teammate is a separate Claude Code instance with its own context window. They coordinate through a shared task list and a persistent memory system.

## Team Roles

| Role | Agent | Phase |
|------|-------|-------|
| Project Manager | (the command itself) | All phases |
| Architect | `ssa-architect` | Design + Remediation Planning + Review |
| Frontend Dev | `ssa-frontend-dev` | Implementation + Remediation |
| Backend Dev | `ssa-backend-dev` | Implementation + Remediation |
| QA Reviewer | `ssa-qa-reviewer` | Review |
| Security Reviewer | `ssa-security-reviewer` | Review |
| Tech Writer | `ssa-tech-writer` | Documentation |

The PM dynamically activates implementation and review roles based on task scope, but the Architect is always involved in planning and remediation approval.

## Prerequisites

- Claude Code v2.1.32 or later
- Agent teams enabled:
  ```json
  // ~/.claude/settings.json
  {
    "env": {
      "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"
    }
  }
  ```

## Installation

```bash
# Add the marketplace and install
claude plugin marketplace add mderganc/ssa-devteam
claude plugin install ssa-devteam@ssa-devteam
```

## Usage

```text
/ssa-devteam Add user authentication with OAuth2 and session management
```

The PM will:
1. Ask clarifying questions about your requirements
2. Decide which team roles to activate
3. Require the Architect to publish the approved baseline before implementation starts
4. Run review and remediation loops until all active reviewers report zero open findings
5. Persist decisions, review findings, and remediation status to `.ssa-devteam/memory/`

## Review Model

- The Architect is always part of planning.
- Review findings use stable IDs and statuses.
- `WARN` is still tracked as an open finding by default.
- Phase 4 completes only when every active review file reports `Open findings: 0` and `Review status: CLEAN`.
- If documentation work edits source files after reviews are clean, Architect and QA review run again before completion.

## Memory System

The team maintains a persistent memory system at `.ssa-devteam/memory/` in your project root:

- **`project.md`** — Shared context, requirements, phase transitions, blocker notes, and the open findings tracker
- **`architect.md`** — Approved architecture baseline, remediation plans, and architecture reviews
- **`[role].md`** — Per-role implementation notes, review findings, remediation rounds, and documentation status

Memory persists across sessions. If you restart `/ssa-devteam` for the same feature, the PM reads existing memory, checks for open findings, and resumes from the earliest incomplete or still-open phase.

Memory is committed to git after each phase gate, preserving the development history.

## License

MIT
