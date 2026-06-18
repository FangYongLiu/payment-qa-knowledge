# CLAUDE.md — payment-qa-knowledge (knowledge content repo)

> This repo holds **reviewed knowledge content only — no code**. It is the single
> source of truth for the knowledge engine (`payment-qa-brain`).

## Rules
- Only add/edit markdown knowledge (wiki pages + typed objects) and `index/` routing —
  never application code.
- **Two-layer model**: every source becomes a `wiki/` page; **technical content
  additionally** gets typed objects under `domains/`. Don't force every document into
  the 8 types.
- Each typed object = one markdown + frontmatter; follow the metadata & naming rules in
  CONTRIBUTING.md. `name` must be human-readable (put code-like names in `aliases`).
- `related_*` must point at object ids that actually exist — no dangling refs. When you
  add a typed object, also add its routing entry in `index/<type>.yaml`.
- `status` defaults to `draft`; only a passed human review flips it to `active`. Only
  `active` knowledge serves production answers.
- All changes go through a PR. Approval (in the workbench review UI) is the human gate;
  the engine auto-opens + auto-merges its own PR (Plan B) and reindexes on merge.

## Reference
- README.md — repo structure & two-layer model
- CONTRIBUTING.md — authoring / review / metadata spec
- templates/ — the 8 object-type templates
