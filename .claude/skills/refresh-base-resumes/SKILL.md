---
description: Regenerate or improve base_resumes/*.tex from the factbase. Use only when the user explicitly asks to refresh or rebuild base resumes.
argument-hint: "[optional: which role family to refresh]"
---

# Refresh Base Resumes Skill

## When to use

ONLY when the user explicitly asks. Examples:
- "refresh base resumes"
- "rebuild base resumes from factbase"
- "update base_resumes/sde_backend.tex"

Do not run automatically. Do not run from `/lean-apply`.

## Goal

Regenerate or improve one or more files in `base_resumes/` so they remain stable, role-generic, one-page LaTeX templates aligned with the current factbase.

## Inputs

Truth source (must read):
- `context/01_verified_claims.md`
- `context/02_do_not_claim.md`
- `context/03_skills.md`
- `context/04_project_bank.md`
- `context/05_bullet_bank.md`
- `context/06_role_targeting.md`
- `context/07_resume_style_rules.md`
- `context/00_resume_factbase.md` (router)

Reference source (style only, never truth):
- `reference_resumes/*.tex`
- existing `base_resumes/*.tex`

Last resort:
- `raw/brain_dump_original.md` only when a needed fact is missing from `context/`.

## Hard rules

- Do not invent facts. Every claim must be supported by the truth source.
- Do not copy unsupported claims from `reference_resumes/*.tex`. References inform LaTeX style only.
- Preserve the existing preamble, color palette, custom commands, and one-page intent of `base_resumes/`.
- Keep each base resume **role-generic** — these are starting templates, not JD-tailored resumes.
- Do not write anything to `applications/`.
- Do not compile.
- Do not create PDF, Notes.md, mapping tables, or summaries.

## Workflow

1. Confirm which base resume(s) to refresh (default: all five).
2. Read the truth source files.
3. Read existing `base_resumes/` and `reference_resumes/` for style cues.
4. Regenerate the chosen `base_resumes/*.tex` files in place.
5. Validate that each base resume:
   - Uses only claims supported by the truth source.
   - Lists no project flagged in `02_do_not_claim.md`.
   - Stays one-page in intent.
   - Matches the role family it represents (per `06_role_targeting.md`).
6. Final response under 5 bullets: which base resumes changed, what high-level changes, any "Needs Verification" item now confirmed.

## Forbidden

- Tailoring for a specific JD.
- Writing to `applications/`.
- Modifying `context/` files.
- Modifying `reference_resumes/` files.
- Producing PDF or any non-`.tex` output.
