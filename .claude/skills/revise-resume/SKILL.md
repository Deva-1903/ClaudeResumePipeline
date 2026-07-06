---
description: Edit an already-generated tailored resume in place ("remove this bullet", "swap this project", "fill the whitespace", "tighten this line"). Bound by the truth hierarchy. Recompiles the PDF and updates meta.json. Use when the user asks for changes to an existing applications/<folder>/Deva_Anand_<Company>.tex.
argument-hint: "[path to Deva_Anand_{Company}.tex] [free-text revision instructions]"
---

# Revise Resume Skill

## Goal

Apply user-directed edits to an existing tailored resume without regenerating from scratch. Preserve truthfulness, one-page layout, and the base resume's visual style.

Trigger phrases (any of these counts as `/revise-resume`):
- "remove this bullet" / "drop the X line"
- "add a bullet about X" (only if X is in the truth source)
- "swap this project for X"
- "there's whitespace at the bottom — fill it" / "the resume looks empty / too dense"
- "tighten this bullet" / "expand this bullet" / "rewrite this in JD language"
- "reorder so Wysa is first"

## Inputs

1. **Path to the `.tex` file** — should be `applications/<folder>/Deva_Anand_<Company>.tex`. If the user does not specify, infer the most recent one (most recent `last_seen` or folder date). If ambiguous, ask once.
2. **Revision instructions** — free text. Could be one edit or several.

Also read (if present in the same folder):
- `job_description.md` — to keep JD framing consistent.
- `meta.json` — to know the role bucket, current fit score, and missing keywords.

## Rules

- **Truth hierarchy still applies.** Same rules as `/lean-apply`. Do not introduce claims that are not in:
  1. `context/01_verified_claims.md`
  2. `context/04_project_bank.md`
  3. `context/05_bullet_bank.md`
  4. `context/03_skills.md`
  5. `context/00_resume_factbase.md`
  6. `raw/brain_dump_original.md` (last resort)
- Do not modify `base_resumes/` or `reference_resumes/`.
- Do not change the file path or rename the resume.
- Do not invent metrics or production claims to fill whitespace.
- Do not introduce em-dashes (`---`) in bullet text.
- Keep the always-on `AWS, GCP, Azure` row.
- Do not leak company name into bullets unless natural.

## Whitespace handling

When the user reports too much whitespace:

1. Inspect the `.tex` to find where the gap is (often a missing bullet under a role, or a project section with only two bullets).
2. **Prioritize Work Experience first.** Fill by strengthening the Experience section before Projects, restore a 2nd/3rd bullet to a thin experience entry (Wysa, Cario) or surface another truthful JD-relevant experience bullet, and only add to the strongest project once Experience is well-shown. Pull additional supporting bullets from `context/05_bullet_bank.md` (or `context/04_project_bank.md` for project-level alternates) that are JD-aligned and truthful.
3. If no truthful additional bullet exists, instead tighten line breaks / adjust spacing macros if the base resume uses them. Do not stretch text by adding filler.
4. Recheck one-page fit after recompile.

When the resume looks dense / overflows:

1. Identify the weakest-for-JD bullet (cross-reference `meta.json.missing_keywords` and `job_description.md`).
2. Cut or compress it.
3. Prefer cutting low-signal lines over shrinking font size.

## Workflow

1. Locate the target `.tex`. Read it. Read sibling `meta.json` and `job_description.md` if present.
2. Read only the `context/` files needed for the requested edits:
   - Bullet swaps: `context/05_bullet_bank.md` + `context/01_verified_claims.md`.
   - Project swaps: `context/04_project_bank.md`.
   - Tightening / phrasing: no additional context reads required.
3. Apply the edits via `Edit` (or `Write` if the rewrite is large) to the `.tex`. Do NOT create a `.tex.bak` or `Deva_Anand_<Company>_v2.tex` — edit in place.
4. Recompile to PDF:

   ```
   tectonic --keep-logs=false --chatter=minimal Deva_Anand_{Company}.tex
   ```

5. Re-evaluate the Fit Score and Keyword match against the same JD (using the rubric from `/lean-apply`).
6. Update `meta.json`:
   - Overwrite `fit_score`, `verdict`, `keyword_match`, `strong_matches`, `missing_keywords` with the new values.
   - Append a new entry to `revisions`: `{ "at": "<ISO 8601>", "summary": "<one-line description of what changed>" }`.
7. If the revision shifted any `[factbase gap]` keywords IN or OUT of the missing list, update `tracking/skill_gaps.jsonl` accordingly:
   - Newly missing → upsert (increment count for this company+role only if not already counted for this application; do not double-count a single application).
   - No longer missing → no action (we don't decrement; the history of "was asked once" still matters).
   - In practice, do NOT re-increment counts for keywords already counted in this application's prior generation. Treat `/revise-resume` as a touch-up, not a new application.

## Output (chat)

Under 6 bullets:

- Edits applied: 1-line summary of each
- Resume: `applications/<folder>/Deva_Anand_<Company>.tex` + `.pdf` (or compile error)
- New JD Fit Score: `XX/100 — verdict` (delta vs prior: `+3` / `-2` / `unchanged`)
- New Keyword match: `X/Y (NN%)` (delta)
- meta.json: `revision #N appended`
- Aggregator: `no change` or short note

No long reasoning. No diff dump. The user can `git diff` if they want the full change.
