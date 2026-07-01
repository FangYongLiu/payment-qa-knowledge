# payment-qa-knowledge

The Payment QA team's **authoritative knowledge base** — the single source of truth for how the
company's **payment system** works. Independently maintained; read-shareable to colleagues who need
to understand the payment system, and read directly by AI (Claude Code CLI / any model) to help with
requirement analysis, test-case writing, and automation coding.

**Knowledge only — no application code, no secrets.** (Code lives in `payment-qa-brain`.)

## Start here

1. **`MAP.md`** — the payment-system landscape: what businesses exist, the 18 domains (one line
   each), how a transaction flows, and where to find what. **Read this first.**
2. **`domains/<domain>/domain_<domain>.md`** — a domain's START HERE: plain-language scope + an
   index of that domain's files.
3. **`docs/GLOSSARY.md`** — terms (MPGS, Xtran, …).
4. **`docs/KB_ARCHITECTURE.md`** — the framework contract: structure, naming, how to contribute.
5. **`docs/COVERAGE.md`** — what's covered vs missing. *(planned)*

## Layout (each folder has one job — see KB_ARCHITECTURE.md)

- `domains/<domain>/` — one taxonomy of **18 business domains**; per domain: `service/ api/
  table/<db>/ flow/ scenario/ troubleshooting/ reference/` + `domain_<domain>.md` entry.
- `MAP.md` / `docs/` — navigation + framework + glossary + coverage.
- `index/domains.yaml` — domain registry (owner / reviewer).
- `templates/` — object templates + authoring rules (read `templates/README.md`).
- `bimo-confirmed/` — knowledge confirmed in BimoQA chats and published.

## How to contribute (and governance)

- All changes go through a **Pull Request** — never push to `main`.
- **Only admins approve/merge** — for both adding new knowledge and removing/changing old
  knowledge (enforced by branch protection + `.github/CODEOWNERS`). Nothing changes silently.
- Follow the framework: find the domain via `MAP.md`, apply `templates/` conventions, distill
  (don't dump) — full steps in `docs/KB_ARCHITECTURE.md` §6–7 and `CONTRIBUTING.md`.
- Merging a PR triggers a `payment-qa-brain` reindex. Before submitting, run
  `scripts/check_knowledge.py` (in `payment-qa-brain`) to catch dangling `related_*` ids.

## Two-layer knowledge model

- **Narrative** — plain-language overviews so a newcomer can understand and follow steps.
- **Typed objects** — technical content (service / API / table / flow / scenario / troubleshooting
  / reference) extracted for precise, linkable knowledge and impact analysis. Don't force every
  document into typed objects — keep business overviews as narrative.

Language: English-first; a little Chinese where it helps (业务术语 / hints).
