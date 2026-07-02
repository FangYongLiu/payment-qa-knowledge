# Contributing — Botim team (botim-core)

Onboarding for the Botim app QA team. For the full rules see `templates/README.md` (authoring) and
`docs/KB_ARCHITECTURE.md` (framework + governance); this page only adds what is specific to the
`botim-core` business line.

## Using this knowledge base with AI (Claude Code)
The knowledge base is plain markdown read **directly** — an AI agent reads it from your local files,
not from a remote server. To use it:

1. **Clone it locally**: `git clone https://github.com/Astra-QA/qa-knowledge-base.git`
2. **Run Claude Code CLI inside the clone.** The root `CLAUDE.md` loads automatically and tells the
   agent how to navigate (read `MAP.md` → pick a domain → read its `domain_<domain>.md` → follow
   `related_*` / `[[links]]`; grep by id prefixes `svc_ api_ tbl_ …`). No index or setup needed —
   the structure is the index.
3. **Using it from another project** (e.g. your test-automation repo): clone this repo alongside and
   point the agent at it (a line in your project's own `CLAUDE.md` such as "Payment / Botim domain
   knowledge lives in `../qa-knowledge-base` — consult it first" works well). The agent does not read
   remote repos on its own.

The repo is internal-visibility; reading a **local clone** needs no extra auth. Keep your clone up to
date with `git pull` before you rely on it.

## Where your knowledge goes
The repo is a two-level tree: `domains/<business-line>/<domain>/`. Your business line is
**`botim-core`** (the Botim app: IM, VoIP, Ads, Mini Program). It currently holds four skeleton
domains — `im`, `voip`, `ads`, `miniprogram` — whose bodies are `待补`, waiting to be filled.
`botim-money` (payment / PayBy) is the other business line; use it as a worked example.

## Adding knowledge — three steps
1. **Register the domain** (only when creating a new one): add an entry to `index/domains.yaml` with
   `business_line: botim-core` and its `owner` (the domain's QA owner).
2. **Create the entry point**: `domains/botim-core/<domain>/domain_<domain>.md`, following
   `templates/domain.md`.
3. **Fill the objects**: under the domain, add files by type — `service/`, `api/`, `table/<db>/`,
   `flow/`, `scenario/`, `troubleshooting/`. Each type has a template in `templates/<type>.md`;
   fill every section.

## Three rules that must hold
- **Never fabricate.** Anything you cannot confirm is marked `待补` (discoverable, filled later) —
  never invented.
- **Cross-references point to existing ids only.** `related_*` and `[[links]]` must resolve; if the
  target does not exist yet, name it in prose and mark `待补` — do not leave a broken link.
- **Add and back-link.** When you add an object, update the related files so both sides reference
  each other.

## Pull request flow (every change goes through a PR)
```
git checkout -b <your-branch>
# edit...
git commit          # commit messages in English
git push -u origin <your-branch>
# open a PR on GitHub targeting main
```
- **Never push to `main`** — branch protection blocks it.
- PRs under `domains/botim-core/` are approved by the Botim QA lead **Kejun.Liu (@kejun-liu_astg)**
  before merge (see `.github/CODEOWNERS`).
- New content is `status: draft`; an admin flips it to `active` at merge.

## Read these first
- `MAP.md` — the landscape; read it first.
- `templates/README.md` — the full authoring rules (object types, naming, frontmatter, relations, self-check).
- `docs/KB_ARCHITECTURE.md` — the framework contract and governance.
- Sample of a fully populated domain: `domains/botim-money/activation/`.
