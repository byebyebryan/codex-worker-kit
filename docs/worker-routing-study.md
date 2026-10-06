# Worker routing research

Date: 2026-10-06. Scope: published experiments, first-party engineering
experience, and current Codex documentation relevant to the
[routing design](worker-routing-design.md). Active workflows are unchanged.

Selective delegation and coordination overhead are established research topics.
The evidence supports keeping the adaptive workflows led by the primary,
delegating suitable work to Luna, and treating another Sol agent as a separate
execution choice. It does not establish an optimal threshold for our particular
Sol XHigh and Luna Max pairing. Keep the resulting policy short and evaluate
accepted outcomes rather than prescribing an elaborate process.

## Selective model use has a quality and cost tradeoff

[RouteLLM](https://arxiv.org/html/2406.18665v4), first submitted in June 2024
and revised in February 2025, learns whether the stronger model is likely to
outperform the weaker model, then varies a threshold to trade response quality
against strong-model usage. This is a controlled routing study using preference
data and answer benchmarks. Its signal is the comparative benefit of the
stronger model, rather than a fixed rule that every request should start cheap.
It does not measure the context transfer and acceptance costs of delegated
repository work.

[FrugalGPT](https://arxiv.org/abs/2305.05176), May 2023, is earlier work on
learned model cascades that reduces cost while preserving answer quality on
its evaluated tasks. It establishes that cheaper models can be useful within
a quality constraint; its historical savings and cascade structure are not
parameters for this kit.

[AgentRouter](https://arxiv.org/pdf/2609.22951), September 2026, studies routing
individual steps within agent trajectories. Its useful distinction is that a
weak output can affect later steps, so judging a step in isolation misses part
of the cost. The paper also reports degraded routing accuracy when transferred
to another orchestration framework. This is a recent, trained-router example,
not evidence to adopt its classifier, model tiers, or savings estimates here.

**Application to this kit:** base Luna delegation on a sound assignment and
credible verification, with a likely saving in total accepted-result effort.
Evaluate the whole task. A primary that has already resolved most of a slice
may have little left to save by handing off the remaining edits.

## Task structure matters more than an extra agent label

[Towards a Science of Scaling Agent Systems](https://arxiv.org/html/2512.08296v3),
first submitted in December 2025 and revised in April 2026, compares 260
configurations across six agentic benchmarks, five architectures, and three
model families. Results vary strongly by domain: decomposable work can benefit,
while sequential dependencies and communication can consume the reasoning
budget. The coding evaluations use 20-instance subsets; the tested models do
not include our GPT-6.1 Sol and GPT-6 Luna pair. Its reported saturation point
and architecture rankings should not become universal thresholds.

[Cognition's context-engineering account](https://cognition.com/blog/dont-build-multi-agents),
June 2025, identifies two practical hazards: losing relevant context during
handoff and allowing workers to make conflicting implicit decisions. Separate
file ownership does not settle shared decisions about behavior or integration.
This is engineering judgment from a coding-agent developer, rather than a
controlled demonstration that all multi-agent systems fail.

[OpenHands' single-agent account](https://www.openhands.dev/blog/dont-sleep-on-single-agent-systems),
September 2024, describes how fixed role divisions can restrict the tools or
context needed to solve a task. It favors a capable generalist where that
structure does not help. The historical article is a design argument, not a
current benchmark ranking.

**Application to this kit:** keep tightly connected reasoning in the primary.
Delegate across a meaningful responsibility boundary once shared invariants
are clear. Give the worker compact but sufficient context and access to the
authoritative artifacts; brevity alone is not a good handoff metric.

## Multi-agent gains can buy more work rather than cheaper work

[Anthropic's research-system account](https://www.anthropic.com/engineering/multi-agent-research-system),
June 2025, describes gains on an internal research evaluation, especially when
independent search directions can run in parallel and return compressed
findings. It also identifies substantial token usage and a poor fit for domains
with shared context and many dependencies, including much coding work. Its
15-times token figure compares multi-agent research with chat interactions;
it is not a measured 15-times penalty for adding one worker to a coding task.

[Anthropic's coordinator cookbook](https://platform.claude.com/cookbook/managed-agents-cma-plan-big-execute-small)
compares cheap reading workers with a solo frontier model under a matched
verification standard and meters actual bills. It reports a fixed setup cost
per worker and higher bills when briefs become too narrow. Both approaches
also verified facts within an incorrectly chosen set of parks: checking
subtask results did not validate the decomposition. The example demonstrates
an economic mechanism on a particular research workload, not a savings ratio
for coding. Its counterfactual price table contains an introductory rate with
an August 2026 expiry, so that table should not be reused as current pricing.

Current [Codex subagent guidance](https://learn.chatgpt.com/docs/agent-configuration/subagents#why-subagent-workflows-help)
also identifies isolated context and parallel read-heavy work as benefits, and
warns that parallel writes add conflicts and coordination.

**Application to this kit:** retain parallel execution and context isolation as
possible reasons for a Sol worker. A substantial, bounded reading or evidence
gathering task can also suit Luna. Preserve access to raw evidence when the
primary needs to judge its nuances, and review whether the decomposition covers
the user's actual request. Different files alone do not justify parallel work.

## Another same-model perspective is not proof of correctness

[The Cost of Consensus](https://arxiv.org/html/2605.00914v1), April 2026,
compares homogeneous debate with isolated self-correction on two difficult
reasoning benchmarks. Its main experiments use 7–8B models and find peer
conformity, destabilized correct reasoning, and added token cost. Those results
concern unguided debate; they do not directly test detached Sol code review.

The evidence is not uniformly against multiple reasoning paths.
[Multi-Agent Reasoning Improves Compute Efficiency](https://arxiv.org/html/2605.01566v1),
May 2026, finds some debate and mixture-of-agents configurations outperform
self-consistency under comparable estimated compute. It uses Llama models on
MMLU-Pro and BBH, with theoretical compute estimates and overlapping confidence
intervals for some configurations. Those are reasoning experiments rather than
end-to-end coding handoffs or billed Codex usage.

**Application to this kit:** preserve an optional independent review for a
specific question. Ask for findings tied to code, requirements, tests, or other
evidence. Treat agreement between agents as a judgment to inspect, and keep
actual acceptance checks. The papers do not justify mandatory reviewers or a
debate loop for ordinary work.

## Simple instructions still need clear boundaries and verification

[Building effective agents](https://www.anthropic.com/engineering/building-effective-agents),
December 2024, recommends simple, composable patterns and adding complexity
when outcomes justify it. It distinguishes routing, parallelization, and
dynamic worker delegation, and emphasizes clear evaluation criteria. The page
notes that its tooling landscape has since changed. The useful enduring lesson
is simplicity with task feedback, rather than adopting its examples as a
mandatory sequence.

[OpenAI's guidance on revisiting skills](https://developers.openai.com/blog/rethinking-skills-and-prompts-for-gpt-6-astra),
September 2026, cautions against broad descriptions, repeated guidance, and
elaborate itineraries, and encourages loading detail only when relevant. It is
specifically about GPT-6 Astra and explicitly notes that models can benefit
from different instructions. It supports auditing this kit's prompt size and
triggers; it does not prove that guidance useful to Sol or Luna can be removed.

[Why Do Multi-Agent LLM Systems Fail](https://arxiv.org/html/2503.13657v3),
first submitted in March 2025 and revised in October 2025, analyzes more than
1,600 traces across seven systems and identifies 14 failure modes grouped
around system design, agent coordination, and verification. Repetition, lost
context, wrong assumptions, and incomplete checks are useful failure categories
to recognize. The taxonomy should inform targeted corrections, not become
another role hierarchy or a universal prediction for newer models.

[AI Agents That Matter](https://arxiv.org/html/2407.01502v1), July 2024,
shows why agent evaluations need cost controls, simple baselines, and adequate
holdouts. Its HumanEval experiments find inexpensive baselines competitive
with more elaborate agents. Function-generation tasks and historical prices
limit direct transfer, but the evaluation principle applies: retain usage
counts so comparisons can be repriced, and report quality alongside expense.

**Application to this kit:** put the routing policy in a few sentences. Keep
the existing compact assignment, ownership, and review practices. Evaluate
several real task shapes, including cases different from the examples used to
write the instructions. These research notes are supporting material for
refining routing, rather than required reading before each task.

## Explicit activation remains a separate issue

Current [Codex skill documentation](https://learn.chatgpt.com/docs/build-skills#optional-metadata)
says `allow_implicit_invocation: false` prevents implicit invocation while
allowing explicit `$skill` use. Both adaptive skills already have that policy
in the inspected source and local installation. Reinforce the named-skill
boundary in descriptions and opening instructions, but do not treat a prose
change as proof that the reported runtime misrouting has been fixed.

## Proposed policy after the study

These are design inferences for this kit, not experimentally optimized rules:

1. Keep adaptive work in the primary when delegation's benefit is uncertain.
2. Use Luna for a clear, reviewable assignment when its expected savings cover
   the handoff and acceptance effort. A focused investigation can qualify.
3. Keep difficult or closely connected reasoning in the primary. A Sol worker
   needs a separate benefit from parallel execution, isolated investigation,
   or independent review.
4. Supply sufficient context, preserve shared invariants, and verify both the
   assigned result and its fit within the user's overall request.
5. Keep explicit Luna workflows intact and adaptive activation explicit.

A candidate short routing paragraph:

> Keep work in the primary when delegation's benefit is uncertain. Delegate to
> Luna when the assignment and verification are clear and the expected savings
> justify the handoff. If Luna is not a confident fit, continue in the primary.
> Use a Sol worker only when independent execution offers a concrete benefit.

Avoid a trained router, numeric confidence scores, fixed role graphs, mandatory
cheap-first attempts, automatic Sol escalation, and routine debate. None is
necessary to apply the useful findings here.

## What a practical comparison should measure

Compare the current instructions, the proposed selective policy, and primary
execution on comparable task outcomes. Record accepted results, actual model
and reasoning settings, primary and worker usage, corrections or takeovers,
and elapsed time. Use billed cost when available and retain token categories
for later repricing. Keep success criteria equal across routes.

Include a clear bounded fix, specified migration, evolving diagnosis, small
remainder, substantial evidence gathering, and work with shared decisions.
Assess optional parallelism separately from the primary-versus-Luna choice.
Check activation in fresh sessions with generic goal-loop wording, named
adaptive and Luna workflows, and requests to discuss the skills.

The online evidence supports a lightweight refinement, but it supplies neither
an optimal delegation percentage for our models nor a diagnosis of the reported
activation issue. Those conclusions depend on actual kit behavior.
