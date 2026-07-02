# Knowledge Base Architecture

The framework contract for this repository, binding on all contributions.

## Purpose
Cover the systems the Astra QA team tests so that both AI agents and people can understand them and
build on them by reading the files directly.

## Principles
- **Structure is the index.** No vector search — directories, names, and navigation files ARE how
  knowledge is found. Keep them self-describing, predictable, greppable.
- **Two levels: business line → business domain.** Every domain belongs to a `business_line`
  (`botim-core` for the Botim app, `botim-money` for payment/fintech) and lives at
  `domains/<business-line>/<domain>/`. The current set is listed in `MAP.md` and
  `index/domains.yaml` and may be revised through governance; there is never a second parallel tree.
- **Navigate first, read few.** `MAP.md` → `domains/<business-line>/<domain>/domain_<domain>.md` → the specific
  file → follow `related_*` / `[[links]]`.
- **Facts, not inputs.** This repo is "how the systems are now". Time-bound docs (PM requirements)
  are distilled into domains, not dumped in (see below).
- **Never fabricate.** Unknowns are marked `待补 (TODO)` and filled by the owner.

## Directory layout — each folder has one job
| Path | Purpose |
|---|---|
| `MAP.md` | Landscape + domains + how they connect + where to find what. Read first. |
| `docs/KB_ARCHITECTURE.md` | This contract. |
| `docs/GLOSSARY.md` | Term → definition + where used. |
| `docs/COVERAGE.md` | Covered vs missing. *(planned)* |
| `docs/CONTRIBUTING_BOTIM.md` | Botim team (`botim-core`) onboarding. |
| `domains/<business-line>/` | One folder per business line (`botim-core`, `botim-money`). |
| `domains/<business-line>/<domain>/` | One folder per business domain (current set in `MAP.md`). |
| `domains/<business-line>/<domain>/domain_<domain>.md` | Domain START HERE: plain scope + index of its files. |
| `domains/<business-line>/<domain>/service/` | Service objects (the anchor). |
| `domains/<business-line>/<domain>/api/` | API objects (path / params / errors / test points). |
| `domains/<business-line>/<domain>/table/<db>/` | Table objects, grouped by database. |
| `domains/<business-line>/<domain>/flow/` | Flows as followable steps (who calls whom + DB checkpoints). |
| `domains/<business-line>/<domain>/scenario/` | Test scenarios (trigger → steps → DB checks → expected). |
| `domains/<business-line>/<domain>/troubleshooting/` | Playbooks (symptom → root cause → steps → fix). |
| `domains/<business-line>/<domain>/reference/` | Reference tables / dictionaries. |
| `index/domains.yaml` | Domain registry (business_line / owner / reviewer / dev_owner). |
| `templates/` | Object templates + authoring rules. |

A file that fits none of these purposes is not added.

## Naming
- Domain folders: `kebab-case`, matching the registry, nested under their business line
  (`domains/<business-line>/<domain>/`). A new domain is registered in `index/domains.yaml` with its
  `business_line` before its folder is added.
- File prefixes: `domain_ svc_ api_ tbl_ flow_ scn_ ts_ auto_ reference_`.
- `id` is unique and stable — renaming a file does not change it. `name` is human-readable; put
  code names / acronyms (e.g. `MPGS`) in `aliases`.
- `related_*` point to **existing** ids only; back-fill the other side when you add an object.
- Full rules: `templates/README.md`. Sample: `domains/botim-money/activation/`.

## PM requirement docs
Don't import raw — they go stale and conflict. **Distill** durable knowledge (new rules / flows /
terms / APIs / tables) into the relevant domain instead.

## How to update (people and AI, every time)
1. Find the domain via `MAP.md`.
2. Apply the `templates/` shape (frontmatter, naming, relations, back-links).
3. Edit under `domains/<business-line>/<domain>/…`; prefer editing over near-duplicates; distill, don't dump.
4. New content is `draft`; an admin flips it to `active` at merge.
5. **Never push to `main`** — open a Pull Request. Removals are PRs too.
6. Leave unknowns as `待补`; never invent facts.

## Governance — only admins approve
`main` is protected: every change (add / edit / remove) needs a PR **approved by an admin**
(branch protection + `.github/CODEOWNERS`). Nothing changes silently. No code, no secrets —
this repo is read-shareable.
