# AGENTS - Codex Maintenance Guide

This repository is a Claude for Financial Services fork. It contains Claude
Cowork plugins, Claude Code plugin metadata, and Claude Managed Agent cookbook
templates. Codex can maintain and adapt the files, but the runtime semantics are
still Claude-oriented unless a task explicitly asks for a Codex conversion.

## First Files To Read

1. `.agentlens/INDEX.md` - fast repository map for agents.
2. `CLAUDE.md` - canonical repository structure and development workflow.
3. `README.md` - user-facing product and installation overview.
4. `docs/codex-usage.md` - Codex-specific usage and adaptation notes.
5. `scripts/check.py` - repository validation contract.

## Source Of Truth

- Edit skill source files under `plugins/vertical-plugins/<vertical>/skills/`.
- Do not edit bundled agent skill copies first. After changing a vertical skill,
  run `python3 scripts/sync-agent-skills.py`.
- Agent system prompts live in `plugins/agent-plugins/<slug>/agents/<slug>.md`.
- Managed Agent wrappers live in `managed-agent-cookbooks/<slug>/`.
- Marketplace registration lives in `.claude-plugin/marketplace.json`.
- Plugin manifests live in each `.claude-plugin/plugin.json`.

## Codex Boundary

- Treat `SKILL.md`, agent markdown, manifests, and cookbooks as structured
  source artifacts. Preserve Claude plugin semantics unless asked to convert.
- Do not replace `claude plugin ...` instructions with Codex commands unless a
  real Codex install path is added and validated.
- If adapting content for Codex local skills, write the adaptation separately
  under `docs/`, a script, or a clearly named Codex package. Do not silently
  mutate the Claude plugin source format.
- Keep financial, legal, tax, accounting, onboarding, ledger-posting, and
  investment recommendation disclaimers intact.
- Do not add fabricated MCP credentials, endpoints, vendor subscriptions, or
  firm policies.

## Validation

Run these before committing repository structure or plugin changes:

```bash
python3 scripts/check.py
bash scripts/test-cookbooks.sh
```

Run `python3 scripts/sync-agent-skills.py` before validation when any source
skill under `plugins/vertical-plugins/*/skills/` changes.

For documentation-only Codex navigation changes, `python3 scripts/check.py` is
the minimum validation. Use `bash scripts/test-cookbooks.sh` when Managed Agent
YAML, deployment scripts, or cookbook references change.

## Change Discipline

- Keep documentation/navigation changes separate from financial workflow
  behavior changes when possible.
- Stage only files in scope. This repository may contain local agent state such
  as `.omx/`; it must not be committed.
- Preserve existing markdown and YAML style. Most files are plain Markdown,
  JSON, YAML, and shell/Python scripts.
- Prefer small, auditable edits over broad rewrites.

## Common Tasks

### Add Or Update A Skill

1. Edit `plugins/vertical-plugins/<vertical>/skills/<skill>/SKILL.md`.
2. Run `python3 scripts/sync-agent-skills.py`.
3. Run `python3 scripts/check.py`.
4. Inspect the diff for both source and bundled skill copies.

### Add Or Update An Agent

1. Update `plugins/agent-plugins/<slug>/`.
2. Update or add `managed-agent-cookbooks/<slug>/`.
3. Register the plugin in `.claude-plugin/marketplace.json` if it should appear
   in the marketplace.
4. Run `python3 scripts/check.py` and `bash scripts/test-cookbooks.sh`.

### Add Codex-Specific Guidance

1. Prefer `docs/codex-usage.md` for user-facing Codex instructions.
2. Prefer this `AGENTS.md` for agent execution rules.
3. Prefer `.agentlens/INDEX.md` for navigation shortcuts.
4. Do not create a fake Codex runtime integration without testing it.
