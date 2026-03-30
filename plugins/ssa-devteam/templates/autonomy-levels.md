# Autonomy Levels

Three tiers of user interaction during the SSA Dev Team workflow.

## Level Definitions

### Level 1 — Full Approval (Default)
Pause at every stage gate for user approval. Maximum user control.

Best for: First time using the plugin, high-stakes work, learning the workflow.

### Level 2 — Key Decisions Only
Pause at Stage 3 (solution approval), Stage 4 (pre-implementation), and Stage 7 (merge decision). Auto-proceed through investigation, solution generation, implementation waves, and review loops.

Best for: Experienced users who trust the investigation/review process but want control over what gets built and how it ships.

### Level 3 — Full Auto
Auto-proceed through all stages. Only pause at Stage 7 for the merge decision. PM auto-selects recommended solutions when the user doesn't intervene.

Best for: Well-understood tasks, trusted codebase, time-sensitive work.

## Gate Behavior Matrix

| Stage | Level 1 | Level 2 | Level 3 |
|-------|---------|---------|---------|
| 1 - Investigation | Pause, present summary | Auto-proceed | Auto-proceed |
| 2 - Solutions | Pause, present summary | Auto-proceed | Auto-proceed, auto-select recommended |
| 3 - Approval | Pause (always) | Pause (always) | Auto-select recommended, log summary |
| 4 - Planning | Pause, present plan | Pause, present plan | Auto-proceed |
| 5 - Implementation | Pause between waves | Auto-proceed, summary after all waves | Auto-proceed |
| 6 - Review | Pause, present summary | Present summary, auto-proceed | Auto-proceed |
| 7 - Documentation & Merge | Pause for merge decision | Pause for merge decision | Pause for merge decision |

## Selection

At startup, the PM presents:

How much autonomy should the team have?

  Level 1 (Default): Pause at every stage gate for your approval
  Level 2: Only pause at solution approval (Stage 3),
           before implementation (Stage 4), and merge (Stage 7)
  Level 3: Full auto — report at end, pause only for merge

  Enter 1, 2, or 3 (or pass --auto1/--auto2/--auto3 next time):

## Keyword Detection

If the user's prompt contains autonomy-related keywords, suggest the appropriate level:
- "autonomous", "go ahead", "don't wait", "continue without me", "full auto" → Suggest Level 3
- "check with me", "I want to approve", "pause for me" → Suggest Level 1
- Default (no keywords): Level 1

Always confirm the suggestion — never auto-set based on keywords alone.

## Mid-Session Changes

The user can change autonomy at any time:
- "switch to level 2" / "go autonomous" / "pause for approvals" / "level 3"
- PM acknowledges, updates project.md, applies immediately to the next gate

Changes are logged in project.md:

## Autonomy
**Current level:** 2
### Changes
- [2026-03-30 14:00] Set to Level 1 (initial)
- [2026-03-30 14:35] Changed to Level 2 (user: "skip minor gates")

Reminder shown after every change:
Autonomy set to Level [N]. Change anytime: 'switch to level 1/2/3'
or 'go autonomous' / 'pause for approvals'.
