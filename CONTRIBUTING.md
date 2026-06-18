# Knowledge Contribution & Review Guide

For all QA members. Goal: knowledge that is trustworthy, traceable, and governable.

## 1. Two-layer model — where content goes
- **Business overviews / mixed documents** → an LLM-Wiki page under `wiki/<domain>/`
  (the engine usually authors these from ingested sources).
- **Technical content** (APIs, tables, scenarios, troubleshooting, automation) → typed
  objects under `domains/<domain>/<subdomain?>/`, plus a routing entry in `index/`.

## 2. Authoring a typed object
1. Copy the matching template from `templates/` to `domains/<domain>/<subdomain?>/`
   (omit the subdomain dir when there is no subdomain).
2. Follow the id convention: `api_<service>_<name>` / `svc_<name>` /
   `tbl_<schema>_<table>` / `scn_<name>` / `ts_<symptom>` / `auto_<name>` /
   `flow_<name>` / `domain_<slug>`.
3. Fill the frontmatter (required fields must be present); list related object ids in
   `related_*`.
4. Add a routing entry in `index/<type>.yaml` (id / name / aliases / domain / status / path).

## 3. Metadata spec
- **Required**: id, object_type, domain, status, owner, reviewer, last_reviewed_at,
  source_type, source_ref, tags.
- **Optional**: subdomain, module, name, aliases, related_services, related_tables,
  related_scenarios, related_logs, related_requirements, related_failures.
  Leave subdomain/module `null` when there is no good value.
- `status`: draft (new) → active (review passed) → deprecated / archived.
- `name` must be human-readable; put code-like names in `aliases`. `name` + `aliases`
  decide whether Chinese/English phrasings hit in retrieval — fill them generously
  (e.g. "DCC" / "DCC qualification" / "dcc 资质").

## 4. related_* rules
- Only reference object ids that **actually exist** — no dangling refs.
- State **known** relations (API→Service/Table/Scenario/Log). Inferred relations
  (failure→root_cause, etc.) are produced by the engine during curation and enter the
  graph after human review.

## 5. Review
- Named submission; reviewed by the domain's Owner / Reviewer.
- Reviewers check: factual correctness, metadata completeness, correct `related_*`,
  sensible status.
- Approval is the **human gate** (Plan B): the engine then auto-opens + auto-merges its
  PR and reindexes. Only `active` knowledge serves production answers.

## 6. Pre-submit check
- Run `scripts/check_knowledge.py` (in the engine repo): no dangling ids in `related_*`
  or in the eval's `expected_object_ids`.
- One object per file; all changes via PR.
