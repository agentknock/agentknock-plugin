# Install Agentknock

Set up Agentknock so a fresh agent session finds a suitable executable and reuses
its pairing without conversation memory, reinstallation, or re-pairing.

Installation is complete only when executable storage, pairing storage, and their
discovery are durable. Continue until this is achieved; if it cannot be achieved,
report setup as incomplete and explain what cannot persist and why.

Reuse a suitable installation. Otherwise, select a current release compatible
with the system and task from the [official installation documentation](https://github.com/agentknock/agentknock-cli#install-the-agentknock-client),
respecting the user's version constraints.

On a regular Linux or macOS machine, use the installation and pairing defaults,
with a persistent PATH adjustment only if needed. Keep a working default setup;
custom storage and a personal skill are unnecessary.

After installation, propose [pairing](pairing.md) if the client is not paired.

## When defaults are unsuitable

Adapt only what the host requires when default locations are ephemeral,
inaccessible, or undiscoverable by future sessions.

### Storage

Establish what survives a fresh conversation versus a recreated execution
environment; neither implies portability to another machine. Persist both the
executable (including runtime dependencies) and private, writable pairing storage
across the required boundary. A saved skill preserves knowledge, not those files.
State any persistence limits using the host's guarantees; a new shell alone
does not establish durability.

Reuse the intended pairing directory. For custom storage, use `AGENTKNOCK_HOME`
or `--agentknock-home`; preserve the wrapped command's `HOME` and configuration.
Selecting another directory does not move an existing pairing.

### Discovery

Configure executable and state discovery through mechanisms future agent sessions
actually load. Shell startup edits help only if the host reads them.

If configuration alone is insufficient, save a small personal `agentknock-local`
skill through the host's supported persistent skill mechanism. Give it this
description: "Local Agentknock installation settings. Read before using Agentknock,
alongside the upstream agentknock skill."

Record:

- Executable location, installation method, and required runtime.
- Pairing-directory location and exact invocation settings.
- Established persistence boundaries and remaining limitations.
- A brief environment note to help recognize a mismatch if the skill is moved.

Keep usage instructions in the upstream skill. Pairing credentials belong only in
Agentknock's state storage; plugin caches are replaceable, so keep customization
elsewhere.

As a last resort, if no supported mechanism can persist and expose the installation
settings to future sessions, ask the user to add them to their global agent
instructions. Provide the exact text, including the applicable environment,
executable and pairing locations, and invocation settings. Discovery remains
pending until the user applies it.
