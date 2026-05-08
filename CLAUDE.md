# Resume Pipeline Instructions

This repo is Deva Anand's resume-tailoring pipeline.

## Default flow

- Use the `/lean-apply` skill when the user pastes a job description.
- Default output is exactly one file:
  `applications/{Company}_{Role}_{YYYY-MM-DD}/Tailored_Resume.tex`

## Truth hierarchy (source of factual claims)

1. `context/01_verified_claims.md`
2. `context/04_project_bank.md`
3. `context/05_bullet_bank.md`
4. `context/03_skills.md`
5. `context/00_resume_factbase.md`
6. `raw/brain_dump_original.md` — last resort only

## Reference hierarchy (style and structure only — never truth)

1. `base_resumes/*.tex` — stable starting templates per role family.
2. `reference_resumes/*.tex` — recent strong resumes for formatting/style examples only.

## Rules

- Do not treat recent `.tex` resumes as truth.
- Do not copy any bullet, metric, tool, or project claim from `reference_resumes/` unless it is also verified in the truth hierarchy above.
- If a reference resume conflicts with the factbase, the factbase wins.
- Do not read old `applications/` resumes by default.
- Do not edit `base_resumes/` during `/lean-apply`.
- Do not edit `reference_resumes/` during `/lean-apply`.
- Copy the selected base resume into the new application folder, then tailor only the copied file.
- Do not invent metrics, production scale, users, tools, publications, employment history, cloud/Kubernetes ownership, or hackathon placements.
- Do not promote coursework to research output or POCs to production.
- Do not list projects flagged in `context/02_do_not_claim.md`.
- Do not create PDF, Notes.md, Job_Description.md, jd_snapshot.md, cover letter, interview prep, JD mapping table, application index row, compile logs, or long chat summaries by default.
- Do not compile LaTeX unless `/compile-resume` is invoked or a PDF is explicitly requested.
- Final response must be under 5 bullets.

## Token discipline

Read order during `/lean-apply`:

1. `context/00_resume_factbase.md` (router)
2. `context/06_role_targeting.md`, `07_resume_style_rules.md`
3. `context/01_verified_claims.md`, `02_do_not_claim.md`, `03_skills.md`
4. `context/05_bullet_bank.md`
5. `context/04_project_bank.md` (only if a phrasing is missing)
6. `reference_resumes/*.tex` (only for formatting/style, only if needed)
7. `raw/brain_dump_original.md` (last resort only)

Do not read old `applications/` folders or generated tailored resumes by default.

## Optional skills (run only when user explicitly invokes)

- `/compile-resume` — compile an existing `Tailored_Resume.tex` to PDF.
- `/interview-prep` — generate interview notes from a chosen tailored resume.
- `/refresh-base-resumes` — regenerate `base_resumes/` from the factbase (uses references for style only).
- `/refresh-factbase` — re-clean `context/` files from `raw/brain_dump_original.md`.
