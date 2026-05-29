# Resume Tailoring Pipeline

A token-efficient pipeline for generating tailored, truthful one-page LaTeX resumes from a job description.

## Default flow

```
Paste JD  →  /lean-apply  →  applications/{Company}_{Role}_{YYYY-MM-DD}/
                              ├── Deva_Anand_{Company}.tex
                              ├── Deva_Anand_{Company}.pdf
                              ├── job_description.md
                              └── meta.json
```

Plus a side effect: `tracking/skill_gaps.jsonl` is upserted with each `[factbase gap]` keyword from the run.

Claude picks one base resume, copies it into a new application folder, tailors the copied file, runs a truth-audit pass against the factbase, compiles to PDF via `tectonic`, confirms one page, scores the fit as an independent reviewer, archives the JD, and writes a `meta.json` generation record. The base resumes themselves are never modified by `/lean-apply`.

## How to use it

1. Open a fresh Claude Code session in this repo.
2. Paste the block from [LEAN_APPLY_PROMPT.md](LEAN_APPLY_PROMPT.md) — the JD goes inline.
3. Claude classifies the role, picks one of five base resumes, tailors a copy, audits it for truth, compiles + scores it, and writes `.tex` + `.pdf` + `job_description.md` + `meta.json`, then updates the skill-gap aggregator.
4. If you want changes ("remove this bullet", "fill the whitespace"), run `/revise-resume`.

### Optional escalations

| Phrase | What it adds |
|---|---|
| `/revise-resume` | Edits an existing tailored resume in place — bullet swaps, project swaps, whitespace fixes, tightening. Recompiles PDF, updates meta.json. Bound by truth hierarchy. |
| `/skill-gaps` | Ranks the keywords most often missing from your factbase across past applications, grouped by role bucket. Your prioritized learning queue. |
| `/compile-resume` | Recompiles the `.tex` to PDF (rarely needed — `/lean-apply` and `/revise-resume` already compile). |
| `/interview-prep` | Generates interview prep notes from a chosen `Deva_Anand_{Company}.tex`. Uses the folder's `job_description.md` automatically. |
| `/refresh-base-resumes` | Regenerates `base_resumes/` from the factbase. Style cues come from `reference_resumes/`. |
| `/refresh-factbase` | Re-cleans `context/` files from `raw/brain_dump_original.md`. |

## Where the rules live (canonical sources)

This README is orientation only. The actual rules are defined once, in these files, so nothing drifts:

- **`CLAUDE.md`** — repo-wide policy: the truth hierarchy, the reference hierarchy (style-only), the JD framing requirement, the verify-before-reporting requirement, free-text answer rules, hard "do not" rules, and token discipline.
- **`.claude/skills/lean-apply/SKILL.md`** — the operational spec `/lean-apply` follows: role classification, file naming, the truth-audit + scoring passes, the `meta.json` schema, the skill-gap aggregator procedure, and the chat output format.
- **`context/02_do_not_claim.md`** — the explicit guardrail list of claims that are off-limits.

If this README ever disagrees with `CLAUDE.md` or `SKILL.md`, those win — update them, not a restated copy here.

## Repo layout

```
.
├── CLAUDE.md                       # Repo-wide policy (canonical)
├── LEAN_APPLY_PROMPT.md            # The paste block to start a run
├── README.md                       # This orientation doc
│
├── context/                        # Source of truth + targeting rules
│   ├── 00_resume_factbase.md
│   ├── 01_verified_claims.md
│   ├── 02_do_not_claim.md
│   ├── 03_skills.md
│   ├── 04_project_bank.md
│   ├── 05_bullet_bank.md
│   ├── 06_role_targeting.md
│   ├── 07_resume_style_rules.md
│   └── 08_motivation_bank.md       # Free-text application answers (not a resume truth source)
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
│   └── *.tex
│
├── applications/                   # Output goes here, one folder per application
│   └── {Company}_{Role}_{YYYY-MM-DD}/
│       ├── Deva_Anand_{Company}.tex
│       ├── Deva_Anand_{Company}.pdf
│       ├── job_description.md
│       └── meta.json
│
├── tracking/                       # Cross-application telemetry
│   ├── skill_gaps.jsonl            # Upserted by /lean-apply, read by /skill-gaps
│   ├── aliases.md                  # Keyword normalization map (k8s -> Kubernetes, etc.)
│   └── README.md
│
├── raw/                            # Archive — last-resort fact lookup only
│   └── brain_dump_original.md
│
└── .claude/
    └── skills/
        ├── lean-apply/SKILL.md     # Operational spec (canonical)
        ├── revise-resume/SKILL.md
        ├── skill-gaps/SKILL.md
        ├── compile-resume/SKILL.md
        ├── interview-prep/SKILL.md
        ├── refresh-base-resumes/SKILL.md
        └── refresh-factbase/SKILL.md
```

## Keeping the factbase current

- Update `context/01_verified_claims.md` (and the project/bullet banks) when a project ships, a metric becomes available, or a "Needs Verification" claim is confirmed.
- Refresh `context/` from the brain dump with `/refresh-factbase`.
- Refresh `base_resumes/` from the factbase with `/refresh-base-resumes`.
- Drop strong recent resumes into `reference_resumes/` to anchor style choices for future runs.
- Do **not** update the factbase to chase a JD keyword. The factbase reflects ground truth; the resume reflects what the JD highlights from that ground truth.
