# Contributing

Use an isolated Linux checkout with Python 3.13 and uv. No GPU, provider account,
or API key is needed. Keep changes focused on local task coordination.

```sh
uv sync --locked --extra test --extra mcp --extra lint
uv run --locked python -m pytest -q
uv run --locked ruff check .
uv build --no-sources
```

The tests require local Unix sockets and spawn small local worker processes.
A sandbox that blocks socket binding cannot run the transport/MCP tests. Tests
use temporary state, not live ledgers. Always install the MCP extra for the full
suite; a missing dependency is not a successful skip. The lint extra is optional
for users, but useful when contributing.

Review the wheel and source archive before publication: the wheel should contain
`probe_core/py.typed`, and the source archive should include the docs and examples.
Run the installed wheel's `probe-agent demo` from outside the source tree in a
fresh virtual environment to catch packaging/import errors.

Do not commit local credentials, `.env` files, databases, receipts, logs, model
weights, or real task contents. Keep runtime directories outside the checkout;
ignore patterns are a backstop, not a privacy guarantee. Use synthetic test data.

Describe behavior changes and exact validation results in a pull request. Preserve
license notices, identify the source/license of any added third-party material,
and do not treat historical validation claims as current test evidence. The
release checklist is in [STATUS.md](STATUS.md). Repository publication remains an
owner decision separate from code review.
