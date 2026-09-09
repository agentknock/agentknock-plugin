# Pair Agentknock with the user's phone

Read this for first-time pairing or a pairing error. Pairing belongs to the
local user and is reused across projects; it is not a per-repository setup.

## Check existing state

Run `agentknock pairing status` in the environment that will run commands.
This reads local state without contacting the phone. An active status does
not prove the phone is reachable or still accepts the pairing.

- **Active:** Continue with the task. A connection failure alone is not a
  reason to remove the pairing.
- **Pending:** Resume the existing verification conversation if its code and
  the user's approval are known. Do not create another request automatically.
- **Not paired:** Start the flow below.

Use `agentknock pairing --help` and the relevant subcommand's `--help` for
syntax and recovery operations.

## Establish a pairing

The user needs the Agentknock mobile app; refer them to
[Agentknock](https://agentknock.dev/) for current availability and installation.
Ask for the pairing address from their app if it is not already provided.
It is an address, not a password or a secret value. Do not invent an address
or use one from an example.

1. Run `agentknock pairing start ADDRESS` with the actual address. Keep the
   command's session alive while it contacts the phone.
2. Show the user the complete 12-digit verification code returned by the CLI,
   preserving leading zeros. Ask them to compare all digits with the phone
   and approve there only if they match. Do not claim to have verified what
   the user sees on their phone.
3. After the user confirms the match and phone approval, run
   `agentknock pairing finish`. Starting successfully or merely seeing a
   pending status is not evidence of that approval.
4. On successful completion, return to the original task. If secret names
   are unknown, `agentknock secret list` can discover them and exercise the
   connection without requesting secret values.

If the code does not match, have the user reject the request and run
`agentknock pairing abort`. If resuming a pending pairing without the original
verification code, explain that verification cannot be completed from status
alone and arrange to abort and restart it with the user.

## Recovery and missing secrets

Follow the CLI's error guidance. Check the execution environment and phone
connectivity before replacing a pairing. Pairing state in `~/.agentknock`
contains credentials: use CLI status and error messages for diagnosis rather
than printing that state into the conversation. Preserve the paired user's
home directory and the required private file permissions.

After an interrupted pairing operation, check status before deciding whether
to resume or restart. Use removal only when the user intends to disconnect or
replace the pairing. `pairing remove --force` removes only local state; the
phone retains its record.

Pairing does not create the secrets needed for a task. If one is missing, have
the user add it in the app. If they want to migrate an existing local secret,
use `agentknock secret upload --help` to choose an input source that reads it
directly, without exposing its contents to the agent. Prompt-based input needs
a terminal the user can actually interact with. An upload is only a proposal:
it becomes available after the user accepts it in the app. Do not delete its
local source just because the upload command completed.
