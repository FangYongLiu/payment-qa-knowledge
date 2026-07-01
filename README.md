# qa-knowledge-base

The Astra QA team's shared knowledge base: how the systems we test work, end to end.
It is read directly — by AI agents (Claude Code CLI) and by people on GitHub — and read-shareable
across the team. Knowledge only: no code, no secrets.

Content is organised by **product line** (`product`), and within each product line by **business
domain**. **Payment** is the first fully populated product line; other product lines (e.g. the Botim
app) are added by their teams under the same framework.

## Start here
- `MAP.md` — landscape: product lines, their domains, key flows, and where to find things.
- `domains/<domain>/domain_<domain>.md` — a domain's entry point.
- `docs/GLOSSARY.md` — terminology.
- `docs/KB_ARCHITECTURE.md` — structure, naming, and contribution rules.

## Layout
- `domains/<domain>/` — one folder per business domain (registered in `index/domains.yaml`, grouped
  by `product` in `MAP.md`); each contains `service/ api/ table/<db>/ flow/ scenario/
  troubleshooting/ reference/` and a `domain_<domain>.md` entry.
- `MAP.md`, `docs/` — navigation, framework, glossary, coverage.
- `index/domains.yaml` — domain registry (product / owner / dev_owner). `templates/` — authoring templates.

## Contributing
Every change — additions, edits, removals — goes through a pull request, merged only by an admin.
See `CONTRIBUTING.md`.
