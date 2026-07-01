# Contributing

All knowledge changes are made through pull requests and merged only by an admin.

## Process
1. Read `docs/KB_ARCHITECTURE.md` and `MAP.md`.
2. Create a branch — never push to `main`.
3. Add or edit files under `domains/<domain>/…`, following `templates/README.md`. New content is `draft`.
4. Open a pull request describing what changed and why.
5. An admin reviews and merges. Removals follow the same process.

## Rules
- No application code, no secrets, no real card numbers or internal hostnames.
- `related_*` reference existing ids only; back-fill the other side when adding an object.
- `name` is human-readable; code names and acronyms go in `aliases`.
- Unknown values are marked `待补`; nothing is invented.
