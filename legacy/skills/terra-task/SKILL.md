---
name: terra-task
description: Deprecated GPT-5.6 Terra compatibility workflow. Use only when the user explicitly invokes $terra-task or explicitly requests this legacy Terra workflow. New work should use the Luna or adaptive worker workflows.
---

# Terra Task

Deprecated and excluded from the default installation. This compatibility
workflow still selects `terra-xhigh` on GPT-5.6 Terra; it never aliases Sol.
Use the Luna or adaptive worker workflows for new work.

Keep the main agent as planner and reviewer. Delegate one cohesive, judgment-heavy
implementation slice to `terra-xhigh`, review the result, and accept it after
proportionate validation. Do not create, update, complete, or otherwise manage
a goal.

## Confirm the task fits

1. Inspect the request, applicable repository instructions, current worktree,
   and enough authoritative context to define the execution boundary.
2. Use this workflow only when the outcome, architecture, invariants, and
   acceptance check are settled and one worker can own the complete change as
   one independently reviewable slice.
3. Terra is appropriate when its broader synthesis or judgment can materially
   reduce rework or consequence: interacting cross-module or cross-runtime
   behavior, large-context investigation, weak or expensive verification,
   costly failure, migrations or state transitions, concurrency, subtle
   debugging, security, or data-integrity risk. Unfamiliarity, file count,
   duration, or volume alone are not reasons to select Terra.
4. Honor the user's explicit Terra selection and do not silently substitute
   Luna. These criteria explain the tier; they do not override the user's choice.
5. The main agent may perform bounded read-only planning to identify files,
   dependencies, risks, and the acceptance check. Keep all product,
   architecture, public-contract, destructive, and scope-expanding decisions
   in the main thread.
6. If a material product decision remains, resolve it with the user before
   delegation. If the work requires multiple implementation slices or sustained
   correction cycles, recommend `$terra-goal-loop` instead. Do not silently
   broaden this workflow.

## Delegate one slice

1. Confirm that `terra-xhigh` is available. If it is unavailable, report the
   limitation instead of silently substituting another worker.
2. Give the worker a compact, self-contained execution contract containing:

   - the objective and observable outcome;
   - owned files or responsibility boundary;
   - invariants and explicit non-goals;
   - authoritative files or context to inspect;
   - required implementation and focused validation; and
   - decisions or conditions that must return to the main agent.

3. Spawn exactly one `terra-xhigh` worker for the slice. Do not split it into
   parallel microtasks.
4. While the worker runs, perform only independent read-only or review
   preparation. Do not duplicate its implementation.

## Review and accept

1. Wait for the worker's handoff, then inspect the actual diff and validation
   evidence. Check the acceptance contract, relevant integration behavior,
   failure paths, unrelated changes, and test gaps.
2. If corrections remain within the original bounded task, send one correction
   pass to the same worker and review the result. If review exposes another
   substantive slice or repeated correction is needed, stop treating the work
   as a task and recommend `$terra-goal-loop`.
3. Run focused validation plus any repository-mandated gate. Run a broader
   suite only when the change, failure evidence, or repository instructions
   justify it.
4. Keep commits, pushes, roadmap updates, live deployment, and other external
   changes in the main thread and within the user's authorization.
5. Report the accepted outcome, worker contribution, changed files,
   validation, remaining risks, and repository state.
