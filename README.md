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

## Updates

Every change merged to `master` publishes an update. Installed copies receive
it when their host next updates or syncs. Git commits identify revisions;
there are no numbered plugin releases or release artifacts.

The [CI workflow](.github/workflows/ci.yml) checks formatting, Markdown,
workflow syntax, package structure, skill frontmatter, and local links.

## Contributing

Start with an issue. External pull requests are supporting prototypes or
reproductions; maintainers write the final changes. See
[CONTRIBUTING.md](CONTRIBUTING.md) for details.

Report vulnerabilities privately using [SECURITY.md](SECURITY.md).

## License

Agentknock plugin is licensed, at your option, under either the
[Apache License 2.0](LICENSE-APACHE) or the [MIT License](LICENSE-MIT).
