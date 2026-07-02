# qa-knowledge-base

The Astra QA team's shared knowledge base: how the systems we test work, end to end.
It is read directly — by AI agents (Claude Code CLI) and by people on GitHub — and read-shareable
across the team. Knowledge only: no code, no secrets.

Content is organised in two levels: **business line** (`business_line`) → **business domain**. Two
business lines: **botim-core** (the Botim app — IM, VoIP, Ads, Mini Program) and **botim-money**
(payment / fintech, the PayBy platform). botim-money is fully populated; botim-core is a skeleton for
its teams to fill.

## Start here
- `MAP.md` — landscape: business lines, their domains, key flows, and where to find things.
- `domains/<business-line>/<domain>/domain_<domain>.md` — a domain's entry point.
- `docs/GLOSSARY.md` — terminology.
- `docs/KB_ARCHITECTURE.md` — structure, naming, and contribution rules.

## Layout
- `domains/<business-line>/<domain>/` — one folder per business domain (registered in
  `index/domains.yaml`, grouped by `business_line`); each contains `service/ api/ table/<db>/ flow/
  scenario/ troubleshooting/ reference/` and a `domain_<domain>.md` entry.
- `MAP.md`, `docs/` — navigation, framework, glossary, coverage.
- `index/domains.yaml` — domain registry (business_line / owner / dev_owner). `templates/` — authoring templates.

## Contributing
Every change — additions, edits, removals — goes through a pull request, merged only by an admin.
See `CONTRIBUTING.md`.
