# AgentLens Index

Fast map for agents working in this repository.

## What This Repo Is

`financial-services-codex` is a fork of a Claude financial-services plugin
repository. It contains:

- Claude Cowork / Claude Code plugin manifests.
- Financial-services `SKILL.md` packages.
- Named workflow agents.
- Managed Agent cookbook templates.
- MCP connector manifests for financial data providers.
- Codex-facing maintenance docs added in this fork.

## Start Here

| Need | File or directory |
|---|---|
| Codex maintenance rules | `AGENTS.md` |
| Repository structure | `CLAUDE.md` |
| User-facing overview | `README.md` |
| Codex usage and adaptation notes | `docs/codex-usage.md` |
| Validation script | `scripts/check.py` |
| Skill sync script | `scripts/sync-agent-skills.py` |
| Managed Agent dry-run tests | `scripts/test-cookbooks.sh` |

## Main Surfaces

| Surface | Path | Notes |
|---|---|---|
| Marketplace manifest | `.claude-plugin/marketplace.json` | Registers all plugins and source paths. |
| Named agents | `plugins/agent-plugins/<slug>/` | Self-contained agent bundles. |
| Canonical agent prompts | `plugins/agent-plugins/<slug>/agents/<slug>.md` | Source prompt for plugin and cookbook wrappers. |
| Bundled agent skills | `plugins/agent-plugins/<slug>/skills/` | Synced copies; do not edit first. |
| Canonical vertical skills | `plugins/vertical-plugins/<vertical>/skills/` | Edit these first. |
| Slash commands | `plugins/vertical-plugins/<vertical>/commands/` | Claude command entrypoints. |
| MCP manifests | `plugins/**/.mcp.json` | Provider connector declarations. |
| Managed Agent cookbooks | `managed-agent-cookbooks/<slug>/` | `agent.yaml`, subagents, security notes, examples. |
| Microsoft 365 installer plugin | `claude-for-msft-365-install/` | Separate Claude Code plugin for add-in setup. |

## Validation Shortcuts

```bash
python3 scripts/check.py
bash scripts/test-cookbooks.sh
```

When a canonical vertical skill changes:

```bash
python3 scripts/sync-agent-skills.py
python3 scripts/check.py
```

## Codex-Specific Notes

- This fork is Codex-friendly for maintenance and adaptation.
- Runtime plugin installation is still documented for Claude unless a future
  task adds and validates a Codex-native package.
- Keep Claude source format intact when adding Codex documentation.
- `.omx/` is local agent state and should stay out of source control.
