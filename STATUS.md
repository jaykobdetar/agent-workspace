# Status and release checklist

Agent Workspace 0.3.0 is an experimental Linux/Python 3.13 coordination tool.
The repository remains private pending owner review. No visibility change,
package publication, service deployment, or historical-state migration is part
of this preparation.

## Validation on 2026-10-29

An isolated checkout of import `b9d48b8` was reviewed and prepared on branch
`release/public-readiness`, using CPython 3.13.13 and locked dependencies.

- `uv sync --locked --extra test --extra mcp --extra lint`: succeeded.
- `.venv/bin/python -m pytest -q`: **18 passed in 4.22 seconds**, no skips,
  with local Unix-socket access. Covers persistence, atomic claims, stale tokens,
  privacy checks, CLI, RPC identities, MCP reconnect, and runner recovery.
- An initial restricted-sandbox run had 14 passes, one failure and three errors
  because socket binding was forbidden. It was rerun with socket access; no
  assertion was removed or skipped to get a passing result.

- `ruff check .`: passed with the explicitly configured E4/E7/E9/F rules.
- `uv lock --check --offline`: passed; dependency pins are unchanged.
- `uv build --no-sources --offline`: source archive and wheel built successfully.
- Fresh wheel-only environment outside the checkout: CLI demo and reopening its
  completed result passed; only `probe-core` was installed.
- Archive inspection: type marker, required source docs/examples present; no
  runtime databases or logs. Relative Markdown links and `git diff --check` pass.
- Available imported history: one commit / 22 text file versions inspected;
  heuristic private-key, GitHub/provider/AWS token, local-home-path and runtime
  filename checks found no matches. Commit metadata uses the owner's public
  GitHub handle and noreply address. Manual source review found no live ledgers,
  receipts, credentials, raw chats, or personal documents. This is a bounded
  review, not a guarantee that every possible secret or provenance issue is absent.

See the release preparation PR for the final revision and review discussion.
Historical counts in the September simplification record are not current test
results. This repository has no CI workflow; the commands in CONTRIBUTING.md are
local checks, not a claim about a hosted CI run.

## Release gates

- [x] Standalone setup, purpose, limitations, and provenance documented.
- [x] Existing MIT notice retained; no third-party source added.
- [x] Missing status, contribution guide, study template, and type marker supplied.
- [x] Locked full test suite passes on Linux/Python 3.13.
- [x] Build, archive contents, isolated wheel smoke, docs links, and lint pass.
- [x] Available import history reviewed for obvious secrets/privacy issues.
- [ ] Owner reviews the draft PR and provenance/ownership before public release.
- [ ] Owner makes a separate visibility/publication decision.

The available history begins at the source-only import. Review cannot certify
absent upstream history or all third-party ownership. No live ledgers, receipts,
credentials, raw conversations, or personal documents should ever be added.
Ignore rules reduce accidental additions but cannot guarantee future privacy.
The board is not a multi-tenant sandbox or proof of scientific correctness; see
[README.md](README.md) and [design](docs/design.md).
