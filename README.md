# Agentknock plugin

Skill, plugins, and marketplaces for using the
[Agentknock CLI](https://github.com/agentknock/agentknock-cli) with Codex and
Claude Code.

The skill covers running commands with Agentknock. Installation and pairing
instructions are separate references, loaded only when needed.

Both plugins share `plugins/agentknock/skills/agentknock/SKILL.md`.
Platform-specific manifests live alongside the shared skill:

- Codex: `plugins/agentknock/.codex-plugin/plugin.json`
- Claude Code: `plugins/agentknock/.claude-plugin/plugin.json`

The repository provides a marketplace catalog for each platform:

- Codex: `.agents/plugins/marketplace.json`
- Claude Code: `.claude-plugin/marketplace.json`
