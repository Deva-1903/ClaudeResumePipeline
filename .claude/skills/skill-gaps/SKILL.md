---
description: Report the top JD keywords missing from Deva's factbase, ranked by count and grouped by role bucket. Use when the user invokes /skill-gaps or asks what to learn next based on past applications.
argument-hint: "[top N — optional, default 15]"
---

# Skill Gaps Skill

## Goal

Read `tracking/skill_gaps.jsonl` and print a ranked, actionable report of what the user is most often missing across past `/lean-apply` runs. This is the prioritized learning queue.

## Rules

- Read-only. Never modify `tracking/skill_gaps.jsonl` or `tracking/aliases.md`.
- Never write new files.
- Do not invent counts or roles — only report what is in the JSONL.
- If the JSONL is empty or missing, say so plainly and suggest running `/lean-apply` a few times first.
- Do not read application folders, `context/`, or the brain dump.

## Input

- Optional `N` argument — how many keywords to show. Default 15.
- Optional filters the user may state in chat:
  - "for SRE roles" / "for ML roles" → filter to entries with that bucket
  - "this month" / "last 7 days" → filter by `last_seen`
  - "show companies" → expand the companies list per row

## Output (chat)

A single compact report. No extra files.

### Section 1: Top N missing keywords

A markdown table, sorted by `count` descending, ties broken by `last_seen` descending:

| # | Keyword | Count | Roles | Last seen |
|---|---|---|---|---|
| 1 | Go | 10 | SDE:4, SRE:5, ML:1 | 2026-05-10 |
| 2 | Kafka | 7 | SDE:5, SRE:2 | 2026-05-09 |

### Section 2: Role-bucket breakdown

For each bucket that has gaps, list the top 5 keywords for THAT bucket:

```
SDE (12 distinct gaps): Go (4), Kafka (5), Redis (3), gRPC (2), Distributed Systems (2)
SRE (8 distinct gaps): Kubernetes (6), Terraform (4), Prometheus (3), ...
ML (4 distinct gaps): ...
```

### Section 3: Suggested learning priorities

3–5 lines of plain-English suggestions:

- "Go is asked in 10 JDs across SDE+SRE — highest ROI to learn first."
- "Kafka shows up in 7 JDs, mostly SDE/backend — pair it with a small streaming side project."
- "Kubernetes is dominantly SRE — only learn if pivoting toward SRE roles."

Be concrete. Tie the suggestion to the bucket distribution.

## What this skill does NOT do

- It does not edit `context/03_skills.md` to add a learned skill. The user must do that manually after actually learning the skill.
- It does not delete entries from the aggregator. Stale entries naturally age out via `last_seen` (the user can filter on it).
- It does not re-run `/lean-apply` against any JDs.

## Final response

Keep the report self-contained. Under ~30 lines of output total. No long preamble, no analysis prose beyond Section 3's suggestions.
