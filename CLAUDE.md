# Resume Pipeline Instructions

This repo is Deva Anand's resume-tailoring pipeline.

## Default flow

- Use the `/lean-apply` skill when the user pastes a job description.
- Default output is the application folder `applications/{Company}_{Role}_{YYYY-MM-DD}/` containing:
  - `Deva_Anand_{Company}.tex` — tailored resume
  - `Deva_Anand_{Company}.pdf` — compiled with `tectonic`
  - `job_description.md` — raw JD as pasted (for later `/interview-prep` and `/revise-resume`)
  - `meta.json` — generation record (base, role bucket, fit score, keyword match, missing keywords, JD hash, timestamps, truth-audit result, one-page flag)
- `{Company}` in the filename uses the same sanitized form as the folder — underscores, no spaces, no punctuation. Example: `Deva_Anand_Uber.tex`.
- After writing meta.json, `/lean-apply` must update `tracking/skill_gaps.jsonl` with each `[factbase gap]` keyword (normalized via `tracking/aliases.md`). `[resume gap]` and `[ignore]` are not aggregated.

## Truth hierarchy (source of factual claims)

1. `context/01_verified_claims.md`
2. `context/04_project_bank.md`
3. `context/05_bullet_bank.md`
4. `context/03_skills.md`
5. `context/00_resume_factbase.md`
6. `raw/brain_dump_original.md` — fallback when a needed fact is missing from the numbered files

If a claim appears in any of these files, treat it as usable factual material. Do not weaken or hedge a claim just because it has a number attached. Quantified facts in the truth source — 8+ UK clients, $340K+ revenue, 10,000+ submissions, 20+ VAPT, 100+ hrs/month, 60% throughput, 150+ tests, 20+ APIs — are meant to be used.

What's still off-limits: inventing claims that do NOT appear anywhere in the truth source. See `context/02_do_not_claim.md`.

## Reference hierarchy (style and structure only — never truth)

1. `base_resumes/*.tex` — stable starting templates per role family.
2. `reference_resumes/*.tex` — recent strong resumes for formatting/style examples only.
3. Recent `.tex` resumes the user explicitly provides — same status: style only.

Recent resumes can guide LaTeX formatting, spacing, bullet density, section layout, and resume voice. They cannot independently introduce a project, metric, tool, business impact, user/client count, publication, or responsibility. If a claim appears only in a reference resume and not in the truth source, do not use it. If a reference resume conflicts with the truth source, the truth source wins.

## Free-text application answers

When the user is filling a free-text application box ("Why are you interested?", "Anything else we should know?", "Why are you looking?"), draw from `context/08_motivation_bank.md` — reusable, company-agnostic voice fragments. Pick 2–3 that fit the role, then add one company-specific hook re-derived from the JD (same stable-truth + per-JD-framing approach as `/lean-apply`).

- Bound by the same truth hierarchy: do not state a motivation that is not backed by the truth source.
- Never bank or reuse a "how did you hear about us" answer — it is always channel-specific; leave it as a fill-in placeholder.
- This is NOT a resume truth source and must NOT be read during `/lean-apply` (see Token discipline).

## /lean-apply must include a JD framing pass

Tailoring is not "pick the right bullets". After selecting evidence, rewrite the resume so the same truthful experience is framed in the language and priorities of the specific JD.

Extract from every JD:
- Role family (SDE/Backend, SRE/Systems, ML, AI, Applied Scientist, Data, Security).
- Employer priority themes (ownership, quality, ambiguity, simple solutions to complex problems, debugging/research mindset, AI-assisted development, infra/platform scale, product thinking, security/reliability).
- Technical keywords (only those supported by the truth source).
- Behavioral / culture signals.

Then tailor by reordering sections/bullets, rewriting phrasing to echo JD language while preserving truth, reordering skills, choosing JD-aligned projects, and cutting bullets that are strong generally but weak for this JD. Do not invent claims. Do not keyword-stuff.

## /lean-apply must verify before reporting

Tailoring is not the last step. After the resume is written, `/lean-apply` runs two mandatory passes (detailed in the skill):

1. **Truth-audit pass** — re-read the generated `.tex` against the truth source as a skeptical fact-checker (not the author). Every metric, tool, scope word, count, and claim must trace to the truth source; fix or cut any that do not. `meta.json.truth_audit.untraceable_remaining` must be 0 before compile or scoring.
2. **One-page + independent score** — compile, confirm the PDF is one page, then score Fit and Keyword match as an independent reviewer with a skeptical default.

A resume with an unresolved untraceable claim is not finished and must not be reported as submittable.

## Other rules

- Do not edit `base_resumes/` during `/lean-apply`. Copy the chosen base into the new application folder, then tailor only the copied file.
- Do not edit `reference_resumes/` during `/lean-apply`.
- Do not read old `applications/` resumes by default (current application's own files are fine).
- Do not promote coursework to research output or POCs to production.
- Do not list projects flagged as off-limits in `context/02_do_not_claim.md`.
- Do not create Notes.md, cover letter, interview prep, JD-to-resume mapping table, application index CSV, compile logs, or long chat summaries by default. A cover letter or other extra artifact is created ONLY on explicit request in the same message, named `Deva_Anand_{Company}_{Artifact}.tex`, bound by the truth hierarchy, and logged in `meta.json.extra_artifacts`. An artifact with no matching `extra_artifacts` entry is drift.
- Compile every `/lean-apply` run to PDF via `tectonic`. If the compile fails, leave the `.tex` in place and surface the error in the final reply.
- Final response under 8 bullets (Fit Score + Keyword match + base + paths + matches + gaps).

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

- `/compile-resume` — recompile an existing `Deva_Anand_{Company}.tex` to PDF.
- `/revise-resume` — edit a tailored resume in place ("remove this bullet", "fill whitespace", "tighten this line"). Bound by the truth hierarchy. Recompiles PDF and updates `meta.json`.
- `/skill-gaps` — read `tracking/skill_gaps.jsonl` and print the top missing keywords by count, grouped by role bucket.
- `/interview-prep` — generate interview notes from a chosen tailored resume (uses the folder's `job_description.md` if present).
- `/refresh-base-resumes` — regenerate `base_resumes/` from the factbase.
- `/refresh-factbase` — re-clean `context/` files from `raw/brain_dump_original.md`.

## Tracking

- `tracking/skill_gaps.jsonl` — one JSON object per line, one line per normalized keyword. Updated by `/lean-apply` and `/revise-resume`. Read by `/skill-gaps`.
- `tracking/aliases.md` — canonical keyword map (e.g., `k8s → Kubernetes`, `golang → Go`). Apply before incrementing counts so spellings do not fragment the data.
