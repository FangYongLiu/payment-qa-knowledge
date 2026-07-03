# Authoring rules (read before adding or editing an object)

This knowledge base is read **directly** — by AI agents (Claude Code CLI) and by people on GitHub.
There is no build step and no search index: **the directory structure, names, and cross-references
ARE how knowledge is found.** Author every file so that a reader who lands on it can understand it
and follow it to whatever is related.

Two rules govern everything:
1. **Write to the template.** Each object type has a `templates/<type>.md` with the required
   frontmatter and body sections. Fill every section.
2. **Add and back-link.** When you add an object, update the related objects so both sides point at
   each other (see the checklist below). An object no one links to is a leaf no reader reaches.

Anything you cannot confirm is marked **`待补` (TODO)** — never invented. A `待补` is discoverable and
gets filled later by the owner. This is the single most important rule.

---

## 1. Object types and naming
| Type | id prefix | File name | When |
|---|---|---|---|
| Domain | `domain_` | `domain_<domain>.md` | One business domain (its START HERE) |
| Service | `svc_` | `service_<app_group>_<name>.md` | One deployable service / app |
| API | `api_` | `api_<service>_<name>.md` | One interface |
| Table | `tbl_` | `table_<db>_<table>.md` | One database table |
| Scenario | `scn_` | `scn_<domain>_<name>.md` | One business test scenario |
| Flow | `flow_` | `flow_<name>.md` | One end-to-end flow |
| Troubleshooting | `ts_` | `ts_<symptom>.md` | One failure / playbook |
| AutomationAsset | `auto_` | `auto_<domain>_<name>.md` | One automation suite |
| Reference | `reference_` | `reference_<name>.md` | A lookup / dictionary / feature overview / access or how-to guide |

**Which type for which document** (business overviews, frontend/access guides, test-step guides all
have a home — do not invent new types or a separate tree):
- Test procedure (how to test X: steps → DB checks → expected) → **Scenario** (`scn_`).
- Feature/business overview, or a frontend/portal access & environment guide → **Reference** (`reference_`).
- End-to-end flow (who calls whom, state machine, checkpoints) → **Flow** (`flow_`).
- Known issue / env-setup problem → **Troubleshooting** (`ts_`). Full table: `docs/KB_ARCHITECTURE.md`.

- `id` is unique and **stable** — renaming a file never changes its `id`.
- Files live under `domains/<business-line>/<domain>/<type>/`; `table/` nests one more level by
  database: `domains/<business-line>/<domain>/table/<db>/`. `domain_<domain>.md` stays at the domain
  root as the entry point.
- **The folder is organisational only.** What binds an object to a domain is its `domain:`
  frontmatter field, which **must equal its own (leaf) folder name**; the folder above it is the
  business line.
- **Business line.** Each domain belongs to a business line, declared once as `business_line` on the
  domain in `index/domains.yaml` (`botim-core` or `botim-money`); `MAP.md` groups domains by it.
  Objects inherit the business line from their domain — do not repeat `business_line` on every
  object. A new domain is registered in `index/domains.yaml` (with its `business_line`) before its
  folder is created.

---

## 2. Frontmatter (machine-readable: identity, relations, ownership)
- `id` — unique, correct prefix.
- `name` — human-readable. Put code names / deploy names / acronyms (e.g. `MPGS`) in `aliases`.
- `domain` — required, equal to the folder name.
- `status` — `active` (approved) or `draft` (pending admin review).
- `owner` / `reviewer` — knowledge owner by business domain (see `index/domains.yaml`).
- `dev_owner` — development contact for the service (who to ask when debugging). Not the knowledge owner.
- `app_group` / `layer` — Service only.
- `related_*` — cross-references to other objects (see §3).

---

## 3. Cross-references (`related_*` and `[[links]]`)
`related_*` frontmatter lists and `[[links]]` in the body are how a reader hops from one object to
the next. They are pointers, not a database.

| Field | Meaning |
|---|---|
| `related_services` | services this object calls / belongs to |
| `related_tables` | tables it reads / writes |
| `related_scenarios` | scenarios that cover it |
| `related_failures` | known failures |
| `related_logs` | log locations (for troubleshooting) |
| `related_requirements` | requirements it affects |

Rules:
- **Point to ids that exist.** A reference to a missing object is a dead end. If the target is not
  written yet, name it in the body and mark `待补` — do not add a broken pointer.
- **Declare each relation once, from its natural source, then back-link the other side in prose.**
  Do not list the same edge on both objects' `related_*` (it drifts). A reader on either side still
  finds the other: one via `related_*`, the other via a `[[link]]` in the body.
- There is **no `related_apis` field** — a service↔API link is declared by the API's
  `related_services`; the service names its APIs with `[[api_…]]` in the body.

### Who declares what
| Object | Declares in `related_*` |
|---|---|
| Service | services (downstream) / tables / scenarios |
| API | services (owning) / tables / scenarios |
| Table | services (owning) / scenarios |
| Scenario | services / tables / logs |
| Flow | services / tables / scenarios |
| Troubleshooting | services / tables / logs / failures |
| Domain | services (the key ones) |
| AutomationAsset | scenarios / services |

---

## 4. Add-and-back-link checklist
After adding an object, update the related files (both the `related_*` field and body `[[links]]`):

- **Service** → add `[[svc_x]]` to `domain_<domain>.md` and its `related_services`; callers declare it in their `related_services`.
- **API** → add `[[api_x]]` to the owning `service_*.md` body; set `api_x.related_services = [svc]`; add `related_tables` / `related_scenarios` if known.
- **Table** → add `[[tbl_x]]` to the owning `service_*.md` body; every service/API that reads it adds `tbl_x` to its `related_tables`.
- **Scenario** → set `scn_x.related_services` / `related_tables`; each covered `api_*.md` adds `scn_x` to `related_scenarios` + `[[scn_x]]` in body; the covering `auto_*.md` adds `scn_x`.
- **AutomationAsset** → set `auto_x.related_scenarios` / `related_services`; each covered `scn_*.md` and each exercised `api_*.md` gets `[[auto_x]]` in body; add `[[auto_x]]` to the owning service/domain.
- **Domain** → `related_services` = the domain's key services; list key services / flows / automation in the body index.

> Rule of thumb: for any A→B relation, **both A and B must be able to see each other** — one via a
> `related_*` field, the other via a `[[link]]` in prose.

---

## 5. Enriching a domain (repeatable playbook)
Work by **data source**, one pass at a time; fill what each source gives and mark the rest `待补`.
Every pass follows §2–§4 (template + relations + back-links). Sample domain: `domains/botim-money/activation/`.

1. **Skeleton and domain assignment** — create/assign the service objects; `dev_owner` = `Given.Surname`,
   `owner` = domain lead (`index/domains.yaml`); file under `domains/<business-line>/<domain>/`, `domain` field = leaf folder.
2. **Call graph (upstream/downstream)** — from real call traces, add `related_services` edges with
   frequency. Downstream = what this service calls; upstream = who calls it.
3. **Tables** — from the database **schema DDL**, build `table_<db>_<table>` (columns / types / PK /
   indexes / comments come from the DDL; purpose / check-points are authored), then back-fill each
   caller's `related_tables`. **Do not invent tables the DDL does not define.**
4. **Known issues (Troubleshooting)** — from real error logs, write `ts_` playbooks. Separate
   business errors from infrastructure noise; do not file expected behaviour as an issue.
5. **Key operations** — from real info logs, record the business methods / entry APIs a service runs;
   drop infrastructure classes.
6. **Scenarios / automation** — read the automation suites; **merge** cases into scenarios by business
   flow (not 1:1); one `AutomationAsset` per suite; connect `related_services` for every service crossed.
7. **End-to-end flows** — capture cross-system sequences, state machines, and rendering rules as `flow_`.
8. **Unknowns** — anything uncertain (missing tables, failure branches, downstream objects) stays `待补`.

---

## 6. Before you commit
- Every new file: complete frontmatter and complete body sections (per `templates/<type>.md`).
- `related_*` point only to existing ids — **zero dead pointers** (grep each id).
- **Zero duplicate ids** (`grep -rh '^id:' domains/ | sort | uniq -d`).
- Valid frontmatter YAML: `status` ∈ {active, draft}; `object_type` is one of the nine types;
  `tags` are all strings (quote bare numbers, e.g. `'707'`); `related_*` use one YAML list style,
  not mixed.
- Back-link checklist (§4) done — the new object is reachable from related files.
- Every unknown marked `待补`; nothing invented.
- **Open a Pull Request** — never push to `main`; an admin approves and flips `draft` → `active`.
