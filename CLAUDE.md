# CLAUDE.md

Guidance for AI agents reading and contributing to this repository.

## Navigation
Read `MAP.md` to select a domain, open `domains/<domain>/domain_<domain>.md` for its index, then
open only the relevant files. Follow `related_*` and `[[links]]`. Resolve terms via
`docs/GLOSSARY.md`. Grep by the stable prefixes (`svc_ api_ tbl_ flow_ scn_ ts_`) and `aliases`.
Do not load the entire repository.

## Authoring
- One taxonomy: product line → business domain, under `domains/<domain>/` (current set in `MAP.md`; each domain declares a `product`). New content lands in an existing domain; a new domain is registered in `index/domains.yaml` with its `product` first.
- Each typed object is one markdown file with frontmatter, per `templates/README.md`.
- `name` is human-readable; code names and acronyms go in `aliases`.
- `related_*` reference existing ids only; back-fill the other side when adding an object.
- New content is `draft`; an admin sets it `active` at merge.
- Renaming a file does not change its `id`.
- Unknown values are marked `待补`; nothing is invented.
- PM requirement documents are distilled into domains, not imported raw.

## Governance
Never push to `main`. Every change — additions, edits, and removals — is a pull request approved by
an admin. No code, no secrets.
