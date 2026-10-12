# decision-red-team-pro — Evidence-based decision analysis and red-team Agent Skill

[中文](README.md) | [English](README.en.md)

decision-red-team-pro is an Agent Skill for comparing consequential choices, examining failure mechanisms, separating evidence from assumptions and designing reversible validation steps. It supports technology selection, project proposals, career choices and other decisions. Installation does not create a standalone bot, internet access or a multi-agent scheduler.

## First task: technology migration

After installation, use this example in Codex:

```text
$decision-red-team-pro Use standard mode to compare keeping our current system,
migrating one low-risk service and a full migration to option A.
Goal: reduce maintenance cost. Constraints: stay within our current budget,
preserve rollback and avoid disruption to critical operations.
Ask for cost, incident and maintenance data. Separate facts from assumptions.
Give the strongest evidence on both sides, a conditional recommendation,
the smallest useful validation step and conditions that would reverse the advice.
Do not invent numerical estimates when evidence is missing.
```

Claude Code uses `/decision-red-team-pro`. This is an illustrative prompt, not a completed analysis. Expect an evidence-aware comparison, unresolved assumptions and validation actions; conclusions depend on supplied material and available verification tools.

## Install the complete directory

```bash
git clone https://github.com/vmayfuture/decision-red-team-pro.git decision-red-team-pro
```

Copy the whole directory, preserving `SKILL.md` and `references/`, into **one** host-specific skills parent:

| Agent | Project parent | User parent | Invocation |
| --- | --- | --- | --- |
| Codex | `.agents/skills/` | `~/.agents/skills/` | `$decision-red-team-pro` or desktop skill selector |
| Claude Code | `.claude/skills/` | `~/.claude/skills/` | `/decision-red-team-pro` |
| Gemini CLI | `.gemini/skills/` | `~/.gemini/skills/` | Request activation by name |
| GitHub Copilot | `.github/skills/` | `~/.copilot/skills/` | `/decision-red-team-pro` in supported local hosts |
| Cursor | `.cursor/skills/` | `~/.cursor/skills/` | Select the skill from `/` in Agent chat |
| OpenCode | `.opencode/skills/` | `~/.config/opencode/skills/` | Ask the native `skill` tool to load it |

A PowerShell example for Codex, run from the clone's parent directory:

```powershell
$decisionSource = (Resolve-Path -LiteralPath './decision-red-team-pro').Path
$decisionParent = Join-Path $env:USERPROFILE '.agents/skills'
$decisionTarget = Join-Path $decisionParent 'decision-red-team-pro'
if (Test-Path -LiteralPath $decisionTarget) { throw 'Target exists; inspect it before updating.' }
New-Item -ItemType Directory -Path $decisionParent -Force | Out-Null
Copy-Item -LiteralPath $decisionSource -Destination $decisionTarget -Recurse -ErrorAction Stop
```

The final entry must be `<skills-parent>/decision-red-team-pro/SKILL.md`. Copying that file alone loses the relative references. The [Chinese guide](README.md) includes full PowerShell/macOS/Linux checks and platform sources, verified there on 2026-10-05. Host versions and organization settings may differ. GitHub cloud agents need repository-visible skills; local user directories are not available there.

## Analysis modes

| Mode | Use case | Deliverable |
| --- | --- | --- |
| quick | Low cost, reversible, fast feedback | Opposition, support, unknowns, advice and reversal conditions |
| standard | General comparison; default | Key evidence, option assessment and next steps |
| deep | High downside, hard to reverse, slow feedback | Evidence ledger, scenarios, sensitivity and exit conditions |
| audit | Decision made; improve execution | Failure mechanisms, warnings, mitigations and rollback |
| incremental | New evidence about an earlier decision | Update affected assumptions and conclusions |

Incremental is an update style usable with any depth. Supply goals, alternatives (including the status quo), constraints, deadline, documents and acceptable downside. Preferences affect utility; feelings are not factual evidence. Missing thresholds must be identified, not replaced with arbitrary numbers.

The six recommendation levels are: strongly recommend proceeding; recommend proceeding; lean toward proceeding subject to prerequisites; defer and validate key assumptions; lean against proceeding; clearly recommend against proceeding. Strength is not a guarantee of the outcome.

## Useful cases and follow-up

- Technology selection: compare a pilot with full migration; test maintenance and rollback assumptions before expansion.
- Project approval: examine customer evidence, budget constraints and the cheapest useful validation step.
- Execution audit: turn failure mechanisms into monitoring, mitigation and exit conditions.

```text
$decision-red-team-pro Update the previous analysis with this pilot report.
Identify changed assumptions, remaining unverified claims and whether advice
or rollback conditions should change.
```

## Reference files and boundaries

[SKILL.md](SKILL.md) is the agent entry point. [Deep analysis](references/deep-analysis.md) covers evidence ledgers, failure trees, scenarios and sensitivity. [Domain playbooks](references/domain-playbooks.md) supply domain methods. References are in Chinese.

Single-agent use is the default. Multiple agents are optional when the host supports scheduling and the task warrants it; they share the decision, constraints and evidence ledger. Consensus does not independently verify claims. The package installs no host-specific sub-agent configurations.

**No internet?** Use supplied materials, mark stale/unverified claims and give conditional conclusions. The skill has no API credentials, execution scripts or trading functions.

**Does invoking it authorize action?** No. Analysis does not authorize signing, sending, trading or executing plans. Tools and authorization come from the host and current user request.

**Does it prove a decision is safe?** No. Evidence quality, missing information, sensitivity and model limitations determine confidence; persuasive reasoning is not validation.
