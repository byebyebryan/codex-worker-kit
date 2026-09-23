---
name: worker-goal-loop
description: Run a substantial goal with Luna by default, primary-agent handling of difficult portions, and optional Sol workers when separate context helps. Use only when the user explicitly invokes $worker-goal-loop. The primary owns decisions, routing, and acceptance.
---

# Worker Goal Loop

Keep the current primary responsible for decisions, integration, and acceptance;
the intended setup is Sol XHigh with Luna Max workers. Route each assignment
independently. This skill does not change the primary model.

## Establish readiness and the goal

Inspect the requested outcome, repository instructions, worktree, authoritative
design, invariants, and exit gate. Resolve ordinary technical decisions in the
primary within the user's scope. Ask the user only for a missing preference,
product choice, or authorization that materially affects the work.

When facts are missing, use bounded investigation to trace code, reproduce a
failure, or propose options. Specify the question and evidence needed; an
investigation does not authorize implementation edits. Start an implementation
writer only when the slice's intended behavior and invariants are settled.
Individual coding steps need not be predetermined.

When execution is ready and goal tools are available, create the explicitly
requested goal or continue a matching active goal. Report a conflicting active
goal instead of replacing it. Do not invent a token budget.

## Route each assignment

Choose the route with the lowest expected total cost of reaching an accepted
result, including primary context, handoffs, review, and retries:

- **Luna by default:** use `luna-max` for bounded investigation or implementation
  with a clear outcome and practical verification. Delegate useful work without
  solving every detail first.
- **Primary directly:** keep architecture decisions and deeply coupled reasoning
  in the primary. Resolve or implement difficult portions there when it already
  has the relevant context, then return settled work to Luna when useful.
  Finish small remainders directly when another handoff would add overhead.
- **Optional Sol worker:** use `sol-xhigh` for complex, self-contained work when
  separate context or independent parallel work has a concrete benefit. State
  that benefit; complexity alone does not require another Sol agent.

Migrations, concurrency, security, cross-module behavior, file count, or
unfamiliarity alone do not rule out Luna. Use evidence of an unresolved decision,
missing verification, or unsuccessful approach to assess the actual difficulty.
Do not route automatically to Terra or Astra, and do not require a failed Luna
attempt before selecting the primary for work already known to need it.

Confirm a selected custom agent is available. If unavailable, disclose it and
continue in the primary; do not silently choose a different paid worker. State
the route and a brief rationale without asking the user to route the work.

## Package and delegate

Choose the largest cohesive assignment that one worker can complete within its
decision boundary and that can be independently reviewed. Give it a compact,
self-contained contract containing:

- investigation or implementation mode, objective, and observable outcome;
- owned files or responsibility, with unrelated changes to preserve;
- invariants, non-goals, and authoritative context to inspect;
- the acceptance check and proportionate validation; and
- unresolved decisions or conditions to return to the primary.

Use the named custom agent and minimum necessary context. Prefer
`fork_turns: "none"` when supported. Honor the client's role and model selection
rules; a task label alone does not select a model. Use one writer by default and
reuse it for related corrections. Do not duplicate its implementation. Use parallel
assignments only when independent responsibilities justify their overhead.

## Review and recover

At meaningful boundaries, inspect actual findings or diffs and focused
validation. Review invariants, integration behavior, failure paths, unrelated
changes, and test gaps. Send ordinary defects back as bounded corrections.

If the same failure repeats without new evidence, or a decision or verification
gap emerges, have the primary diagnose or take over the difficult portion.
Before changing write ownership, obtain the handoff or stop the writer and
inspect partial changes. Preserve useful work. A subsequent Sol assignment
still requires a benefit from separate context or independent work; avoid
cycling between workers. Return clear remaining work to Luna when useful.

Route the next slice independently so a primary or Sol assignment does not
displace Luna from later suitable work. Continue the authorized goal without
pausing merely to ask the user to choose another workflow.

## Close the loop

Perform an overall contract review after integration. Complete remaining fixes
and resolve verification gaps, including in work done by the primary. Run the
repository's required final gate. Avoid repeated full-suite runs
unless a change or unresolved risk justifies them. Keep commits, pushes,
deployment, and roadmap changes within existing authorization.

Mark the goal complete only when the outcome and exit gate are satisfied with
no required work remaining. Otherwise follow the goal tool's blocking rules;
do not mark an active goal paused without a user request. Report the outcome,
routing rationale, worker and primary contributions, validation, remaining
uncertainty, and repository state. Include total usage or cost only when the
runtime provides it.
