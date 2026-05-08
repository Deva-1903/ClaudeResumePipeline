# Resume Tailoring Pipeline

A token-efficient pipeline for generating tailored, truthful one-page LaTeX resumes from a job description.

## Default flow

```
Paste JD  →  /lean-apply  →  applications/{Company}_{Role}_{YYYY-MM-DD}/Tailored_Resume.tex
```

That's it. No PDF, no notes, no cover letter, no interview prep — unless you ask.

Claude picks one base resume, copies it into a new application folder, tailors the copied file, and writes `Tailored_Resume.tex`. The base resumes themselves are never modified by `/lean-apply`.

## How to use it

1. Open a fresh Claude Code session in this repo.
2. Paste the block from [LEAN_APPLY_PROMPT.md](LEAN_APPLY_PROMPT.md) — the JD goes inline.
3. Claude classifies the role, picks one of five base resumes, copies it into a new application folder, tailors the copy, and writes one `.tex` file.
4. To compile to PDF later, run `/compile-resume` and point it at the file.

### Optional escalations

| Phrase | What it adds |
|---|---|
| `/compile-resume` | Compiles the `.tex` to PDF. No tailoring, no notes. |
| `/interview-prep` | Generates interview prep notes from a chosen `Tailored_Resume.tex`. Does not modify the resume. |
| `/refresh-base-resumes` | Regenerates `base_resumes/` from the factbase. Style cues come from `reference_resumes/`. |
| `/refresh-factbase` | Re-cleans `context/` files from `raw/brain_dump_original.md`. |

## Repo layout

```
.
├── CLAUDE.md
├── LEAN_APPLY_PROMPT.md
├── README.md
│
├── context/                        # Source of truth
│   ├── 00_resume_factbase.md
│   ├── 01_verified_claims.md
│   ├── 02_do_not_claim.md
│   ├── 03_skills.md
│   ├── 04_project_bank.md
│   ├── 05_bullet_bank.md
│   ├── 06_role_targeting.md
│   └── 07_resume_style_rules.md
│
├── base_resumes/                   # Stable one-page LaTeX templates per role family
│   ├── sde_backend.tex
│   ├── sre_systems.tex
│   ├── ml_engineer.tex
│   ├── ai_engineer.tex
│   └── applied_scientist.tex
│
├── reference_resumes/              # Style-only references — never truth
│   ├── README.md
│   └── *.tex                       # (you drop strong recent resumes here)
│
├── applications/                   # Output goes here, one folder per application
│   └── {Company}_{Role}_{YYYY-MM-DD}/
│       └── Tailored_Resume.tex
│
├── raw/                            # Archive — last-resort fact lookup only
│   └── brain_dump_original.md
│
└── .claude/
    └── skills/
        ├── lean-apply/SKILL.md
        ├── compile-resume/SKILL.md
        ├── interview-prep/SKILL.md
        ├── refresh-base-resumes/SKILL.md
        └── refresh-factbase/SKILL.md
```

## Brain dump vs recent resumes

The cleaned brain dump and `context/` files are the **source of truth**. Recent `.tex` resumes can be placed in `reference_resumes/`, but they are used only for layout, style, spacing, and examples of strong final resumes.

The pipeline must not rely on recent resumes for factual claims. If a bullet, metric, tool, project detail, or achievement appears in a recent resume but is not supported by the factbase, Claude will not use it.

## Reference resume usage

Rules:
- Use `reference_resumes/*.tex` only for formatting and style.
- Do not copy unsupported claims from a reference resume.
- Do not use a reference resume as a base resume unless explicitly promoted (move it into `base_resumes/`).
- Do not promote a generated `applications/.../Tailored_Resume.tex` into a reference unless the user manually moves it into `reference_resumes/`.

## How role classification works

`/lean-apply` reads the JD and picks one of five buckets:

| Bucket | Base resume | When |
|---|---|---|
| SDE / Backend | `sde_backend.tex` | "Software Engineer," "Backend," "Full-Stack" |
| SRE / Systems | `sre_systems.tex` | "Site Reliability," "Platform," "Performance," "Infrastructure" |
| ML Engineer | `ml_engineer.tex` | "ML Engineer," "ML Systems," "ML Platform" |
| AI Engineer | `ai_engineer.tex` | "AI Engineer," "LLM Engineer," "Agentic AI," "GenAI" |
| Applied Scientist | `applied_scientist.tex` | "Research Intern," "Applied Scientist," "Research Engineer" |

Tie-break rules and JD-specific routing live in [context/06_role_targeting.md](context/06_role_targeting.md).

## Truth rules

The pipeline is built around three guarantees:

1. **No invention.** Every claim must trace to the truth hierarchy below.
2. **Hard guardrails.** Things forbidden by default — production scale claims, fake metrics, unverified publications, projects with no public repo — live in [context/02_do_not_claim.md](context/02_do_not_claim.md).
3. **Adjacent truth.** When a JD asks for something unsupported, the resume rephrases adjacent truthful experience instead of stretching a claim.

### Truth hierarchy

1. `context/01_verified_claims.md`
2. `context/04_project_bank.md`
3. `context/05_bullet_bank.md`
4. `context/03_skills.md`
5. `context/00_resume_factbase.md`
6. `raw/brain_dump_original.md` (last resort only)

### Reference hierarchy (style only)

1. `base_resumes/*.tex` (starting structure)
2. `reference_resumes/*.tex` (formatting/style examples only)

## Token discipline

`/lean-apply` reads files in this order and stops as soon as it has what it needs:

1. `context/00_resume_factbase.md` (router)
2. `context/06_role_targeting.md`, `07_resume_style_rules.md`
3. `context/01_verified_claims.md`, `02_do_not_claim.md`, `03_skills.md`
4. `context/05_bullet_bank.md`
5. `context/04_project_bank.md` (only if a phrasing is missing)
6. `reference_resumes/*.tex` (only for formatting/style, only if needed)
7. `raw/brain_dump_original.md` (last resort only)

It does NOT read old `applications/` folders or previous tailored resumes by default.

## When to update what

- Update `context/01_verified_claims.md` (and the project/bullet banks) when a project ships, a metric becomes available, or a "Needs Verification" claim is confirmed.
- Refresh `context/` from the brain dump with `/refresh-factbase`.
- Refresh `base_resumes/` from the factbase with `/refresh-base-resumes`.
- Drop strong recent resumes into `reference_resumes/` to anchor style choices for future runs.
- Do NOT update the factbase to chase a JD keyword. The factbase reflects ground truth; the resume reflects what the JD highlights from that ground truth.
