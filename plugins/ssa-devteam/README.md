# ssa-devteam

A Claude Code plugin that spawns an agent team for end-to-end feature development.

## What It Does

`/ssa-devteam` creates a full development team with a Project Manager orchestrating specialized teammates through five phases:

1. **Brainstorm** — PM explores requirements with you
2. **Architecture** — Architect designs the implementation approach
3. **Implementation** — Frontend + Backend developers build in parallel
4. **Reviews** — Architect, QA, and Security reviewers validate the work
5. **Documentation** — Tech Writer documents what was built

Each teammate is a separate Claude Code instance with its own context window. They coordinate through a shared task list and a persistent memory system.

## Team Roles

| Role | Agent | Phase |
|------|-------|-------|
| Project Manager | (the command itself) | All phases |
| Architect | `ssa-architect` | Design + Review |
| Frontend Dev | `ssa-frontend-dev` | Implementation |
| Backend Dev | `ssa-backend-dev` | Implementation |
| QA Reviewer | `ssa-qa-reviewer` | Review |
| Security Reviewer | `ssa-security-reviewer` | Review |
| Tech Writer | `ssa-tech-writer` | Documentation |

The PM dynamically activates roles based on task scope — a frontend-only bugfix won't spawn a backend dev or security reviewer.

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

```
/ssa-devteam Add user authentication with OAuth2 and session management
```

The PM will:
1. Ask clarifying questions about your requirements
2. Decide which team roles to activate
3. Spawn the team and manage the full lifecycle
4. Persist decisions and progress to `.ssa-devteam/memory/`

## Memory System

The team maintains a persistent memory system at `.ssa-devteam/memory/` in your project root:

- **`project.md`** — Shared context, requirements, phase transitions
- **`[role].md`** — Per-role decisions, findings, implementation notes

Memory persists across sessions. If you restart `/ssa-devteam` for the same feature, the PM reads existing memory and resumes from where it left off.

Memory is committed to git after each phase gate, preserving the development history.

## License

MIT
