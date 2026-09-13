# Agentknock plugin

Skill, plugins, and marketplaces for using the
[Agentknock CLI](https://github.com/agentknock/agentknock-cli) with Codex and
Claude Code.

The skill covers using secrets through Agentknock. Installation, pairing, and
secret upload/migration instructions are separate references, loaded only when
needed. Installation guidance addresses durable storage and discovery in fresh
sessions, with an optional personal `agentknock-local` skill for local settings.

Both plugins share `plugins/agentknock/skills/agentknock/SKILL.md`.
Platform-specific manifests live alongside the shared skill:

- Codex: `plugins/agentknock/.codex-plugin/plugin.json`
- Claude Code: `plugins/agentknock/.claude-plugin/plugin.json`

The repository provides a marketplace catalog for each platform:

- Codex: `.agents/plugins/marketplace.json`
- Claude Code: `.claude-plugin/marketplace.json`
