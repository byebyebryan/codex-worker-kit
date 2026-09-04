---
name: luna-goal-loop
description: Run a cost-efficient architect-worker loop with luna-max for a substantial goal whose slices are clear and reliably verifiable. Use when the user invokes $luna-goal-loop or asks for a goal or checkpoint loop with Luna or luna-max. The main agent assesses readiness and owns product and architecture decisions; use Terra for judgment-heavy execution.
---

# Luna Goal Loop

Keep the main agent as architect and reviewer. Assess readiness and plan as
needed before using `luna-max` for clear, independently verifiable implementation
slices. Luna is the selected execution tier, not additional product or
architecture authority.

Subagents have fixed context and coordination cost. Do not use this loop
implicitly for a trivial change; honor an explicit user invocation.

## Assess execution readiness

1. Resolve the requested outcome, applicable repository instructions, current
   worktree state, design authority, and required exit gate.
2. Classify the request before creating a goal or starting a writer:

   - **Ready**: the desired outcome, architecture and invariants, and exit gate
     are settled well enough to package an execution slice. Individual coding
     steps do not need to be predetermined.
   - **Needs implementation planning**: the product contract is settled, but
     relevant code paths, dependencies, risks, or slice boundaries are not yet
     clear.
   - **Needs product decision**: desired behavior, architecture, scope, or an
     invariant remains unresolved and materially changes the implementation.

3. For **Needs implementation planning**, keep synthesis and decisions in the
   main thread. Inspect the repository and form an execution contract. A
   bounded read-only evidence-gathering assignment may be delegated to
   `luna-max`, after confirming it is available, when the assignment is narrow,
   well-defined, and materially reduces main-agent exploration without requiring
   an architecture or product decision. Do not start a writer. Reclassify after
   planning.
4. For **Needs product decision**, explain the unresolved choice and continue
   the discussion with the user. Do not create an execution goal or spawn
   `luna-max`.
5. Proceed only when the request is **Ready**.

## Establish the execution goal

1. Confirm that the `luna-max` custom agent is available if it was not already
   used for evidence gathering. If it is unavailable, stop and report that
   limitation instead of silently substituting a more expensive worker.
2. When goal tools are available, create the explicitly requested goal or
   continue it when the active goal matches. Report a conflicting active goal
   instead of replacing it. Do not invent a token budget.

## Package an execution slice

Choose the largest cohesive slice that one worker can implement, test, and
self-review without making a new architecture or product decision. Bound the
slice by decision authority and independently reviewable behavior, not by a
small line or file count. Prefer slices with a clear, reliable acceptance check
or an inexpensive review-and-retry cycle.

Give the worker a self-contained execution contract with:

- objective and observable outcome;
- owned files or responsibility boundary;
- invariants and behavior that must remain unchanged;
- explicit non-goals;
- authoritative context and files to inspect;
- required implementation and focused validation;
- decisions or conditions that must return to the main agent; and
- a concise handoff containing outcome, changed files, validation, and risks.

Point to authoritative repository material instead of reproducing long
conversation history. Pass only the minimum recent thread context needed by
the client.

## Delegate and supervise

1. Use one `luna-max` writer by default. Do not create several microtasks where
   one coherent assignment would work.
2. While the worker runs, perform only independent architectural or read-only
   work. Do not duplicate its implementation.
3. Reuse the same worker for clarifications and correction passes when
   practical so it retains task-local context.
4. At a meaningful slice boundary, inspect the actual diff and focused test
   evidence. Review design invariants, integration behavior, failure paths,
   unrelated changes, and test gaps.
5. Package substantive corrections for the same worker. Resolve architecture
   or scope decisions in the main thread before delegating the resulting
   bounded change.
6. If a slice reveals judgment-heavy, cross-boundary, weakly verified, or
   consequential execution, pause, report the evidence, and recommend
   `$worker-goal-loop` or `$terra-goal-loop`. Do not silently switch tiers
   inside an explicitly Luna-selected loop.
7. Start another implementation slice only when required by the goal. Keep
   write ownership non-overlapping if true parallel work is necessary.

## Close the loop

1. Perform one overall contract-focused review after the implementation slices
   are integrated.
2. Delegate resulting implementation fixes to `luna-max`, then review the
   resulting diff. Avoid repeated full-suite runs during intermediate slices.
3. Run the repository's complete required gate once the candidate is final.
4. Keep roadmap status, architecture evidence, and commit or push decisions in
   the main thread unless the user explicitly delegates them.
5. Mark the goal complete only when the requested outcome and exit gate are
   satisfied with no required work remaining. Otherwise follow the goal
   mechanism's blocking rules and report the concrete limitation.
6. Report the final outcome, the worker's contribution, validation, remaining
   risks, and repository state.
