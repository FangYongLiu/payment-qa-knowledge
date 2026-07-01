# CLAUDE.md — payment-qa-knowledge (knowledge content repo)

> Knowledge content only — **no code, no secrets**. This is the single source of truth for the
> company's payment system, read directly by AI and people. Read `MAP.md` first, then
> `docs/KB_ARCHITECTURE.md` (the framework contract).

## Navigate (read efficiently — you only have read/grep/glob, no vector search)
1. `MAP.md` → pick the domain. 2. `domains/<domain>/domain_<domain>.md` → its index; open only
relevant files. 3. Follow `related_*` / `[[links]]`. 4. Resolve terms via `docs/GLOSSARY.md`.
5. Grep with stable prefixes (`svc_ api_ tbl_ flow_ scn_ ts_`) and `aliases` (code names/acronyms).
**Do not load the whole repo.**

## Rules for adding/updating knowledge
- One taxonomy: **18 business domains** (`domains/<domain>/`). New content lands in an existing
  domain. Keep business overviews as narrative; extract typed objects only for technical content —
  don't force every doc into the 8 types.
- Each typed object = one markdown + frontmatter. Follow `templates/README.md` (naming, frontmatter,
  relations section, back-linking). `name` is human-readable; put code names/acronyms in `aliases`.
- `related_*` must point to **existing** ids (no dangling). When adding an object, back-fill the
  related objects' links.
- New content is `draft`; only an admin review flips it to `active` at merge.
- Renaming a file does **not** change its id.
- **Never fabricate.** Unknown values → `待补 (TODO)` / `DDL未定义`.
- PM requirement docs: **distill** durable knowledge into domains; don't dump raw (see
  `docs/KB_ARCHITECTURE.md` §5).

## Governance (important)
- **Never push to `main`.** Every change (add / edit / remove) → a **Pull Request**.
- **Only admins approve/merge** (branch protection + `.github/CODEOWNERS`). Explain what changed
  and why in the PR body. Deletions need the same approval — nothing is silent.
- Before submitting, run `scripts/check_knowledge.py` (in `payment-qa-brain`) to catch dangling ids.
