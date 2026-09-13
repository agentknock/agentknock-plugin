# Set up a durable Agentknock installation

The goal is that a fresh agent session can discover and use a suitable
Agentknock executable and the same pairing directory without remembered
conversation context, repeated installation, or repeated pairing. The wrapped
command must retain its expected environment and configuration.

Choose the simplest supported arrangement that achieves this in the actual
execution environment. Ordinary machines may already provide everything
needed. Other hosts may require durable storage, environment configuration, an
installation record, or a user-applied setting. No particular path, package
manager, or companion skill is required everywhere.

## Discover what the host supports

Follow the main skill's installation-record lookup before selecting defaults.
Identify the execution platform, existing installation, effective executable
search path, writable storage, and the mechanisms available for saving settings
and instructions. Inspect relevant settings without dumping credentials.

Establish which boundaries the setup must survive: a new conversation,
recreation of the execution environment, and a different machine are distinct.
Use the host's documentation and supported facilities to establish durability.
A writable directory, a mounted filesystem, or a successful test in another
shell alone does not establish survival across those boundaries.

Treat these as three separate requirements:

- The executable and any runtime dependencies remain available.
- The pairing directory remains available, private, and writable.
- A fresh session discovers the executable and selects that same directory.

Persisting instructions proves neither of the first two. Persisting a binary
and state proves nothing about whether a fresh session can find them.

## Select and persist the executable

Choose a release compatible with the execution system and the capabilities
needed for the task, respecting the user's version constraints. Reuse a suitable
existing installation. For a new installation, prefer a current supported
release; check the platform requirements and installation choices in the
[CLI documentation](https://github.com/agentknock/agentknock-cli#install-the-agentknock-client).

Evaluate the available methods against the host rather than choosing one by
habit. A verified prebuilt binary may be sufficient; a package manager may
already provide durable installation and updates; building from source may be
appropriate when no suitable artifact exists. Account for runtime dependencies,
writable caches, permissions, network access, and where the result is stored.
An `npx` invocation is not a reliable setup merely because it is one command.

The official installer targets `~/.local/bin`. Use it when that destination
fits the host; do not assume it is durable or on `PATH`. When another location
is needed, select an installation method that can place the verified executable
there. Keep enough information to update that installation without accidentally
introducing another executable earlier on `PATH`.

## Keep pairing storage independent of HOME

Select durable, private storage before first pairing. Reuse the intended state
directory for an existing pairing. It must support Agentknock's file access,
locking, and updates during use; a read-only snapshot is insufficient.

Use the selected executable's `--help` to confirm its state-directory controls.
Agentknock 0.5.0 introduced `AGENTKNOCK_HOME` and `--agentknock-home`. The option
overrides the environment variable; without either, the default is
`$HOME/.agentknock`. Prefer absolute paths in durable settings so changing the
working directory cannot select another pairing.

These controls leave the wrapped command's `HOME` unchanged. The option also
leaves its `AGENTKNOCK_HOME` environment unchanged; an environment-variable
override is inherited normally. Choose according to the host's configuration
facilities. If an older installation lacks independent state selection and
needs it, choose a compatible version that supports it rather than redirecting
`HOME` and consequently Git, SSH, and other child-tool configuration.

Use the selected directory for every Agentknock operation. Selecting a new
directory does not move an existing pairing. Resolve any intended state move
explicitly; an empty directory is not evidence that the user needs to pair again.
Keep pairing credentials in Agentknock's state storage, never in skills or
custom instructions.

## Make discovery survive a fresh session

Use the host's supported configuration mechanisms. This may mean persistent
`PATH` and state-directory settings, a documented per-plugin configuration
facility, or durable instructions specifying the executable and invocation.
Check whether the agent's noninteractive execution tools actually read shell
startup files. An export in one tool call is not persistent configuration.

When configuration alone cannot make the installation discoverable, use a
small personal skill named `agentknock-local` if the host supports saving one.
Its description should identify it as Agentknock installation configuration
and say where it applies. Preserve information for other environments when
updating an existing record. Record only the facts needed to use and maintain
this installation:

- The environment it applies to, with enough context to distinguish other
  machines, accounts, or workspaces where the skill might also be visible.
- The executable location, installation method, and any runtime requirements.
- The state-directory location and exact invocation or environment settings.
- The persistence boundaries established, and any remaining limitations.

Keep operating instructions in the upstream `agentknock` skill; the personal
skill supplies local configuration and refers back to it for usage. Do not
fork the upstream instructions or depend on the personal skill being selected
first. The upstream skill explicitly looks it up before using defaults.

Save the record durably and discoverably. Do not customize an installed plugin
cache: updates or environment recreation can replace it. A supported durable
configuration facility can make a personal skill unnecessary. If persistence
requires user-managed global instructions or another setting the agent cannot
edit, provide the exact text or change for the user to apply. Until that is
done, report the remaining dependency rather than calling setup complete.

## Verify the outcome

Exercise discovery from the cleanest supported session or execution context,
without relying on temporary exports or conversation memory. Confirm that it
finds the intended executable, runs `--version` and `--help`, and resolves the
intended state directory for `pairing status`. A not-paired result is expected
for a new installation; it does not validate persistence by itself.

Verify the wrapped command's environment is preserved without retrieving any
secret values. For a new pairing, continue with [pairing.md](pairing.md) using
the resolved invocation, then check reuse from a fresh session where possible.

Report what was established separately from what was inferred. A new shell
does not prove machine-recreation persistence; if the required boundary cannot
be tested, identify the supporting guarantee or the remaining check. If the
host lacks the required durable storage, discovery, or permissions, explain
that limitation instead of promising automatic recovery.
