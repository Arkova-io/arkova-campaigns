# Security disposition

## Current decision

This Keila setup is approved only for a localhost evaluation with invented contacts and the bundled Mailpit test inbox. It is not approved for internet exposure, real customer data, an external mail provider, or production sending.

## Known blocker

The pinned Keila v0.30.2 dependency installation reported multiple published security advisories during the native build, including high-severity denial-of-service findings. The JavaScript dependency audit also reported high-severity findings.

These messages come from the upstream dependency set; Arkova has not modified Keila application code. They still block production use until we:

1. upgrade or patch the affected dependencies;
2. rebuild from a reviewed and reproducible source pin;
3. rerun dependency and container-image scans;
4. test authentication, authorization, data export, backup, restore, and unsubscribe behavior; and
5. receive an explicit production approval.

## Local safeguards

- Keila and Mailpit listen only on `127.0.0.1`.
- PostgreSQL has no host port.
- Docker containers run with `no-new-privileges`.
- Registration and upstream update checks are disabled.
- Credentials live in the ignored, mode-`0600` `.env` file.
- Test mail is captured by Mailpit; no external relay is configured.
- Customer lists, customer assets, and production credentials are prohibited.

## Reporting

Do not put secrets or customer data in a GitHub issue. Report a suspected security issue privately to Arkova's technical owner, including the affected component, version, reproduction steps, and impact.
