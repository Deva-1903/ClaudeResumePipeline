---
description: Sync a tailored application folder's meta.json into the "Summer 2026 Internship Applications" Notion database (upsert one lean row, idempotent, never clobbers manual edits). Use when the user asks to log/sync an application to Notion, or invokes /sync-notion. Also called as the final step of /lean-apply.
argument-hint: "[application folder name, optional]"
---

# Sync to Notion Skill

## Goal

Upsert one **lean** row into the Notion database **Summer 2026 Internship Applications** from a tailored application folder's `meta.json`. The application folder is the source of truth and holds all the rich metadata; Notion holds only the few fields needed to track and triage at a glance. Idempotent: running it twice for the same application updates the same row, never creates a duplicate, and never overwrites fields the user edited by hand in Notion.

This skill is invoked two ways:
- Standalone (`/sync-notion`, or "sync this to Notion") — sync one named folder, or the most recently generated application if none is named.
- As the final step of `/lean-apply` — sync the application that was just generated.

## Notion target (stable identifiers)

- Database: `Summer 2026 Internship Applications` (`ce18727e-229e-4926-8231-2f720c8393b3`).
- Data source (parent for new rows): `data_source_id = 82266594-1a82-4da2-9c8d-34263950cc62`.

If a Notion write fails because an ID is stale, re-`fetch` the database to recover the current data source id, then proceed. Do not invent IDs.

## Property mapping (meta.json → Notion column) — LEAN SET ONLY

The pipeline writes ONLY these columns. Keep it minimal — the folder has the full breakdown.

| Notion column | Type | Value from meta.json |
|---|---|---|
| `Company Name` | title | `company` |
| `Position Title` | text | `role` |
| `Application Status` | status | **score-gated** (see below): `"Applied"` if `fit_score >= 70`, else `"Researching"` |
| `date:Date Applied:start` | date | `applied_date` (also set `date:Date Applied:is_datetime` = 0) |
| `Match Score` | number | `fit_score` (the JD Fit Score, e.g. 82) |

**Score-gated status.** Only confidently mark a row `Applied` when the resume is a strong match; otherwise park it as `Researching` for the user to review/submit by hand.
- `fit_score >= 70` (verdict Submit or Strong Submit) → `Applied`
- `fit_score < 70` (verdict Maybe or Weak Fit) → `Researching`

Columns this skill must **never** write (manual-only — the user owns these): `Rejection Date`, `Requirements Match`, `Notes`, `Application Deadline`, `Job Posting URL`, `Location`, `Salary/Stipend`, `Referral`, `Contact Person`, `Contact Email`, `Next Steps`. In particular, `Rejection Date` and the `Rejected` status are set by hand by the user when a rejection arrives — automation does not touch them.

## Procedure

1. **Resolve the folder.** Use the named folder if given; else the application folder with the newest `applied_date` / most recent `meta.json`. Read its `meta.json`.

2. **Already linked?** If `meta.notion.page_id` is present, this row exists → go to step 4 (update). Otherwise go to step 3 (find-or-create).

3. **Find-or-create.**
   - Search the data source for an existing row matching this application, to avoid duplicating a row the user logged by hand. Use `notion-search` with `query` = company name and `data_source_url = collection://82266594-1a82-4da2-9c8d-34263950cc62`, then among results match on **both** `Company Name` AND `Position Title` (case-insensitive, ignore markdown like `**bold**`).
   - **Match found** → adopt that page: record its `page_id`, then go to step 4 (update), respecting the don't-clobber rule.
   - **No match** → create a new page via `notion-create-pages` with `parent = { type: "data_source_id", data_source_id: "82266594-1a82-4da2-9c8d-34263950cc62" }` and the lean property set (`Company Name`, `Position Title`, `Application Status` = the score-gated value, `date:Date Applied:start`, `date:Date Applied:is_datetime`=0, `Match Score`). Leave page content blank. Capture the returned `page_id` and `url`.

4. **Update (don't-clobber rule).** `fetch` the page's current properties first, then update via `notion-update-page` (`command: "update_properties"`) following these rules exactly:
   - `Application Status`: compute the target (`Applied` if `fit_score >= 70`, else `Researching`). Set it **only if it would move the row forward**, never backward. Status rank: `Not Interested`/`Not Started`/`Researching` (lowest) < `Applied` < `Phone Screen` < `Interview Scheduled` < `Interviewed` < `Offer`/`Rejected`/`Withdrawn` (terminal). Set the target only if current status is empty or ranks **below** the target; otherwise leave it untouched. So `Researching`→`Applied` is allowed (e.g. a re-run scored higher), but `Applied`→`Researching` and any user-advanced status (`Phone Screen`+) are never downgraded.
   - `Match Score`, `Position Title`, `Date Applied`: fill only if currently empty; never overwrite a non-empty value.
   - Never write any manual-only column (see list above).

5. **Write back the link.** Add/refresh a `notion` block in the folder's `meta.json` so future runs are idempotent:
   ```json
   "notion": { "page_id": "<id>", "url": "<page url>", "synced_at": "<ISO 8601>", "action": "created" | "updated" }
   ```
   Preserve all other meta.json fields exactly.

6. **Report** (one or two lines): created vs updated, company + role, Match Score, and the Notion page URL. If invoked from `/lean-apply`, fold this into that skill's final response as a single bullet instead of a separate report.

## Safety

- This skill writes to an external service (Notion). It creates/updates exactly one row per invocation per folder. Do not batch-write many rows unless the user explicitly asks for a backfill.
- Never delete Notion rows. Never set `Rejection Date` or `Rejected` status (manual-only).
- If `meta.json` is missing required fields (`company`, `role`, `applied_date`, `fit_score`), report the gap and skip the sync rather than writing a malformed row.
