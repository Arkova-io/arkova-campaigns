# Arkova Campaigns

Private audience and marketing-campaign control for Arkova, designed to replace Mailchimp while keeping email delivery with a specialist provider.

## Decision

- Adopt [Keila](https://github.com/pentacent/keila) (AGPL-3.0) as an unmodified upstream service for the human UI, contacts, segments, templates, campaigns, scheduling, and analytics.
- Use [Amazon SES](https://aws.amazon.com/ses/) for delivery, DKIM, feedback loops, suppression, and bounce/complaint events. Arkova will not operate an SMTP/MTA fleet.
- Build an Arkova-owned REST/MCP gateway for SSO, safe filters, approvals, idempotency, audit, quotas, and a send kill switch.
- Keep the gateway as a separate process and do not couple proprietary modules into Keila.

## Agent contract

Initial tools: `contacts_upsert`, `contacts_import`, `segments_list`, `segments_create`, `segments_preview`, `templates_list`, `templates_upsert`, `templates_preview`, `campaigns_create`, `campaigns_test`, `campaigns_schedule`, and `campaigns_status`.

Agents may prepare drafts, previews, audience counts, and test sends. A production schedule/send requires a human approval token bound to the content revision, audience count, sender, and scheduled time.

## Delivery gates

- Import Mailchimp active, unsubscribed, cleaned, bounced, and complaint state; never migrate only active contacts.
- Verify SPF, DKIM, DMARC alignment, visible and one-click unsubscribe, consent provenance, postal footer, and webhook authenticity.
- Prove duplicate prevention, cancellation, restart recovery, retries, complaint/hard/soft-bounce handling, suppression reconciliation, backups, and restore.
- Treat opens as directional analytics rather than authoritative engagement.

Expected production adoption is 6–10 engineer-weeks. See [docs/product-contract.md](docs/product-contract.md).
