# Agentknock plugin

Use phone-approved secrets with Codex and Claude Code.

[Agentknock](https://agentknock.dev/) lets command-line tools use credentials
stored on your phone. Environment secrets are delivered to the approved command;
SSH private keys stay on the phone for authentication and Git signing.

This plugin teaches your agent to install and pair Agentknock, run commands with
secrets, and migrate existing credentials to your phone. It contains instructions;
the [Agentknock CLI](https://github.com/agentknock/agentknock-cli) is installed
separately, either by you or with your agent's help.

## Install the plugin

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

After installing the plugin, ask your agent:

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

Every change merged to `master` publishes a plugin update. Installed copies
receive it when their host next updates or syncs. Git commits identify revisions;
there are no numbered plugin releases or release artifacts.

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
settings. Plugin updates update the instructions; update the Agentknock CLI
through the method used to install it.

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

Agentknock plugin is licensed, at your option, under either the
[Apache License 2.0](LICENSE-APACHE) or the [MIT License](LICENSE-MIT).
