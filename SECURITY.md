# Security

## Supported revision

Security fixes are published on `master`. Include the installed plugin's Git
commit or installation date when known, and whether the issue also occurs with
the current `master` revision.

## Report a vulnerability

Do not report a suspected vulnerability in a public issue, discussion, or pull
request.

For the Agentknock skill, plugins, or marketplaces, email
[security@fulldisclosure.fi](mailto:security@fulldisclosure.fi). Full Disclosure
operates Agentknock and receives reports sent to that address.

For vulnerabilities confined to another component, use its private reporting
channel:

- [Agentknock CLI](https://github.com/agentknock/agentknock-cli/security/advisories/new).
- [Agentknock for Android](https://github.com/agentknock/agentknock-android/security/advisories/new).

For the service, website, protocol, multiple components, or an uncertain
component, use the email address above. Send one report for a vulnerability
affecting multiple components.

Include the following information when available:

- The affected component and revision or version.
- The agent host, model, and execution environment.
- A description of the vulnerability and its security impact.
- The conditions and steps required to reproduce it.
- A minimal proof of concept, relevant logs, or both.
- A possible mitigation or fix.

Do not send credentials, pairing data, or personal data from a live system.
Use test data, and remove sensitive information from logs and screenshots.

## Test safely

Test only accounts, devices, systems, and data that you own or have permission
to use. Do not disrupt the service, degrade its availability, or access another
person's data. If you encounter another person's data, stop testing and report
the vulnerability.

## Coordinate disclosure

Give the maintainers reasonable time to investigate and fix a vulnerability
before disclosing it publicly. The maintainers will coordinate disclosure
with you and credit your contribution unless you ask to remain anonymous.
