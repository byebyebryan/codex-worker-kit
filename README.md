# Codex Worker Kit

Reusable Codex worker agents and execution workflows for implementation tasks.
The main agent remains responsible for product and architecture decisions,
planning, review, and acceptance.

## Worker tiers

- `luna-max` is the cost-efficient tier for clear, localized, repeatable, or
  strongly verifiable execution.
- `terra-xhigh` is the broader tier for judgment-heavy, cross-boundary, or
  consequential execution where deeper synthesis can reduce rework or risk.

The tier changes execution depth, not decision authority. Both workers return
product, architecture, and scope decisions to the main agent.

## Workflows

Task workflows handle one bounded implementation slice:

- `$luna-task` explicitly delegates to `luna-max`.
- `$terra-task` explicitly delegates to `terra-xhigh`.
- `$worker-task` selects the suitable tier for the slice using verification,
  rework, and consequence signals.

Goal-loop workflows handle substantial work across multiple slices:

- `$luna-goal-loop` keeps execution on `luna-max`.
- `$terra-goal-loop` keeps execution on `terra-xhigh`.
- `$worker-goal-loop` selects a tier independently for each slice.

All workflows keep planning, review, and acceptance in the main agent. Use an
explicit tier when you already know the worker you want; use a `worker-*`
workflow when the routing decision should be made from the task contract.

## Installation

Clone the repository and install the two custom agents and six skills:

```sh
git clone https://github.com/byebyebryan/codex-worker-kit.git
mkdir -p ~/.codex/agents ~/.agents/skills
cp codex-worker-kit/agents/*.toml ~/.codex/agents/
cp -R codex-worker-kit/skills/. ~/.agents/skills/
```

The example uses `~/.codex/agents` for custom agents and `~/.agents/skills`
for user skills. If your client supports another personal skills directory,
install the same skill directories there. The client and account must provide
the referenced worker models and support custom agents and skills; availability
can vary. Explicit workflows report an unavailable requested tier rather than
silently changing the selection.

Run `scripts/check` after copying or updating the kit.
