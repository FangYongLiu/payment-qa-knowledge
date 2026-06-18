# payment-qa-knowledge

The Payment QA team's **canonical knowledge repository** — the single source of truth.
It stores **reviewed** markdown/yaml knowledge only; **no code** (code lives in the
engine repo `payment-qa-brain`).

The knowledge engine (`payment-qa-brain`) derives its runtime index
(PostgreSQL + pgvector) from this repo; merging a PR triggers a reindex.

## Two-layer knowledge model
- **Base · LLM-Wiki pages (`wiki/`)** — every source document becomes one linked
  markdown page with light frontmatter (`domain` + `tags` + `[[links]]`). Flexible and
  readable; holds any kind of document (business overviews, specs, notes).
- **Upper · Typed objects (`domains/`)** — for **technical content only**, the engine
  additionally extracts the 8 typed objects + relations into the graph (powering
  requirement-impact analysis and test-case generation). Business overviews stay as
  wiki pages.

> Do **not** force every document into the 8 types — that was the v1 mistake. Let
> business-level content live as wiki pages; reserve typed objects for technical content.

## Layout
- `wiki/<domain>/<slug>.md` — LLM-Wiki base pages (one per source document)
- `domains/<domain>/<subdomain?>/<file>.md` — typed knowledge objects (subdomain is
  optional; when absent the file sits directly under the domain — no placeholder dir)
- `templates/` — templates for the 8 object types (copy one to author a new object)
- `index/` — per-type routing index (id / name / aliases / domain / status / path)

> Physical layout is for humans; retrieval relies on `index/` + metadata + vectors,
> not on the directory structure.

## Knowledge objects (8 types)
Domain / Service / API / Table / Flow / Scenario / Troubleshooting / AutomationAsset.
Each typed object = one markdown file + frontmatter metadata. Metadata spec: see
CONTRIBUTING.md.

## How to contribute
**Preferred:** the workbench / knowledge-engine update-request workflow
(named submission → review → the engine opens the PR). Approval in the review UI is the
**human gate**; the engine then auto-opens and auto-merges its own PR (Plan B), and the
merge triggers a reindex. Direct edits to this repo also go through a PR + review.
See CONTRIBUTING.md.

## Validation
Before committing / in CI, run `python scripts/check_knowledge.py` (in the engine repo)
to ensure `related_*` and eval references contain no dangling ids.
