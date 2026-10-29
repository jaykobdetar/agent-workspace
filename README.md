# Agent Workspace

A small persistent task board for cooperating agents. Agents submit instructions,
claim ready work, use their own tools, and save a result or failure. The board
coordinates work; it does not execute submitted tasks.

## Features

- SQLite persistence, atomic claims across processes, and dependency ordering.
- Idempotent submission, bounded JSON results, and stale-claim rejection.
- CLI, Linux Unix-socket RPC with peer UID checks, and optional stdio MCP adapter.
- Explicit owner recovery and a separate resumable local-command example.

The distribution is named `probe-core`; imports use `probe_core`. Version 0.3.0
is an experimental developer tool, not a hosted service or a production SLA.

## Quick start

Use Linux, Python 3.13, Git, and [uv](https://docs.astral.sh/uv/).
The supported Python range is currently `>=3.13,<3.14`.

```sh
git clone https://github.com/jaykobdetar/agent-workspace.git
cd agent-workspace
uv sync --locked
uv run --locked probe-agent demo --state "$(mktemp -d)/state"
```

The demo is offline and needs no credentials, models, GPU, or paid service.
It saves a word count and a dependent report. Use a fresh state path each time.
The base package has no third-party runtime dependencies. To use MCP:

```sh
uv sync --locked --extra mcp
```

See the [usage guide](README.source.md) for service/client commands, owner recovery,
and the [resumable runner](examples/resumable_run.py). The
[study template](examples/research-study.md) shows a manual coordination workflow.
For development and builds, see [CONTRIBUTING.md](CONTRIBUTING.md).

## Limits and trust

Claims never expire. There are no automatic retries, task deadlines, spending
controls, process supervision, or cloud resource cleanup. Cancellation and owner
release invalidate claims; they do not stop external work. Confirm that old work
has stopped before reassigning it.

Agent labels are not security identities. All authorized clients share a board;
`--local` trusts the same OS account. Separate service/client UIDs and private
state are required for OS-level separation. This is Linux-specific local transport,
not a network-facing multi-tenant service. See [design](docs/design.md).

Results are agent-supplied records, not independently verified evidence. The
optional runner executes trusted commands with your environment and permissions;
it is not a sandbox. Store ledgers, receipts, commands, and logs outside the
checkout and never commit credentials or live runtime data.

## Status and provenance

This is the standalone home for the selected P0289 source snapshot imported on
2026-10-29. It originated in AI-assisted work associated with
[jaykobdetar/Test-Repo](https://github.com/jaykobdetar/Test-Repo), but its original
Git history and live state were not imported. Test-Repo is historical context,
not a dependency or the clone target for this project. Its other copies may differ.

See [STATUS.md](STATUS.md) for current validation and release gates, and
[the history note](docs/history/README.md) for the limits of the preserved evidence.
The existing [MIT license](LICENSE) and copyright notice are retained. This review
does not independently establish ownership of all historical upstream material.
