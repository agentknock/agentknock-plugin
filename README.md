# Agentknock plugin

Skill, plugin, and marketplace scaffolding for using the
[Agentknock CLI](https://github.com/agentknock/agentknock-cli) with Codex and
Claude Code.

This repository contains placeholders. Agentknock workflow instructions have
not been implemented yet.

Both plugins share `plugins/agentknock/skills/agentknock/SKILL.md`.
Platform-specific manifests live alongside the shared skill:

- Codex: `plugins/agentknock/.codex-plugin/plugin.json`
- Claude Code: `plugins/agentknock/.claude-plugin/plugin.json`

The repository provides a marketplace catalog for each platform:

- Codex: `.agents/plugins/marketplace.json`
- Claude Code: `.claude-plugin/marketplace.json`
