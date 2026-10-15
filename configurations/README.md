# Device configuration exports

The exact saved configurations were not uploaded with the request, so this package does **not** claim to contain complete device backups.

## Add exports

Export the saved configuration from PMN-OS for each device and add files such as:

- `R2.cfg`
- `R3.cfg`
- `R4.cfg`
- `R5-ISP.cfg`
- `DSW1.cfg`
- `DSW2.cfg`
- `SW2.cfg`

Before committing, inspect the files for:

- `enable secret`, local user passwords, TACACS/RADIUS secrets
- SNMP communities or authentication/privacy secrets
- VPN pre-shared keys, private keys, API tokens
- real customer/site details or public IPs that should not be disclosed

Use placeholders such as `<REDACTED>` in public examples. Do not include any credential that is still valid.

The `reconstructed-snippets/` directory contains selected configuration fragments inferred from command history. They are reference notes, not a complete or guaranteed deployable configuration. Verify syntax and current state in PMN-OS before use.
