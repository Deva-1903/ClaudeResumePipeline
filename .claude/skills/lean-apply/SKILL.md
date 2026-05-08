---
description: Generate a lean, truthful tailored LaTeX resume from a pasted job description. Use when the user says lean apply mode, pastes a JD, or asks for a tailored resume.
argument-hint: "[job description]"
---

# Lean Apply Resume Skill

## Goal

Given a pasted JD, generate the strongest truthful one-page LaTeX resume for Deva Anand.

Default output must be exactly one file:

`applications/{Company}_{Role}_{YYYY-MM-DD}/Tailored_Resume.tex`

Do not create any other file unless explicitly requested.

## Truth vs reference (do not confuse these)

**Truth source** — the only places factual claims may come from:
1. `context/01_verified_claims.md`
2. `context/04_project_bank.md`
3. `context/05_bullet_bank.md`
4. `context/03_skills.md`
5. `context/00_resume_factbase.md`
6. `raw/brain_dump_original.md` (last resort only)

**Reference source** — formatting and style only; never truth:
1. `base_resumes/*.tex` (starting structure)
2. `reference_resumes/*.tex` (recent strong resumes for layout, spacing, voice)

If a reference resume conflicts with the factbase, the factbase wins.

## Hard default restrictions

Do NOT create:
- Resume.pdf or Tailored_Resume.pdf
- Notes.md
- Job_Description.md
- jd_snapshot.md
- cover letter
- interview prep
- JD-to-resume mapping table
- application tracker / `_Applications_Index.csv` row
- compile logs
- long explanation in chat

Do NOT compile by default.
Do NOT modify files in `base_resumes/`.
Do NOT modify files in `reference_resumes/`.
Do NOT edit historical application folders.
Do NOT read old application folders unless explicitly asked.
Do NOT read `raw/brain_dump_original.md` unless a needed fact is missing from the numbered context files.
Do NOT treat any tailored resume in `applications/` as a reference unless the user has explicitly moved it into `reference_resumes/`.

## Source files (read in this order, stop when you have what you need)

Always read:
1. `context/00_resume_factbase.md`
2. `context/06_role_targeting.md`
3. `context/07_resume_style_rules.md`
4. `context/01_verified_claims.md`
5. `context/02_do_not_claim.md`
6. `context/03_skills.md`
7. `context/05_bullet_bank.md`

Read only if needed:
- `context/04_project_bank.md` (project-level alternate phrasings)
- `reference_resumes/*.tex` (formatting / spacing / voice only — not for facts)
- `raw/brain_dump_original.md` (last resort for a specific fact)

## Role classification

Pick exactly one bucket:

1. SDE / Backend → `base_resumes/sde_backend.tex`
2. SRE / Systems / Infrastructure / Platform → `base_resumes/sre_systems.tex`
3. ML Engineer / ML Systems → `base_resumes/ml_engineer.tex`
4. AI Engineer / LLM Engineer / Agentic AI → `base_resumes/ai_engineer.tex`
5. Applied Scientist / Research Intern / Research Engineer → `base_resumes/applied_scientist.tex`

Use `context/06_role_targeting.md` "Ambiguous Role Rules" to break ties. Pick the resume that best matches the JD's evaluation criteria, not just the title.

## Reference resume rules

`reference_resumes/*.tex` may be consulted for:
- LaTeX preamble / custom-command patterns.
- Section ordering.
- Bullet density and spacing.
- Voice and tone of strong final resumes.

`reference_resumes/*.tex` may NOT be used to:
- Introduce a new factual claim, metric, tool, or project not already in the truth source.
- Override a phrasing in `context/05_bullet_bank.md`.
- Replace the chosen base resume.

If a claim appears in a reference resume but not in the truth source, do not use it. Either omit it or rephrase truthfully from the factbase.

## Resume quality rules

The resume must:
- Stay one page in intent.
- Preserve the chosen base resume's preamble, custom commands, and visual style exactly.
- Use truthful verified evidence only.
- Be ATS-friendly without keyword stuffing.
- Prefer concrete engineering verbs.
- Prefer JD-relevant projects and bullets.
- Avoid vague filler.
- Avoid fake metrics, production claims, cloud/Kubernetes claims, or model-scale claims.

Allowed edits to the **copied file** in `applications/`:
- Reorder skills row.
- Reorder projects.
- Swap bullets for more JD-relevant ones from `05_bullet_bank.md`.
- Tighten or compress bullets without distorting meaning.
- Adjust the coursework list to highlight JD-relevant courses.
- Add JD-relevant keywords ONLY when supported by `01_verified_claims.md` or `03_skills.md`.

Forbidden edits:
- Inventing metrics, tools, users, production scale, publications, or deployment claims.
- Importing unsupported buzzwords from a reference resume.
- Promoting coursework to research output or POCs to production.
- Listing projects flagged in `02_do_not_claim.md` (e.g., LLM Inference Service, Distributed Training Simulator, Scalar-Tensor Autograd Engine, private CS 690PF projects).

## Application folder naming

Pattern: `applications/{Company}_{Role}_{YYYY-MM-DD}/Tailored_Resume.tex`

- Use underscores, not spaces.
- Remove punctuation from company / role.
- Date format: YYYY-MM-DD using today's date.

Example: `applications/Amazon_SDE_Intern_2026-05-08/Tailored_Resume.tex`

## Workflow

1. Parse the JD: extract company, role title, and key requirements.
2. Classify role bucket (use `06_role_targeting.md` for tie-breakers).
3. Select one base resume from `base_resumes/`.
4. Read required context files in the order listed above.
5. Optionally inspect `reference_resumes/*.tex` for formatting/style only — never for facts.
6. Read `04_project_bank.md` only if a needed phrasing is missing.
7. **Copy** the selected base resume to `applications/{Company}_{Role}_{YYYY-MM-DD}/Tailored_Resume.tex`. Do NOT edit the original `base_resumes/` file.
8. Tailor only the copied file: reorder skills/projects, swap bullets from `05_bullet_bank.md`, tighten as needed.
9. Do not compile.
10. Final response under 5 bullets.

## Final response format

Reply with only:
- Base used: `<base_resumes/...>`
- Output: `<applications/.../Tailored_Resume.tex>`
- Top 2–3 tailoring changes
- Any unverifiable claim avoided (only if relevant)

No long reasoning. No JD analysis. No mapping table.
