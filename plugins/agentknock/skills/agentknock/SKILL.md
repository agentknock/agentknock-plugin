---
name: agentknock
description: Use Agentknock to run commands with phone-approved secrets, authenticate with SSH keys, or sign Git commits. Also use when installing Agentknock or pairing it with the user's phone.
---

# Agentknock

Agentknock supplies secrets to a command after approval on the user's phone.
Environment secrets go directly to the command; SSH private keys stay on the
phone. Use it to accomplish the user's task without bringing secret values
into the conversation.

## Read only what you need

- For installation, updates, or a missing executable, read
  [installation.md](references/installation.md).
- For an absent, pending, or broken pairing, read
  [pairing.md](references/pairing.md).
- For command syntax and options, use the installed CLI's `--help`, usually
  `agentknock run --help`. Consult other subcommands' help when needed. The
  CLI is evolving; use its help rather than guessing flags.

An already working installation and pairing need no repeated setup checks.

## Choose the secret and command

Use secret names supplied by the user or already established in this session.
When the names or their contents are unknown, run `agentknock secret list`.
It contacts the phone and returns JSON metadata: names, descriptions, variable
names, and SSH public keys, never secret values. Reuse that information until
there is a reason to refresh it. Example names in documentation are not names
to assume exist on the user's phone.

Wrap the command that needs the secret:

```sh
agentknock -s SECRET --reason "Explain the purpose of this command" -- COMMAND ARGUMENTS
```

Give a short, specific reason that helps the user recognize the request on
their phone. Choose the secrets needed for this command. If an environment
secret contains unrelated variables, use the delivery controls in `run --help`
to select the needed ones. Renaming and stdin delivery can adapt a stored
variable to a tool's interface without revealing its value to the agent.

Agentknock launches an executable, not an implicit shell. Prefer wrapping the
tool directly. Shell aliases and functions are not executables; shell operators
outside the wrapped command do not extend its secret-bearing environment.
When a script or explicit shell is needed, keep its work within the requested
task and quote it so expansion happens in the intended process.

Agentknock is not a sandbox: the command and its descendants can disclose the
values they receive. Do not retrieve credentials with `env`, `printenv`, shell
tracing, or an echo command, or write them into agent configuration. Verify
access through the intended operation instead.

## Execute and wait

Run as the paired user, with access to the real home directory and the network.
Agentknock stores sensitive pairing state in `~/.agentknock` and may update it
even during secret use or listing. SSH and Git signing also need local Unix
sockets. If the agent's execution sandbox blocks these facilities, use its
normal permission mechanism for the command. Do not change `HOME`, copy pairing
state, or re-pair merely to work around sandbox restrictions.

Allow time for a person to respond on their phone. A tool call returning a
running process or session identifier is not a failed command: keep that
session and wait for its completion. Tell the user when phone interaction is
needed, and continue independent work while waiting when possible. Do not
start duplicate requests or impose a short command timeout on an approval wait.

The phone can ask separately for SSH authentication or a Git signature after
the command has started. Keep waiting on the original command through these
requests. Completion of the initial approval does not mean the task succeeded.

On a denial, report it and stop that attempt. On another failure, distinguish
an Agentknock request failure from an error in the launched command. If the
command started, check what it actually did before retrying a mutation.

## SSH and Git signing

Wrap the usual SSH or Git command with the selected SSH secret. Agentknock can
offer the key and obtain signatures, but it does not configure remote account
access or SSH host trust.

For Git signing, preserve the repository's signing choices. Agentknock does
not enable signing or change `gpg.format`; Git must already request SSH signing
or be instructed to do so for that command. An explicit `user.signingKey` or
SSH `IdentityAgent` setting can select a different key or agent. Inspect these
settings when the expected phone request does not appear, rather than assuming
the pairing failed. Use `run --help` for the available SSH and signing controls.
