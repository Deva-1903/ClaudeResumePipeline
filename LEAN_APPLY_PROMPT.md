# LEAN_APPLY_PROMPT.md

> Paste the block below into a fresh Claude Code session in this repo, with the JD appended.
> This runs **inside Claude Code chat**, not in the terminal shell.

---

```
/lean-apply

JD:

[paste job description here]
```

---

Default output:

```
applications/{Company}_{Role}_{YYYY-MM-DD}/Tailored_Resume.tex
```

Exactly one file. No PDF, no notes, no JD snapshot, no cover letter, no interview prep, no index update.

## Optional escalations (use the exact phrase)

| Phrase | Adds |
|---|---|
| `compile this resume` or `/compile-resume` | runs LaTeX on the latest `Tailored_Resume.tex`; produces `.pdf` only |
| `interview mode` or `/interview-prep` | generates interview prep notes from the chosen resume; does not touch the resume |
| `refresh base resumes` or `/refresh-base-resumes` | regenerates `base_resumes/` from the factbase (style cues from `reference_resumes/`) |
| `refresh factbase` or `/refresh-factbase` | re-cleans `context/` files from `raw/brain_dump_original.md` |
| `archive JD` | saves the JD to `jd_snapshot.md` in the application folder |
| `update index` / `track this application` | appends one row to `applications/_Applications_Index.csv` |

## What `/lean-apply` does

- Reads `context/00_resume_factbase.md` first (router), then the rest of the numbered context files as needed.
- Picks one base from `base_resumes/`: `sde_backend.tex`, `sre_systems.tex`, `ml_engineer.tex`, `ai_engineer.tex`, or `applied_scientist.tex`.
- **Copies** the chosen base resume into a new application folder, then tailors only the copy.
- Optionally consults `reference_resumes/*.tex` for formatting/style only — never for facts.
- Writes only `applications/{Company}_{Role}_{YYYY-MM-DD}/Tailored_Resume.tex`.
- Final reply is under 5 bullets.
