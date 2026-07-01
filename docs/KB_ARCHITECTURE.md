# Knowledge Base Architecture

The framework contract for this repository, binding on all contributions.

## Purpose
Cover the entire payment system so that both AI agents and people can understand it and build on it
by reading the files directly.

## Principles
- **Structure is the index.** No vector search — directories, names, and navigation files ARE how
  knowledge is found. Keep them self-describing, predictable, greppable.
- **One taxonomy: 18 business domains.** All content lives under it. No second parallel tree.
- **Navigate first, read few.** `MAP.md` → `domains/<domain>/domain_<domain>.md` → the specific
  file → follow `related_*` / `[[links]]`.
- **Facts, not inputs.** This repo is "how the system is now". Time-bound docs (PM requirements)
  are distilled into domains, not dumped in (see below).
- **Never fabricate.** Unknowns are marked `待补 (TODO)` and filled by the owner.

## Directory layout — each folder has one job
| Path | Purpose |
|---|---|
| `MAP.md` | Landscape + 18 domains + how they connect + where to find what. Read first. |
| `docs/KB_ARCHITECTURE.md` | This contract. |
| `docs/GLOSSARY.md` | Term → definition + where used. |
| `docs/COVERAGE.md` | Covered vs missing. *(planned)* |
| `domains/<domain>/domain_<domain>.md` | Domain START HERE: plain scope + index of its files. |
| `domains/<domain>/service/` | Service objects (the anchor). |
| `domains/<domain>/api/` | API objects (path / params / errors / test points). |
| `domains/<domain>/table/<db>/` | Table objects, grouped by database. |
| `domains/<domain>/flow/` | Flows as followable steps (who calls whom + DB checkpoints). |
| `domains/<domain>/scenario/` | Test scenarios (trigger → steps → DB checks → expected). |
| `domains/<domain>/troubleshooting/` | Playbooks (symptom → root cause → steps → fix). |
| `domains/<domain>/reference/` | Reference tables / dictionaries. |
| `index/domains.yaml` | Domain registry (owner / reviewer). |
| `templates/` | Object templates + authoring rules. |

A file that fits none of these purposes is not added.

## Naming
- Domain folders: `kebab-case`, matching the registry.
- File prefixes: `domain_ svc_ api_ tbl_ flow_ scn_ ts_ reference_`.
- `id` is unique and stable — renaming a file does not change it. `name` is human-readable; put
  code names / acronyms (e.g. `MPGS`) in `aliases`.
- `related_*` point to **existing** ids only; back-fill the other side when you add an object.
- Full rules: `templates/README.md`. Sample: `domains/kyc/`.

## PM requirement docs
Don't import raw — they go stale and conflict. **Distill** durable knowledge (new rules / flows /
terms / APIs / tables) into the relevant domain instead.

## How to update (people and AI, every time)
1. Find the domain via `MAP.md`.
2. Apply the `templates/` shape (frontmatter, naming, relations, back-links).
3. Edit under `domains/<domain>/…`; prefer editing over near-duplicates; distill, don't dump.
4. New content is `draft`; an admin flips it to `active` at merge.
5. **Never push to `main`** — open a Pull Request. Removals are PRs too.
6. Leave unknowns as `待补`; never invent facts.

## Governance — only admins approve
`main` is protected: every change (add / edit / remove) needs a PR **approved by an admin**
(branch protection + `.github/CODEOWNERS`). Nothing changes silently. No code, no secrets —
this repo is read-shareable.
