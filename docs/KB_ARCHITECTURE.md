# Knowledge Base Architecture (KB_ARCHITECTURE)

> The **framework contract** for `payment-qa-knowledge`. Read this before adding or
> reorganizing knowledge. AI agents (Claude Code CLI / brain / any model) also read this
> to learn how to navigate and how to contribute correctly.
>
> Language: **English-first**; a little Chinese is fine where it helps readers
> (业务术语 / short hints). Keep meta-docs mostly English so any model reads them well.

## 0. Who this is for & why

**Primary readers (co-equal):**
1. **AI** — when anyone talks to Claude Code CLI, the agent reads this repo (`read/grep/glob`)
   to answer how the payment system works and to do requirement analysis, test-case writing,
   and automation coding.
2. **People** — QA newcomers, and colleagues granted read access, who browse the repo to
   understand the whole payment system.

**One-line goal:** cover the **entire payment system**; make it **newcomer-followable** and
**precise + efficient for AI to read**.

## 1. Core principles

- **Structure IS the index (built for direct reading).** Claude Code CLI has no vector search —
  only `read/grep/glob`. So **directories, naming, and navigation files ARE the retrieval
  interface**: they must be self-describing, predictable, greppable.
- **One taxonomy: 18 business domains.** All content (narrative + typed objects) lives under the
  same 18-domain vocabulary. No second parallel tree.
- **Navigate first, read few.** Fixed path for humans/AI: `MAP.md` (landscape) → `domains/<domain>/
  domain_<domain>.md` (that domain's index) → drill into specific files → follow `related_*` /
  `[[links]]`. A few precise reads, not a full load.
- **Facts vs inputs.** This repo is the **authoritative "how the system is now"**. Time-bound
  inputs (PM requirement docs) are **not** dumped in — only distilled into durable domain
  knowledge (see §5).
- **Never fabricate (不臆造).** Unknown definitions / fields / rules are marked `待补 (TODO)` and
  filled by the domain owner — never invented.

## 2. Directory layout — every folder has ONE job

| Path | Purpose (what goes here) | What does NOT go here |
|---|---|---|
| `README.md` | Entry point: what this repo is + reading protocol (start at `MAP.md`) | Detailed knowledge |
| `MAP.md` | **Landscape**: system overview, 18 domains (one line each), how they connect, where to find what | Per-object detail |
| `CLAUDE.md` | AI contract: navigation + contribution rules for agents | Human onboarding prose |
| `docs/KB_ARCHITECTURE.md` | This file — the framework contract | Knowledge content |
| `docs/GLOSSARY.md` | Term → definition + where used (MPGS, Xtran, …) | Full flows/specs |
| `docs/COVERAGE.md` | Coverage tracker: payment-system areas × covered / partial / missing | Knowledge content |
| `domains/<domain>/domain_<domain>.md` | **START HERE for the domain**: plain-language scope + a table-of-contents of the domain's files + links to adjacent domains | Deep object detail |
| `domains/<domain>/service/` | Service objects (services are the anchor) | Non-technical narrative |
| `domains/<domain>/api/` | API objects (path/params/errors/test points) | — |
| `domains/<domain>/table/<db>/` | Table objects, grouped by database | Fabricated columns (mark `DDL未定义`) |
| `domains/<domain>/flow/` | Cross-system flows as **followable steps** (who calls whom + DB checkpoints) | — |
| `domains/<domain>/scenario/` | Test scenarios (trigger → steps → DB checks → expected) | — |
| `domains/<domain>/troubleshooting/` | Playbooks (symptom → root cause → steps → fix) | — |
| `domains/<domain>/reference/` | Reference tables / dictionaries | — |
| `domains/<domain>/narrative/` | Narrative overviews (converged wiki content, co-located) — *planned* | Typed-object content |
| `requirements/` | *(planned, optional)* dated PM-requirement archive, clearly marked "input, not source of truth", isolated from `domains/` | Anything treated as current fact |
| `index/domains.yaml` | Domain registry (owner / reviewer — authoritative) | — |
| `templates/` | Writing templates + rules for the 8 object types (read `templates/README.md`) | — |
| `bimo-confirmed/` | Knowledge confirmed in BimoQA chats and published, bucketed by source | Domain-owned content |

> If a new file doesn't fit one of these jobs, it probably shouldn't be added — ask first.

## 3. The 18 business domains

See `MAP.md` (landscape + one-liner each) and `index/domains.yaml` (owner/reviewer). New content
MUST land in an existing domain. A genuinely new domain requires editing `index/domains.yaml` and
registering it in `MAP.md`.

## 4. Naming & authoring conventions (so AI can grep precisely)

- Domain folders: `kebab-case`, matching the registry (e.g. `online-business`).
- File prefixes: `domain_ / svc_ / api_ / tbl_ / flow_ / scn_ / ts_ / auto_ / reference_`.
- `id` is unique and stable; **renaming a file does not change its id**. `name` is human-readable;
  code names / acronyms (e.g. `MPGS`, `acquireii`) go in `aliases` so grep finds them.
- `related_*` must point to **existing** ids (no dangling); when adding an object, back-fill the
  related objects' links. Full rules: `templates/README.md`. Fully-linked sample: `domains/kyc/`.

## 5. PM requirement docs

- **Do not import raw.** Requirements are time-bound, go stale, and can conflict — importing them
  pollutes "current state".
- **Distill into domains:** extract durable knowledge (new rules / flows / terms / APIs / tables)
  and update the relevant `domains/<domain>/`.
- To keep history for requirement analysis: put it under `requirements/` (dated, labeled "input,
  not source of truth"), physically separate from `domains/`.

## 6. How to update knowledge (humans AND AI — follow this every time)

1. **Find the right domain** via `MAP.md`. If unsure which domain, ask / note it in the PR.
2. **Follow the template** for the object type (`templates/README.md`): frontmatter, naming,
   "关联关系 / relations" section, back-linking.
3. **Add or edit** files under `domains/<domain>/…`. Prefer editing an existing object over
   creating a near-duplicate. Distill, don't dump (§5).
4. **New content status = `draft`**; only an admin review flips it to `active` at merge.
5. **Never push to `main`.** Create a branch → open a **Pull Request**.
6. **Removing / deprecating** knowledge is a PR too, and needs the same admin approval — deletions
   are never silent.
7. Merge triggers a brain **reindex**. Before submitting, run `scripts/check_knowledge.py`
   (in `payment-qa-brain`) to catch dangling `related_*` ids.

### AI contribution protocol (short form for agents)
> When asked to add/update knowledge: locate the domain via `MAP.md` → apply the matching
> `templates/` shape → write/edit under `domains/<domain>/` with valid frontmatter + back-links →
> mark `draft` → propose it as a branch + PR (do **not** commit to `main`). Explain what you
> changed and why in the PR body. Leave unknowns as `待补 (TODO)`; never invent facts.

## 7. Governance — only admins approve changes

- `main` is **protected**: no direct pushes; every change lands via **Pull Request**.
- **Only admins can approve/merge** — both **adding new knowledge** and **removing/changing old
  knowledge**. Approval is enforced by GitHub branch protection + `CODEOWNERS`
  (`.github/CODEOWNERS`). Contributors open PRs; admins review and merge.
- Admins keep the merge history as the audit trail; nothing is changed or deleted silently.
- **Repo hygiene (all contributors):** no application code, no secrets / real card numbers /
  internal hostnames / traceCodes. This repo is read-shareable — keep it clean.

> Admin setup (one-time, by repo owner): enable branch protection on `main`
> (require PR, require review from Code Owners, no direct push), and list admins in
> `.github/CODEOWNERS`.
