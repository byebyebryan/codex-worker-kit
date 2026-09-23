# Codex Worker Kit

Reusable workers and execution workflows for a Sol XHigh primary with Luna Max
handling most bounded investigation, implementation, and validation. The primary
owns product and architecture decisions, difficult portions, review, and
acceptance. Workflows preserve the selected primary model.

## Models and responsibilities

| Role | Model | Reasoning | Responsibility |
| --- | --- | --- | --- |
| Recommended primary | `gpt-6-sol` | `xhigh` | Decisions, difficult portions, integration, and acceptance |
| Default worker `luna-max` | `gpt-6-luna` | `max` | Bounded investigation and implementation with practical verification |
| Optional worker `sol-xhigh` | `gpt-6-sol` | `xhigh` | Complex, self-contained work that benefits from separate context or independent execution |

Luna is the starting choice. Missing facts can become a focused investigation,
reproducer, or proposed options. The primary resolves difficult decisions and
hands clear implementation back to Luna when useful. It may finish a small
remainder directly when another handoff adds overhead.

A Sol worker needs a concrete benefit from separate context or independent work.
Complexity alone does not justify spawning another Sol agent when the primary
already has the context. Terra and Astra are outside automatic routing.

Escalation requires evidence: an unresolved decision, contradictory observations,
a verification gap, or repeated failure without new evidence. Cross-module work,
migrations, concurrency, security, file count, or unfamiliarity alone do not
exclude Luna. A worker may reason about options; the primary retains authority
over decisions outside the execution contract.

## Workflows

| Workflow | Scope | Delegation |
| --- | --- | --- |
| `$luna-task` | One bounded task; no goal management | Luna only; primary handles difficult portions |
| `$luna-goal-loop` | A substantial goal across cohesive assignments | Luna only; primary handles difficult portions |
| `$worker-task` | One bounded task; no goal management | Luna by default, primary directly, optional Sol worker |
| `$worker-goal-loop` | A substantial goal, routed per assignment | Luna by default, primary directly, optional Sol workers |

The Luna workflows preserve the explicit worker choice without requiring a
workflow switch when the primary needs to help. The adaptive workflows choose
whether delegation helps and which worker to use. An unavailable optional worker
returns work to the primary; an explicitly requested unavailable Luna worker is
reported without silently substituting another model.

Use one cohesive assignment and one writer by default. Reuse workers for related
corrections, keep context compact, and transfer write ownership before taking
over. Ordinary defects usually call for corrections. Failed attempts without
new evidence call for primary diagnosis rather than repeated worker cycling.

## Installation

Clone the repository and install the two current custom agents and four skills:

```sh
git clone https://github.com/byebyebryan/codex-worker-kit.git
mkdir -p ~/.codex/agents ~/.agents/skills
cp codex-worker-kit/agents/*.toml ~/.codex/agents/
cp -R codex-worker-kit/skills/. ~/.agents/skills/
```

The example uses `~/.codex/agents` for custom agents and `~/.agents/skills`
for user skills. If your client supports another personal skills directory,
install the same skill directories there. With a dotfile manager, update its
source and published pins instead of copying over managed targets.

Select the primary separately in your client or configuration:

```toml
model = "gpt-6-sol"
model_reasoning_effort = "xhigh"
```

Each custom agent pins both its model and reasoning effort. The client and
account must support these models, custom agents, and skills. A task label alone
does not select a model; workflows use the named custom agent with a compact
execution contract and minimal inherited context. See the official
[custom agent documentation](https://learn.chatgpt.com/docs/agent-configuration/subagents#custom-agents).

### Existing Terra installations

GPT-5.6 Terra compatibility files live under `legacy/` and are deprecated. They
retain the `terra-xhigh`, `$terra-task`, and `$terra-goal-loop` identities and do
not alias Sol. Install them separately only to preserve an explicit Terra workflow:

```sh
cp codex-worker-kit/legacy/agents/terra-xhigh.toml ~/.codex/agents/
cp -R codex-worker-kit/legacy/skills/. ~/.agents/skills/
```

Copying the current default bundle does not remove previously installed Terra
files. When migrating, retire the old agent and both Terra skill directories
through the configuration manager or installation method that owns them. Check
both supported personal skill roots if an earlier installation used a different
one. For archive consumers, publish the kit before changing external URLs and
checksums; do not point a deployment at an unpublished checkout.

## Validation and tuning

Run `scripts/check` after changing the kit. It validates the default and legacy
inventory, agent model/effort selections, and skill metadata. It does not prove
routing quality or runtime model availability.

Review representative behavior as well:

- A specified migration with useful acceptance checks stays with Luna.
- An unclear failure can start with a bounded Luna investigation before edits.
- A deeply coupled design decision returns to the primary, which may hand the
  resulting implementation back to Luna.
- A complex independent assignment can use Sol when its separate context helps.
- An ordinary failed test goes back for correction; repeated failure without new
  evidence returns to the primary.
- An explicit Luna workflow never silently creates a Sol or Terra worker.

Compare total primary-plus-worker usage, corrections, elapsed time, and accepted
results on representative tasks. Use runtime cost data when available; do not
infer savings from the number of Luna assignments or from token rates alone.
