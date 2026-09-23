---
name: worker-task
description: Complete one bounded investigation or implementation task with Luna by default, primary-agent handling of difficult portions, and an optional Sol worker when separate context helps. Use only when the user explicitly invokes $worker-task. The primary owns decisions and review; no goal management.
---

# Worker Task

Keep the current primary responsible for decisions, integration, and acceptance;
the intended setup is Sol XHigh with Luna Max workers. This skill does not change
the primary model or create or manage a goal.

## Define and route the task

Inspect the request, repository instructions, worktree, and enough authoritative
context to define the outcome, ownership boundary, and acceptance check. Resolve
ordinary technical decisions within the user's scope. Ask the user only for a
missing preference, product choice, or authorization that materially affects
the work. Start implementation once intended behavior and invariants are settled;
individual coding steps need not be predetermined.

Choose the route with the lowest expected total cost of reaching an accepted
result, including primary context, handoffs, review, and retries:

- **Luna by default:** use `luna-max` for a bounded assignment with a clear
  outcome and practical verification. When facts are missing, delegate tracing,
  reproduction, a focused investigation, or proposed options before editing.
- **Primary directly:** keep architecture decisions and deeply coupled reasoning
  in the primary. Handle a difficult portion there when it already has the
  necessary context; return settled implementation to Luna when useful. A small
  remainder may be cheaper to finish directly than to hand off again.
- **Optional Sol worker:** use `sol-xhigh` for complex, self-contained work only
  when separate context or independent parallel work has a concrete benefit.
  Complexity alone does not require another Sol agent. State that benefit.

Migrations, concurrency, security, cross-module behavior, file count, or
unfamiliarity alone do not rule out Luna. Use evidence of an unresolved decision,
missing verification, or unsuccessful approach to assess the actual difficulty.
Do not route automatically to Terra or Astra.

Confirm a selected custom agent is available. If unavailable, disclose it and
continue in the primary; do not silently select a different paid worker. State
the chosen route and a brief rationale without asking the user to route it.

## Delegate when useful

Give the selected worker a compact, self-contained contract containing:

- investigation or implementation mode, objective, and observable outcome;
- owned files or responsibility, with unrelated changes to preserve;
- invariants, non-goals, and authoritative context to inspect;
- the acceptance check and proportionate validation; and
- unresolved decisions or conditions to return to the primary.

An investigation does not authorize implementation edits. Use the named custom
agent with minimum necessary context; prefer `fork_turns: "none"` when supported.
Honor the client's role and model selection rules rather than relying on a task
label. Prefer one cohesive assignment over parallel microtasks. Do not duplicate
the worker's implementation while it runs.

## Review and recover

Inspect actual findings or diffs and validation evidence. Reuse the worker for
clarifications and bounded corrections. An ordinary failed test is usually a
correction. If the same failure repeats without new evidence, or a decision or
verification gap emerges, have the primary diagnose or take over the difficult
portion. Do not require an unsuccessful Luna attempt before choosing the primary
for work already known to need it.

Before changing write ownership, obtain the handoff or stop the current writer
and inspect partial changes. Preserve useful work. A subsequent Sol assignment
still requires a concrete benefit from separate context or independent work;
avoid cycling between workers. Return clear remaining work to Luna when useful.

## Finish

Review integration behavior, failure paths, unrelated changes, and test gaps.
Resolve verification gaps before acceptance, including work done by the primary.
Run checks appropriate to the assignment and repository-required gates; broaden
checks only for an unresolved risk. Complete corrections within the original task without
silently expanding scope or creating a goal.

Keep commits, pushes, deployment, and other external actions within existing
authorization. Report the outcome, routing rationale, worker and primary
contributions, validation, remaining uncertainty, and repository state.
