---
name: luna-task
description: Delegate one clear, bounded, reliably verifiable implementation task to luna-max while the main agent owns the contract and review. Use only when the user explicitly invokes $luna-task. Choose a goal loop for multiple slices and Terra for judgment-heavy execution; keep unresolved product or architecture decisions in the main thread.
---

# Luna Task

Keep the main agent as planner and reviewer. Delegate one cohesive implementation
slice to `luna-max`, review the result, and accept it after proportionate
validation. Do not create, update, complete, or otherwise manage a goal.

## Confirm the task fits

1. Inspect the request, applicable repository instructions, current worktree,
   and enough authoritative context to define the execution boundary.
2. Use this workflow only when the outcome, architecture, invariants, and
   acceptance check are settled and one worker can own the complete change as
   one independently reviewable slice.
3. Luna is a good fit when execution is localized, repeatable, mechanical, or
   high-volume and the result has a clear, reliable acceptance check or is
   inexpensive to review and retry.
4. The main agent may perform bounded read-only planning to identify files,
   dependencies, risks, and the acceptance check. Keep all product,
   architecture, public-contract, destructive, and scope-expanding decisions
   in the main thread.
5. If a material product decision remains, resolve it with the user before
   delegation. If the work requires multiple implementation slices or sustained
   correction cycles, recommend `$luna-goal-loop`. If inspection instead exposes
   judgment-heavy, cross-boundary, weakly verified, or consequential execution,
   report the evidence and recommend `$worker-task` or `$terra-task`. Honor the
   explicit Luna choice and do not silently substitute another tier.

## Delegate one slice

1. Confirm that `luna-max` is available. If it is unavailable, report the
   limitation instead of silently substituting another worker.
2. Give the worker a compact, self-contained execution contract containing:

   - the objective and observable outcome;
   - owned files or responsibility boundary;
   - invariants and explicit non-goals;
   - authoritative files or context to inspect;
   - required implementation and focused validation; and
   - decisions or conditions that must return to the main agent.

3. Spawn exactly one `luna-max` worker for the slice. Do not split it into
   parallel microtasks.
4. While the worker runs, perform only independent read-only or review
   preparation. Do not duplicate its implementation.

## Review and accept

1. Wait for the worker's handoff, then inspect the actual diff and validation
   evidence. Check the acceptance contract, relevant integration behavior,
   failure paths, unrelated changes, and test gaps.
2. If corrections remain within the original bounded task, send one correction
   pass to the same worker and review the result. An ordinary defect or failed
   test is a correction, not evidence that Luna is the wrong tier.
3. If review exposes another substantive slice, repeated correction, or hidden
   Terra-suitable risk, stop and return the routing decision to the user rather
   than silently switching workers.
4. Run focused validation plus any repository-mandated gate. Run a broader
   suite only when the change, failure evidence, or repository instructions
   justify it.
5. Keep commits, pushes, roadmap updates, live deployment, and other external
   changes in the main thread and within the user's authorization.
6. Report the accepted outcome, worker contribution, changed files,
   validation, remaining risks, and repository state.
