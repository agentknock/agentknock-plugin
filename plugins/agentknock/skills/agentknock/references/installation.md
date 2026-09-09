# Install or update Agentknock

Read this when the CLI is missing, needs updating, or cannot start. Installing
the plugin does not install the executable or pair the machine.

## Choose an installation method

First check `command -v agentknock` and, if present, `agentknock --version`.
Reuse a working installation. For an update, use its original installation
method so another copy does not unexpectedly take precedence on `PATH`.

Check the execution environment, not just the user's desktop OS. The client
supports x86-64 and ARM64 Linux, including WSL2, and Apple Silicon macOS.
The documented minimums are Linux 5.8 with `/proc` mounted, or macOS 15.
Native Windows and Intel macOS are not supported. Check the
[CLI README](https://github.com/agentknock/agentknock-cli#supported-platforms)
for changes to platform support.

Use the user's established package manager when applicable. Otherwise, the
official installer provides a user-local binary:

```sh
curl -fsSL https://agentknock.dev/install.sh | bash
```

It selects the latest release for the platform, checks the published SHA-256
checksum, and installs to `~/.local/bin/agentknock`. It does not require root.
Run the same command to update an installation made this way. If this directory
is not on the agent's `PATH`, use the full executable path or adjust the command
environment; a successful install does not change an existing shell's `PATH`.

Alternatives from the CLI's installation documentation:

| Existing tooling | Install | Update |
| --- | --- | --- |
| Nix | `nix profile add github:agentknock/agentknock-cli` | `nix profile upgrade agentknock-cli` |
| mise | `mise use --global github:agentknock/agentknock-cli` | `mise upgrade github:agentknock/agentknock-cli` |
| npm | `npm install --global agentknock` | `npm update --global agentknock` |
| Cargo | `cargo install --locked agentknock` | Run the same command again |

The npm package requires Node.js `^22.15.0` or `>=24.0.0`; building with Cargo
requires Rust 1.89 or later. For temporary use, `npx agentknock --help` or
`nix run github:agentknock/agentknock-cli -- --help` can run without a persistent
installation. With Nix, the first `--` belongs to `nix run`; a wrapped command
still needs Agentknock's own `--` separator.

## Verify and continue

Run `agentknock --version` and `agentknock --help` through the same execution
environment the agent will use for tasks. If they fail, resolve the executable,
runtime, or platform error before trying to pair. Do not delete pairing state
as part of installation or an ordinary update.

If the user needs release provenance verification or a manual archive install,
consult the [CLI installation documentation](https://github.com/agentknock/agentknock-cli#install-the-agentknock-client).

For first use, continue with [pairing.md](pairing.md).
