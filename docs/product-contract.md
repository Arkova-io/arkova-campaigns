# Product contract

## Outcome

An authorized person or agent can manage consent-aware contacts and segments, prepare and test an on-brand campaign, obtain approval, schedule it, and inspect delivery health without Mailchimp.

## Architecture boundary

Codex, Claude, and Arkova services call the Arkova gateway. The gateway applies policy and calls Keila's API. Keila owns campaign workflow and PostgreSQL-backed jobs. SES owns internet mail transport and reputation primitives.

## Acceptance criteria

- Contact CRUD/import/export with normalized addresses, attributes, consent source/timestamp, and global suppression.
- Saved allow-listed segments with audience preview and exact count.
- HTML/MJML/Markdown template preview, plain-text part, test send, schedule, status, and immutable approval snapshot.
- Immediate complaint/hard-bounce suppression and a tested soft-bounce policy.
- One-click unsubscribe, preference page, double opt-in, audit log, scoped tokens, rate/volume caps, health alerts, backup, and restore.
- No production send without a valid human approval token matching the exact revision and audience.

## Explicit non-goals

Self-hosted MTA, CRM integrations, journeys, SMS/push, multi-tenancy, lead scoring, A/B testing, custom landing pages, and a bespoke drag-and-drop editor.
