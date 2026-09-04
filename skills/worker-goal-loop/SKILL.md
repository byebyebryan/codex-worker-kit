---
name: worker-goal-loop
description: Run a cost-aware architect-worker loop for a substantial implementation goal, selecting luna-max or terra-xhigh per slice according to verification, rework, and consequence. Use only when the user explicitly invokes $worker-goal-loop. The main agent assesses readiness and owns product and architecture decisions.
---

# Worker Goal Loop

Keep the main agent as architect and reviewer. Assess readiness and plan as
needed, then select `luna-max` or `terra-xhigh` independently for each cohesive
implementation slice. A worker tier changes execution depth, not product or
architecture authority.

Subagents have fixed context and coordination cost. Honor an explicit user
invocation, but do not create a goal or start a writer until the request is
execution-ready.

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
   bounded read-only evidence-gathering assignment may be delegated when it
   materially reduces exploration and requires no architecture or product
   decision; select its tier using the criteria below. Do not start a writer.
   Reclassify after planning.
4. For **Needs product decision**, explain the unresolved choice and continue
   the discussion with the user. Do not create an execution goal or spawn an
   implementation worker.
5. Proceed only when the request is **Ready**.

## Establish the execution goal

When goal tools are available, create the explicitly requested goal or continue
it when the active goal matches. Report a conflicting active goal instead of
replacing it. Do not invent a token budget.

## Route each execution slice

Select a tier separately for every slice instead of locking the entire goal to
one worker. Start with `luna-max`. Keep Luna for clear, localized, repeatable,
mechanical, or high-volume execution, especially with a clear, reliable
acceptance check or inexpensive review and retry.

Choose `terra-xhigh` only when its broader synthesis or judgment is likely to
reduce enough rework or consequence to justify its material cost premium. Good
signals include interacting cross-module or cross-runtime behavior; broad or
large-context synthesis; weak, manual, slow, or expensive verification; costly
failure; migrations or state transitions; concurrency; subtle debugging;
security or data-integrity risk; or lower-tier evidence exposing one of those
conditions.

Do not choose Terra based only on unfamiliarity, file count, diff size, duration,
or volume. If the evidence is borderline, choose Luna. State the tier and a
brief concrete rationale in commentary without asking the user to choose again.

Confirm the selected custom agent is available before delegation. If it is
unavailable, disclose that limitation and use the other tier only when it
independently fits the slice; otherwise report the blocker instead of silently
substituting it.

## Package and delegate a slice

Choose the largest cohesive slice that one worker can implement, test, and
self-review without making a new architecture or product decision. Bound the
slice by decision authority and independently reviewable behavior, not by a
small line or file count.

Give the selected worker a self-contained execution contract with:

- objective and observable outcome;
- owned files or responsibility boundary;
- invariants and behavior that must remain unchanged;
- explicit non-goals;
- authoritative context and files to inspect;
- required implementation and focused validation;
- decisions or conditions that must return to the main agent; and
- a concise handoff containing outcome, changed files, validation, and risks.

Use one writer per slice by default. While it runs, perform only independent
architectural or read-only work and do not duplicate its implementation. Reuse
the same worker for clarifications and bounded correction passes when practical.

## Review and adjust routing

1. At each meaningful slice boundary, inspect the actual diff and focused test
   evidence. Review design invariants, integration behavior, failure paths,
   unrelated changes, and test gaps.
2. Package ordinary corrections for the same worker. Resolve architecture or
   scope decisions in the main thread before delegating the resulting bounded
   work.
3. If a Luna slice reveals hidden coupling, an ambiguous or expensive acceptance
   check, high consequence of failure, or another concrete Terra signal,
   transfer the remaining work in that slice to `terra-xhigh` once and explain
   the evidence. Do not escalate merely because an ordinary defect or test
   failure needs correction.
4. Route the next slice independently from earlier choices. Keep write
   ownership non-overlapping if true parallel work is necessary.

## Close the loop

1. Perform one overall contract-focused review after the implementation slices
   are integrated.
2. Route any remaining implementation fix as a bounded slice, then review its
   actual diff. Avoid repeated full-suite runs during intermediate slices.
3. Run the repository's complete required gate once the candidate is final.
4. Keep roadmap status, architecture evidence, and commit or push decisions in
   the main thread unless the user explicitly delegates them.
5. Mark the goal complete only when the requested outcome and exit gate are
   satisfied with no required work remaining. Otherwise follow the goal
   mechanism's blocking rules and report the concrete limitation.
6. Report the final outcome, per-slice routing, worker contributions,
   validation, remaining risks, and repository state.
