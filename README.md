# Arkova Campaigns

A lightweight, isolated pilot of [Keila](https://github.com/pentacent/keila) for newsletters and contact lists.

## What this pilot does

- Runs the unmodified Keila Community application on this Mac.
- Stores contacts, templates, and campaigns in a private PostgreSQL database.
- Captures every test email in Mailpit instead of sending it to the internet.
- Binds both web interfaces to `127.0.0.1`, so they are available only on this Mac.
- Keeps all generated passwords in an ignored local `.env` file.

This is intentionally smaller than the future production contract. There is no Arkova gateway, SES connection, DNS change, customer-list migration, or production-send capability in this phase.

## Start the pilot

```bash
./scripts/pilot-up
```

The first run downloads two pinned support containers, fetches Keila's exact v0.30.2 source commit, builds it natively for this Mac, and creates local credentials. The initial build can take several minutes; later starts reuse it.

- Keila: <http://127.0.0.1:4000>
- Test mailbox: <http://127.0.0.1:8025>
- Login email: `admin@arkova.local`
- Login password: stored as `KEILA_PASSWORD` in `.env`

To display the local password:

```bash
grep '^KEILA_PASSWORD=' .env
```

## Create the safe test sender

After signing in to Keila:

1. Create a project named `Arkova Test`.
2. Open **Manage Senders**, then create an **SMTP** sender.
3. Use `mailpit` as the server and `1025` as the port.
4. Use `keila` as the username.
5. Use the value of `MAILPIT_PASSWORD` from `.env` as the password.
6. Disable SSL and STARTTLS for this local-only connection.
7. Use `Arkova Test <newsletter@arkova.local>` as the sender identity.

Every message will appear in Mailpit. No external relay is configured, so the pilot does not deliver those messages to real recipients.

## Operate the pilot

```bash
./scripts/pilot-status
./scripts/pilot-down
```

`pilot-down` stops the services but preserves the database and uploaded assets. The named Docker volumes are not deleted.

## Production boundary

Do not import a customer list or connect an internet mail provider during this pilot. Production use requires a separate approval covering at least:

- Mailchimp consent, unsubscribe, bounce, and complaint-state migration;
- an SES sender and verified Arkova domain with SPF, DKIM, and DMARC alignment;
- visible and one-click unsubscribe behavior;
- backups and a tested restore;
- bounce and complaint handling;
- a human-approved first production audience.

The longer-term acceptance contract remains in [docs/product-contract.md](docs/product-contract.md), but it is not the scope of this quick replacement test.

The current security disposition and production blockers are recorded in [SECURITY.md](SECURITY.md).

## Third-party software

Versions, image digests, licenses, and sources are recorded in [THIRD_PARTY.md](THIRD_PARTY.md).
