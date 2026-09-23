---
name: luna-task
description: Delegate one bounded investigation or implementation task to luna-max while the primary owns decisions and review. Use only when the user explicitly invokes $luna-task. Luna is the only delegated model; difficult portions return to the primary.
---

# Luna Task

Use `luna-max` for one cohesive task. Keep the current primary responsible for
decisions, integration, and acceptance; the intended setup is Sol XHigh. This
skill does not change the primary model or create or manage a goal.

## Define the assignment

Inspect the request, repository instructions, worktree, and enough authoritative
context to identify the outcome, ownership boundary, and practical acceptance
check. Delegate useful work without solving every implementation detail first.

When facts are missing, Luna can trace code, reproduce a failure, investigate a
bounded question, or propose options. Specify investigation or implementation
mode. An investigation does not authorize implementation edits.

Resolve ordinary technical decisions in the primary within the user's scope.
Ask the user only for a missing preference, product choice, or authorization
that materially affects the work. Start implementation once its behavior and
invariants are settled; coding steps need not be predetermined.

## Delegate

Confirm `luna-max` is available. If unavailable, report the limitation; do not
silently substitute another worker or claim delegation occurred.

Give one worker a compact, self-contained contract containing:

- the mode, objective, and observable outcome;
- owned files or responsibility, with unrelated changes to preserve;
- invariants, non-goals, and authoritative context to inspect;
- the acceptance check and proportionate validation; and
- unresolved decisions or conditions to return to the primary.

Use the named custom agent and minimum necessary context. Prefer
`fork_turns: "none"` when supported so the contract is self-contained. Honor the
client's role and model selection rules; a task label alone does not select Luna.
Prefer one cohesive assignment over parallel microtasks. Do not duplicate the
worker's implementation while it runs.

## Review and resolve difficulty

Inspect actual findings or diffs and validation evidence. Reuse the worker for
clarifications and bounded corrections. An ordinary failed test is usually a
correction, not a reason to change the plan.

Return an unresolved decision, verification gap, contradictory evidence, or
repeated failure without new evidence to the primary. Cross-module behavior,
migrations, concurrency, or file count alone do not disqualify Luna. The primary
may resolve the difficult portion and return a clearer assignment to Luna, or
finish the original task directly when another handoff adds no value. Explain
that takeover. Luna remains the only delegated model; do not introduce a Sol,
Terra, or Astra worker under this skill.

Before the primary edits worker-owned files, obtain the handoff or stop the
writer and inspect partial changes. Preserve useful work.

## Finish

Review integration behavior, failure paths, unrelated changes, and test gaps.
Resolve verification gaps before acceptance, including work done by the primary.
Run checks appropriate to the assignment and repository-required gates; broaden
checks only for an unresolved risk. Complete corrections within the original task without
silently expanding scope or creating a goal.

Keep commits, pushes, deployment, and other external actions within existing
authorization. Report the outcome, Luna's contribution, any primary takeover,
validation, remaining uncertainty, and repository state.
