# tracking/

Cross-application telemetry for the resume pipeline. Updated automatically by `/lean-apply` and `/revise-resume`. Read by `/skill-gaps`.

## Files

### `skill_gaps.jsonl`

Append/upsert log of JD keywords that are **missing from the factbase** (tagged `[factbase gap]` in the run output). One JSON object per line.

```json
{ "keyword": "Go", "count": 10, "roles": { "SDE": 4, "SRE": 5, "ML": 1 }, "companies": ["Uber", "Snowflake_Systems"], "first_seen": "2026-05-08", "last_seen": "2026-05-10" }
```

Fields:
- `keyword` — canonical name after applying `aliases.md`.
- `count` — total number of `/lean-apply` runs where this gap was surfaced.
- `roles` — bucket counts (`SDE`, `SRE`, `ML`, `AI`, `Applied_Scientist`).
- `companies` — distinct list of companies (deduped, append-only).
- `first_seen` / `last_seen` — ISO date.

What is NOT in here:
- `[resume gap]` keywords — those exist in the factbase already and indicate a regeneration issue, not a learning gap.
- `[ignore]` keywords — JD-specific noise, not a learning signal.

### `aliases.md`

Canonical name map. Apply before incrementing counts so `k8s` / `Kubernetes` / `kubernetes` collapse to one entry. User-extensible — add new aliases at the bottom of the list.

## Reading the data

Run `/skill-gaps` for a ranked report. It prints top N keywords by count, grouped by role bucket. That is your prioritized learning queue.

## Resetting

To start over: delete `skill_gaps.jsonl` (or rename it to `skill_gaps.YYYY-MM-DD.jsonl` to archive). The next `/lean-apply` will recreate the file.
