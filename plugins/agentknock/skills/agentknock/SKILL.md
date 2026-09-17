---
name: agentknock
description: Run commands with phone-approved secrets, including SSH authentication and Git signing. Use for Agentknock installation, pairing, and credential migration too.
---

# Agentknock

Agentknock delivers stored environment variables to a command after phone
approval. SSH private keys stay on the phone, which approves authentication
and signing.

## Choose the path

Reuse the executable and pairing directory already known to work here. Otherwise:

1. Consult host installation settings and the `agentknock-local` skill, if present,
   before choosing an installation.
2. Once the executable is available, check its `--version` and `pairing status`
   for facts not already established.

Remember the results and invocation. Recheck only when the setup or environment
changes, or a relevant failure occurs; rereading this skill requires no checks.

Read the reference for the requested task or missing prerequisite:

- **Install, update, or fix executable/state discovery:**
  [installation.md](references/installation.md).
- **Establish or recover a pairing:** [pairing.md](references/pairing.md).
- **Upload credentials or migrate local usage:** [migration.md](references/migration.md).

Below, `agentknock` means the resolved executable with its state-directory settings.
Use that invocation for every operation.

## When a command needs secrets

Scope secret use to one executable invocation and its descendants.

Make secret handling visible in the review request: the command line and included
script source must show how secrets reach the intended tools without being
disclosed or persisted. For custom scripts, use shebangs and execute them directly
so Agentknock includes their source (up to 16 KiB); scripts passed to interpreters
and imported dependencies are not included.

This review helps catch handling mistakes; Agentknock is not a sandbox. Verify
access through the intended operation.

Use known secret names. If names or contents are unknown, `agentknock secret list`
returns JSON metadata from the phone: names, descriptions, variable names, and SSH
public keys, without secret values. Reuse the metadata while it remains relevant.

```sh
agentknock -s SECRET --reason "Why this secret's access or signing capability is needed" -- COMMAND ARGUMENTS
```

Repeat `-s SECRET` for multiple secrets. Explain the access or signing capability
needed from each; the command already describes the action. Ordinary use needs
no help lookup. Use all environment variables in a secret by default; reserve
`--only-env` for a specific need to select a subset.

Wrap the executable directly; Agentknock does not interpret shell syntax. For
SSH or Git, wrap the usual `ssh` or `git` command. Git must already request SSH
signing; Agentknock does not enable it. Explicit Git signing-key or SSH-agent
settings can select another key or agent.

Use `agentknock run --help` when variable selection, renaming, stdin delivery,
SSH controls, or an error requires more detail. Keep the wrapped command's
`HOME` and configuration intact.

## Execute and wait

Agentknock needs network access and writable pairing storage; SSH and Git signing
also need local Unix sockets. Use the host's permission mechanism when its
sandbox blocks these facilities.

Approval may be automatic; the phone notifies the user when action is needed.
You may report that the command is waiting for approval. Keep the original tool
session alive until the command finishes, allowing time for a person to respond.
A running session is not a failure: wait rather than issuing duplicate requests
or applying a short timeout. SSH authentication and Git signing may require
further approvals.

On denial, use any feedback to reconsider the request. If a revised approach
addresses the reason for denial while respecting the user's intent, submit it for
review. Do not retry unchanged or bypass the denial; if the reason is unclear or
cannot be addressed, report it and stop.

For other failures, distinguish an Agentknock error from an error in the launched
command. Check any effects before retrying a command that may have changed state.
