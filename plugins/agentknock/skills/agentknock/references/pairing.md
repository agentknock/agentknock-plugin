# Pair Agentknock with the user's phone

Establish or recover a verified pairing for the installation selected by the main
skill. A pairing belongs to its state directory, not a project. Reuse an existing
working pairing.

Use `agentknock pairing --help`, subcommand help, and CLI feedback for the pairing
flow, status, and recovery commands.

If the user lacks the mobile app, direct them to the
[official mobile installation instructions](https://github.com/agentknock/agentknock-cli#install-the-agentknock-mobile-app)
for their platform before continuing. Ask for the pairing address from their app
when needed.

Pairing normally takes two conversational turns:

1. Start pairing through the CLI and show the complete 12-digit verification code,
   preserving leading zeros. Ask the user to compare it with their phone, approve
   only if it matches, and reply so you can finish. End the turn here.
2. After the user confirms the match and phone approval, finish pairing through
   the CLI and report the result.

For an interrupted pairing, consult status and resume only when the verification
code and any required user confirmation are known. Otherwise, arrange a verified
restart with the user. Diagnose connectivity failures before replacing an active
pairing. Use CLI diagnostics rather than reading pairing credentials into the
conversation.

Normally the phone already holds the user's secrets; pairing a new client needs
no secret setup. For a new user, explain how to add secrets in the phone app.
If context suggests the user's credentials are stored on this machine—for example,
because it is their development laptop—propose migrating them to the phone. For that workflow,
read [migration.md](migration.md).
