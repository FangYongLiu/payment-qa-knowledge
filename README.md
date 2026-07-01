# payment-qa-knowledge

Authoritative knowledge base for the payment system, describing how it works end to end.
It is standalone and read-shareable: read or clone it to understand the payment system and build on
it. Knowledge only — no code, no secrets.

## Start here
- `MAP.md` — landscape: the businesses, the 18 domains, transaction flow, and where to find things.
- `domains/<domain>/domain_<domain>.md` — a domain's entry point.
- `docs/GLOSSARY.md` — terminology.
- `docs/KB_ARCHITECTURE.md` — structure, naming, and contribution rules.

## Layout
- `domains/<domain>/` — the 18 business domains; each contains `service/ api/ table/<db>/ flow/
  scenario/ troubleshooting/ reference/` and a `domain_<domain>.md` entry.
- `MAP.md`, `docs/` — navigation, framework, glossary, coverage.
- `index/domains.yaml` — domain registry. `templates/` — authoring templates.

## Contributing
Every change is made through a pull request and merged only by an admin, removals included.
Direct pushes to `main` are not permitted. Rules: `docs/KB_ARCHITECTURE.md`.
