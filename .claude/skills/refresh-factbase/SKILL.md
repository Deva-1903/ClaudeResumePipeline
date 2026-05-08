---
description: Re-clean context/ files from raw/brain_dump_original.md. Use only when the user explicitly asks to refresh, rebuild, or re-clean the factbase.
argument-hint: "[optional: which context file to refresh]"
---

# Refresh Factbase Skill

## When to use

ONLY when the user explicitly asks. Examples:
- "refresh factbase"
- "re-clean context files from brain dump"
- "update verified claims from raw"

Do not run automatically. Do not run from `/lean-apply` or `/refresh-base-resumes`.

## Goal

Re-derive the structured `context/` files from `raw/brain_dump_original.md` (and any updates the user has merged into the brain dump) so the factbase stays current and consistent.

## Inputs

Primary source:
- `raw/brain_dump_original.md`

Existing structured files (read to understand current shape and to update in place):
- `context/00_resume_factbase.md`
- `context/01_verified_claims.md`
- `context/02_do_not_claim.md`
- `context/03_skills.md`
- `context/04_project_bank.md`
- `context/05_bullet_bank.md`
- `context/06_role_targeting.md`
- `context/07_resume_style_rules.md`

## Hard rules

- Do not invent facts. Every fact in the structured files must trace to `raw/brain_dump_original.md`.
- Cleanly separate **verified claims** from **needs-verification** claims. When in doubt, downgrade.
- Do not promote a "needs verification" claim into a verified claim without explicit user confirmation.
- Preserve role family taxonomy in `06_role_targeting.md`.
- Preserve the structure of each numbered file; do not rename files.
- Do not modify `base_resumes/` or `reference_resumes/`.
- Do not write to `applications/`.
- Do not generate a tailored resume.
- Do not compile.

## Workflow

1. Confirm scope (default: refresh all eight `context/` files).
2. Read `raw/brain_dump_original.md` and the current `context/` files.
3. Update each `context/` file in place:
   - `00_resume_factbase.md` — keep as a router/index.
   - `01_verified_claims.md` — only claims supported by the brain dump; mark uncertain claims as "Needs verification".
   - `02_do_not_claim.md` — guardrails and risky-claim watchlist.
   - `03_skills.md` — labelled by Strong / Working knowledge / Exposure based on evidence.
   - `04_project_bank.md` — facts, technologies, possible bullets, and per-project "do not claim" notes.
   - `05_bullet_bank.md` — paste-ready bullets, tagged by role family.
   - `06_role_targeting.md` — base resume routing and emphasis per role family.
   - `07_resume_style_rules.md` — style and tailoring rules.
4. Surface any contradictions found in the brain dump (e.g., metric drift, role-title variants) under "Needs verification".
5. Final response under 5 bullets: which `context/` files changed, the most important factual updates, any newly-flagged "Needs verification" items, anything that became safe to promote.

## Forbidden

- Generating tailored resumes.
- Writing to `applications/`.
- Modifying `base_resumes/` or `reference_resumes/`.
- Producing PDF or any non-Markdown output.
- Inventing claims that are not in the brain dump.
