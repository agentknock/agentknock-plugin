# Upload or migrate secrets to the phone

Transfer the user's selected credentials to their phone using a method that
clearly avoids printing secret values or saving additional copies along the way.
New secrets are normally created in the mobile app.

Use `agentknock secret upload --help` for transfer methods and the effects of
creating, updating, or replacing a secret. Choose the mode that matches the user's
intent and use metadata to identify existing secrets.

The CLI finishes when the phone receives the upload. Ask the user to review and
accept it in the app; the secret becomes usable only after acceptance. The CLI
does not wait for this decision. The user can rename a new secret when accepting
it, so check metadata for its final name when needed.

Even if an upload fails or is interrupted, the phone may still receive it. Check
with the user before retrying to avoid duplicate uploads.

## Switch existing tools to Agentknock

Propose temporarily disabling access to the local credential, for example by
removing its key from the SSH agent or setting its file permissions to `000`.
Keep enough information to restore the previous setup. Test the intended tools
through Agentknock with local fallback disabled to establish that they use the
phone's secret. Restore local access if the migration fails.

Delete the original credentials only after Agentknock is established as the
primary source, the user wants the local copies removed, and any required
backups have been made.
