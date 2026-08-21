# Agent instructions

- This repository is isolated from Arkova's customer application. Do not import source from or write into the main application repository.
- Keep the REST contract canonical; MCP tools must be narrow, typed adapters with no arbitrary upstream-call or code-execution escape hatch.
- Never commit credentials, customer assets, meeting data, contact lists, or production exports.
- Pin and inventory third-party code and assets. Preserve required MIT, Apache, MPL, AGPL, font, and media notices.
- Production-impacting actions require explicit human approval, immutable audit events, idempotency, and a tested rollback or kill switch.
- Work on feature branches and use draft pull requests until the acceptance criteria are met.
