# Agentknock agent skill and plugins

Teach your agent to use phone-approved secrets.

[Agentknock](https://agentknock.dev/) lets command-line tools use credentials
stored on your phone. Environment secrets are delivered to the approved command;
SSH private keys stay on the phone for authentication and Git signing.

The [Agentknock skill](plugins/agentknock/skills/agentknock/SKILL.md) teaches an
agent to install and pair Agentknock, run commands with secrets, and migrate
existing credentials to your phone. Any LLM agent can use these instructions;
executing commands requires an environment that can run the
[Agentknock CLI](https://github.com/agentknock/agentknock-cli).

This repository also provides [plugin packaging](plugins/agentknock) with
OpenAI, Anthropic, and Cursor marketplace catalogs and metadata. The installation
examples below cover Codex CLI, Claude Code, workspace-managed ChatGPT Work, and
Cursor / Grok Bot; the skill itself is independent of those hosts.

The skill and plugins contain instructions. Install the CLI separately, either
yourself or with your agent's help.

> Early release · [Share feedback](mailto:agentknock@fulldisclosure.fi)

## Install the skill

Use your host's skill installer, or copy the complete
[agentknock skill directory](plugins/agentknock/skills/agentknock) into its
supported skills location. Keep the `references/` directory alongside `SKILL.md`.

An agent without a skill-loading mechanism can read `SKILL.md` and consult its
linked references directly. Make those files accessible to the agent and point
it to the skill when asking it to use Agentknock.

## Install the plugin

For hosts with OpenAI, Anthropic, or Cursor plugin support, install the packaged
skill through a marketplace.

### Cursor and Grok Bot

Cursor and Grok Bot install plugins from the [Cursor Marketplace](https://cursor.com/marketplace).
This repository includes Cursor packaging under `.cursor-plugin/` and
`plugins/agentknock/.cursor-plugin/`.

Until Agentknock is listed in the public marketplace:

1. Submit this repository at [cursor.com/marketplace/publish](https://cursor.com/marketplace/publish)
   (or ask the Cursor team to list it), **or**
2. For local testing in Cursor, copy or symlink `plugins/agentknock` to
   `~/.cursor/plugins/local/agentknock` and reload Cursor.

After the plugin is listed, install **Agentknock** from the Cursor Marketplace
in Cursor or Grok Bot. The skill becomes available to the agent automatically.

### Codex CLI

Run these commands in your terminal:

```sh
codex plugin marketplace add agentknock/agentknock-plugin --ref master
codex plugin add agentknock@agentknock
```

Start a new Codex session. Use `$agentknock` to select the skill explicitly,
or mention Agentknock in your request.

### Claude Code

Run these commands in your terminal:

```sh
claude plugin marketplace add https://github.com/agentknock/agentknock-plugin.git#master
claude plugin install agentknock@agentknock
```

Start a new Claude Code session. Use `/agentknock:agentknock` to select the
skill explicitly, or mention Agentknock in your request.

### ChatGPT Work

For a workspace-managed installation, a workspace admin can import this GitHub
marketplace through **Admin → Plugins → Add → Import marketplace**:

- **Source:** `https://github.com/agentknock/agentknock-plugin`
- **Path:** leave empty.
- **Branch, tag, or commit:** `master`.

The admin then makes Agentknock available to the appropriate workspace roles.
Install it from the workspace's Plugins tab and start a new Work conversation.
See [OpenAI's workspace plugin instructions](https://learn.chatgpt.com/docs/enterprise/plugin-management)
for availability and access requirements.

## Get started

You need the Agentknock mobile app to pair a client and use secrets. See the
[mobile installation instructions](https://github.com/agentknock/agentknock-cli#install-the-agentknock-mobile-app)
for supported phones and downloads.

After making the skill available to your agent, ask:

> Set up Agentknock on this machine.

The agent can reuse an existing CLI installation or help install one. On a
regular Linux or macOS machine it uses the normal defaults. In a hosted
environment, it works out how the installation and pairing can persist across
sessions and explains any limitations.

To pair the client:

> Pair Agentknock with my phone.

The agent starts pairing and shows a verification code. Compare the complete
code with your phone, approve only if it matches, and reply to the agent so it
can finish pairing.

Once paired, ask for the operation you want:

> Use Agentknock to list the issues in my GitHub repository.
>
> Sign this Git commit using my SSH key in Agentknock.
>
> Help me migrate my local SSH key to Agentknock.

The agent can discover the available secret names and wraps the command with
Agentknock. Approval may be automatic; your phone notifies you when action is
needed. The command waits while approval is pending.

For a new account, add secrets in the mobile app. Existing users can reuse the
secrets already on their phone after pairing another client.

## Updates

Every change merged to `master` publishes a skill and plugin update. Installed copies
receive it when their host next updates or syncs. Git commits identify revisions;
there are no numbered plugin releases or release artifacts.

If you installed the skill directly, update it through your host's skill installer
or replace the complete skill directory with the latest copy from `master`.

For Codex CLI, refresh the marketplace and the installed plugin:

```sh
codex plugin marketplace upgrade agentknock
codex plugin add agentknock@agentknock
```

For Claude Code, refresh the marketplace and update the plugin:

```sh
claude plugin marketplace update agentknock
claude plugin update agentknock@agentknock
```

Start a new session after updating. Claude Code also offers an auto-update
setting under **/plugin → Marketplaces → agentknock**; third-party marketplaces
have it disabled by default. See the
[Claude Code update instructions](https://code.claude.com/docs/en/discover-plugins#configure-auto-updates).

Workspace-managed ChatGPT installations follow the workspace's marketplace sync
settings. Cursor Marketplace listings refresh when Cursor or Grok Bot syncs the
published plugin. Plugin updates update the instructions; update the Agentknock
CLI through the method used to install it.

## Feedback and contributions

[Open an issue](https://github.com/agentknock/agentknock-plugin/issues/new/choose)
for problems or suggestions involving the skill, plugins, or marketplaces.
Include your agent host and relevant behavior, with sensitive information removed.
For problems with the CLI itself, use the
[CLI repository](https://github.com/agentknock/agentknock-cli/issues/new/choose).

Contributions start with issues. External pull requests provide prototypes or
reproductions; maintainers write the final changes. See
[CONTRIBUTING.md](CONTRIBUTING.md) for details.

Report vulnerabilities privately using [SECURITY.md](SECURITY.md).

## Development

Both plugins share the [Agentknock skill](plugins/agentknock/skills/agentknock/SKILL.md).
Installation, pairing, and migration guidance lives in its `references/` directory
and is loaded only when needed.

The [CI workflow](.github/workflows/ci.yml) checks formatting, Markdown, workflow
syntax, package structure, skill frontmatter, and local links. It contains the
pinned tools and commands used for these checks. Passing CI validates structure;
changes to agent behavior also need testing in a fresh session.

## License

This repository is licensed, at your option, under either the
[Apache License 2.0](LICENSE-APACHE) or the [MIT License](LICENSE-MIT).
