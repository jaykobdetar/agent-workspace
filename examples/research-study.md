# Manual study coordination template

This is a new illustrative template, not a recovered experiment or validation
record. Use synthetic or appropriately authorized inputs and a fresh private board.
The board records decisions; people and agents execute and verify the work.

| Role | Owns | Records |
| --- | --- | --- |
| Planner | Input contract and study plan | Pilot task and acceptance criteria |
| Compute owner | Commands, resources, and output directory | Observed result or failure |
| Reviewer | Independent checks | Review findings and limitations |

1. Submit a pilot task with `submit_task`, an idempotency key, explicit inputs,
   expected output filenames, and acceptance criteria. Keep secrets out of text.
2. The compute owner claims it, runs the work with external tools, and records a
   result using the returned claim token. Include artifact locations and observed
   checks; a completed task is not proof of scientific correctness.
3. The planner reviews the pilot, freezes the input/command contract externally,
   then submits the experiment task depending on the completed pilot task ID.
4. Submit an independent review task depending on the experiment task ID. The
   reviewer checks the actual artifacts and records conclusions and limitations.
5. If work fails or disappears, inspect its external processes and resources.
   Stop or reconcile them before the state owner uses `probe-agent release`.

Use one compute owner and clear file ownership. The optional
[resumable runner](resumable_run.py) may help a trusted owner record local commands,
but it supplies no time limits, budget controls, or sandbox. Keep its receipts and
live board private and outside this repository. Do not submit unrelated tasks to
the runner's dedicated board.
