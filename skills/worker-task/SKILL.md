---
name: worker-task
description: Route one bounded, execution-ready implementation task to luna-max or terra-xhigh using a cost-aware assessment of verification, rework, and consequence. Use only when the user explicitly invokes $worker-task. The main agent owns planning and review; choose a goal loop for multiple slices and keep unresolved decisions in the main thread.
---

# Worker Task

Keep the main agent as planner and reviewer. Select the appropriate worker tier,
delegate one cohesive implementation slice, and accept it after proportionate
validation. Do not create, update, complete, or otherwise manage a goal.

## Confirm the task fits

1. Inspect the request, applicable repository instructions, current worktree,
   and enough authoritative context to define the execution boundary.
2. Use this workflow only when the outcome, architecture, invariants, and
   acceptance check are settled and one worker can own the complete change as
   one independently reviewable slice.
3. Keep all product, architecture, public-contract, destructive, and
   scope-expanding decisions in the main thread. If one remains unresolved,
   resolve it with the user before delegation.
4. If the work requires multiple implementation slices or sustained correction
   cycles, recommend `$worker-goal-loop` instead. Do not silently broaden this
   workflow.

## Select the worker tier

Start with `luna-max`. Keep Luna when the contract is clear and execution is
localized, repeatable, mechanical, or high-volume, especially when the result
has a clear, reliable acceptance check or is inexpensive to review and retry.

Choose `terra-xhigh` only when its broader synthesis or judgment is likely to
reduce enough rework or consequence to justify its material cost premium. Good
signals include:

- interacting cross-module or cross-runtime behavior;
- broad or large-context investigation and synthesis;
- weak, manual, slow, or expensive verification, or costly failure;
- migrations or state transitions, concurrency, subtle debugging, security,
  or data-integrity risk; or
- evidence from a lower-tier pass that the task requires one of these qualities.

Do not choose Terra based only on unfamiliarity, file count, diff size, expected
duration, or volume. If the evidence is borderline, choose Luna. State the tier
and a brief concrete rationale in commentary without asking the user to choose
again.

Confirm that the selected custom agent is available. If it is unavailable,
disclose that limitation and use the other tier only when it independently fits
the task; otherwise stop instead of silently substituting it.

## Delegate one slice

Give the selected worker a compact, self-contained execution contract containing:

- the objective and observable outcome;
- owned files or responsibility boundary;
- invariants and explicit non-goals;
- authoritative files or context to inspect;
- required implementation and focused validation; and
- decisions or conditions that must return to the main agent.

Spawn one worker for the slice. Do not split it into parallel microtasks. While
it runs, perform only independent read-only or review preparation and do not
duplicate its implementation.

## Review and accept

1. Inspect the actual diff and validation evidence. Check the acceptance
   contract, relevant integration behavior, failure paths, unrelated changes,
   and test gaps.
2. Send one bounded correction pass to the same worker when the remaining work
   stays within the original contract.
3. If a Luna pass reveals hidden coupling, an ambiguous or expensive acceptance
   check, high consequence of failure, or another concrete Terra signal, the
   main agent may transfer the remaining original task to `terra-xhigh` once.
   Explain the evidence and do not escalate merely because an ordinary defect
   or test failure needs correction.
4. If review exposes another substantive slice or repeated correction is
   needed, stop treating the work as a task and recommend `$worker-goal-loop`.
5. Run focused validation plus any repository-mandated gate. Run a broader
   suite only when the change, failure evidence, or repository instructions
   justify it.
6. Keep commits, pushes, roadmap updates, live deployment, and other external
   changes in the main thread and within the user's authorization.
7. Report the accepted outcome, routing rationale, worker contribution,
   changed files, validation, remaining risks, and repository state.
