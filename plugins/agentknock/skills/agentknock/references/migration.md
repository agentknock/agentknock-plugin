# Upload or migrate secrets to the phone

Read this when the user wants to upload local secret data or migrate existing
credentials to the phone. Use the executable and state directory resolved through the
main skill's installation lookup. If pairing is needed, follow
[pairing.md](pairing.md) first.

New secrets are normally created in the mobile app. For local sources, use
`agentknock secret upload --help` to select an input method that lets the CLI
read the value directly. Do not print a credential, read it into the conversation,
or put its literal value in command arguments to construct the upload.

Choose the source that already holds the data: process environment, a dotenv
file, a value file, or an OpenSSH private-key file. Prompt-based input requires
a terminal the user can actually interact with; an agent-only terminal does
not make a secret-entry prompt usable. Encrypted SSH keys also require a
passphrase source. Consult help for source combinations and format requirements
rather than transforming or decrypting key material through the conversation.

Match the upload mode to the user's intent. Creating a secret, updating selected
values, and replacing an entire secret have different effects. In particular,
replacement removes omitted content when accepted. Confirm the existing secret's
identity from metadata when necessary; do not infer it from an example name.

Keep the upload session alive while it waits for the device. Successful upload
means the phone received the proposal, not that the secret is ready to use.
The user must review and accept it in the app. A newly created secret may be
renamed during acceptance, so discover its accepted name if needed.

After acceptance, verify metadata and exercise the intended operation through
Agentknock without exposing the value. Removing local credentials is a separate
migration step: check that the replacement works and that the user intends the
cleanup before deleting source files or changing other tools' configuration.
An upload by itself neither deletes local copies nor migrates their consumers.
