# Stage 2 — Solution Generation & Evaluation

## Purpose
Generate 2-4 meaningfully distinct solution options per root cause, score each on 6 dimensions, and recommend a preferred approach — with cons/risks explicit for every option.

## Lead Agent
**Architect** — generates and scores solutions

## Superpowers Integration
- Invoke `superpowers:brainstorming` if available to explore solution space

## PM Actions

### 1. Assign Solution Generation

Send to Architect:

> **Task: Generate solutions for [N] root causes**
>
> Read `.ssa-devteam/memory/investigation.md` for confirmed root causes.
>
> For each root cause:
> 1. Generate 2-4 meaningfully distinct solutions (not variations of the same approach)
> 2. Score each using `templates/scoring-rubric.md` — justify every score
> 3. List specific cons/risks for every option
> 4. Check for cross-solution conflicts and compound solutions
> 5. Recommend one solution per root cause with rationale
>
> Write to `.ssa-devteam/memory/solutions.md`.
> Create beads issues for each solution option (if beads available).
> Mark recommended solutions with `recommended` label.

### 2. Task Type Framing

| Task Type | Solution Framing |
|-----------|-----------------|
| Bugfix | "Here are N ways to fix root cause X" |
| Refactor | "Here are N approaches to restructure around root cause X" |
| Feature | "Here are N architectural approaches to address core challenge X" |

### 3. Run Review Loop

Per `templates/review-loop.md`:

| Step | Agent | Focus |
|------|-------|-------|
| Self-review | Architect | Each option genuinely distinct? Cons honest? Scores defensible? Compound solutions considered? |
| Cross-review | Security (if activated), QA | New attack surface? Risk scores accurate? Solutions testable? Effort realistic? |
| Critic challenge | Critic | Worst case for recommended? Cons understated? When would non-recommended be better? |
| PM validation | PM | Every root cause has ≥2 options? Scores consistent? Cons specific enough for user? |

Loop until all pass cleanly in the same round.

### 4. Beads Tracking

For each solution option:
bd create "[solution description]" -t task --parent [epic-id] -l "solution,stage-2,option"
bd dep add [solution-id] [root-cause-id] --type blocks
bd comments add [solution-id] "Scores: Q=N T=N C=N R=N E=N P=N"

Mark recommended: bd label add [solution-id] recommended

### 5. Stage Gate

| Autonomy | Behavior |
|----------|----------|
| Level 1 | Present solution summary to user, proceed to Stage 3 |
| Level 2 | Auto-proceed to Stage 3 (always pauses there) |
| Level 3 | PM auto-selects recommended, logs rationale, skips Stage 3 |

### 6. Git Checkpoint

git add .ssa-devteam/ && git commit -m "ssa-devteam: Stage 2 complete — solutions evaluated"

Record in project.md: `## Stage 2: COMPLETE [timestamp]`
