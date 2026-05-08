# reference_resumes/

Drop strong recent `.tex` resumes here as **style and formatting references only**.

## What these files are for

- LaTeX preamble and custom-command examples.
- Section ordering and layout choices that worked.
- Bullet density, spacing, and visual rhythm.
- Project-ordering examples on real applications.
- Examples of what a "finished" resume looks and reads like.
- Preserving Deva's resume voice across tailoring runs.

## What these files are NOT

- They are **not** the source of truth for any factual claim.
- They are **not** base resumes — `/lean-apply` does not start from them.
- They are **not** automatically promoted from `applications/`.

## Hard rules

1. Do not copy a bullet, metric, tool, project detail, or achievement from a reference resume unless it is also supported by:
   - `context/01_verified_claims.md`, or
   - `context/04_project_bank.md`, or
   - `context/05_bullet_bank.md`, or
   - (last resort) `raw/brain_dump_original.md`.
2. If a reference resume conflicts with the factbase, **the factbase wins**. Update the reference resume — never the factbase — to match.
3. Generated tailored resumes in `applications/` are **not** references. They only become references if the user manually moves a `.tex` file into this folder.
4. `/lean-apply` may *consult* files here for style and formatting only, and only if needed.

## Suggested naming

`{role-family}_{date}.tex` — e.g. `sde_backend_2026-05.tex`, `ai_engineer_2026-04.tex`. Keeps the most recent reference per role family obvious.
