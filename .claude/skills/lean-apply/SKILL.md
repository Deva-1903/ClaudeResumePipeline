---
description: Generate a lean, truthful tailored LaTeX resume from a pasted job description. Use when the user says lean apply mode, pastes a JD, or asks for a tailored resume.
argument-hint: "[job description]"
---

# Lean Apply Resume Skill

## Goal

Given a pasted JD, generate the strongest truthful one-page LaTeX resume for Deva Anand and report a JD Fit Score in chat.

Default output is exactly one file:

`applications/{Company}_{Role}_{YYYY-MM-DD}/Tailored_Resume.tex`

The JD Fit Score appears only in the final chat response. No extra files.

## Truth vs reference (do not confuse these)

**Truth source** — the only places factual claims may come from:
1. `context/01_verified_claims.md`
2. `context/04_project_bank.md`
3. `context/05_bullet_bank.md`
4. `context/03_skills.md`
5. `context/00_resume_factbase.md`
6. `raw/brain_dump_original.md` (fallback for missing facts)

Trust the truth source. Quantified claims that already live there (8+ UK clients, $340K+, 10K+ submissions, 20+ VAPT, 100+ hrs/month, 60% throughput, 150+ tests, 20+ APIs, 8 architectures on CIFAR-10, 100–500-question batches, etc.) are usable as-is. Do not weaken or hedge them.

**Reference source** — formatting and style only; never truth:
1. `base_resumes/*.tex`
2. `reference_resumes/*.tex`
3. Recent `.tex` resumes the user pastes inline (treated identically to `reference_resumes/`).

If a claim appears only in a reference resume, do not use it. If a reference conflicts with the truth source, the truth source wins.

## Hard default restrictions

Do NOT create:
- `Resume.pdf` or `Tailored_Resume.pdf`
- `Notes.md`
- `Job_Description.md`
- `jd_snapshot.md`
- cover letter
- interview prep
- JD-to-resume mapping table
- application tracker / `_Applications_Index.csv` row
- compile logs
- long explanation in chat

Do NOT compile by default.
Do NOT modify files in `base_resumes/` or `reference_resumes/`.
Do NOT edit historical application folders.
Do NOT read old application folders unless explicitly asked.
Do NOT read `raw/brain_dump_original.md` unless a needed fact is missing from `context/`.

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

Use `context/06_role_targeting.md` "Ambiguous Role Rules" and "Broad SDE Internship Strategy" to break ties. For broad multi-track internships (Shopify-like: Software + Data + Applied ML + Infra + Security with ownership/quality/ambiguity language), default to SDE/Backend unless the JD is clearly ML/research/infra-specific.

## JD framing pass (MANDATORY)

After evidence is selected, before writing the resume, extract from the JD:

1. **Role family** — which of the five buckets, plus any secondary track angles.
2. **Employer priority themes** — ownership, quality, ambiguity, fast-paced execution, simple solutions to complex problems, debugging/research mindset, infra/platform scale, product thinking, AI-assisted development, security/reliability.
3. **Technical keywords** — APIs, distributed systems, pipelines, databases, ML models, data products, infra, security, plus company-stack keywords. Only surface keywords supported by the truth source.
4. **Behavioral / culture signals** — constant learner, takes ownership, enjoys research, quality-focused, resilient in ambiguity, uses AI tools effectively.

Then, while editing the **copied** resume in `applications/`:

A. Reorder sections and project order to put the JD's emphasis first.
B. Rewrite bullet phrasing to echo JD language while preserving truth.
C. Reorder skills row so JD-relevant tools appear first.
D. Choose projects that match the team's likely placement.
E. Adjust project subtitles where they sharpen role relevance.
F. Cut bullets that are strong in general but weak for this specific JD.
G. Make the resume feel written for this company/role — without inserting the company name unless natural.

A resume that reads "generic + correct" has failed the framing pass. See `context/06_role_targeting.md` "Bullet rewriting examples" for the rewrite pattern.

## Resume quality rules

- Stay one page in intent.
- Preserve the chosen base resume's preamble, custom commands, and visual style exactly.
- Use truthful verified evidence only.
- Be ATS-friendly without keyword stuffing.
- Prefer concrete engineering verbs.
- Prefer JD-relevant projects and bullets.
- Avoid vague filler.
- Avoid fake metrics, production claims, cloud/Kubernetes claims, or model-scale claims that aren't in the truth source.
- **Always-on Cloud row**: every tailored resume must surface `AWS, GCP, Azure` somewhere in the Skills row (in a Cloud / DevOps category), even when the JD does not mention cloud. The "do not claim cloud production ownership" rule still holds — these are listed as resume-safe skills only.
- **No em-dashes (`---`)** in bullet or item text. LaTeX renders `---` as an em-dash; use a comma instead. (LaTeX section-marker comments like `%----------SKILLS----------` are fine — they don't render.)

Allowed edits to the **copied file** in `applications/`:
- Reorder skills row.
- Reorder projects.
- Swap bullets for more JD-relevant ones from `05_bullet_bank.md`.
- Tighten or compress bullets without distorting meaning.
- Adjust the coursework list to highlight JD-relevant courses.
- Add JD-relevant keywords ONLY when supported by `01_verified_claims.md` or `03_skills.md`.

Forbidden:
- Inventing metrics, tools, users, production scale, publications, deployment claims.
- Importing unsupported claims from a reference resume.
- Promoting coursework to research output or POCs to production.
- Listing projects flagged in `02_do_not_claim.md` as off-limits.

## Application folder naming

Pattern: `applications/{Company}_{Role}_{YYYY-MM-DD}/Tailored_Resume.tex`

- Underscores, no spaces.
- Strip punctuation from company / role.
- Date format: YYYY-MM-DD using today's date.

Example: `applications/Shopify_Software_Engineering_Intern_2026-05-08/Tailored_Resume.tex`

## Workflow

1. Parse the JD: extract company, role title, key requirements.
2. Run the JD framing pass: extract role family, priority themes, technical keywords, culture signals.
3. Classify role bucket (use `06_role_targeting.md` for tie-breakers; use the broad-internship strategy for Shopify-like JDs).
4. Select one base resume from `base_resumes/`.
5. Read required `context/` files in the order listed above.
6. Optionally inspect `reference_resumes/*.tex` for formatting/style only.
7. Read `04_project_bank.md` only if a needed phrasing is missing.
8. **Copy** the selected base resume to `applications/{Company}_{Role}_{YYYY-MM-DD}/Tailored_Resume.tex`. Do NOT edit the original `base_resumes/` file.
9. Tailor only the copied file: reorder skills/projects, swap bullets, rewrite phrasing to mirror JD priorities, cut weak-for-JD bullets.
10. Compute the JD Fit Score (rubric below) against the final resume — for chat output only.
11. Do not compile.
12. Final response under 7 bullets in the format below.

## JD Fit Score (chat-only)

After writing `Tailored_Resume.tex`, evaluate the final resume against the pasted JD using this rubric. Do NOT do dumb keyword matching — score truthful coverage.

| Dimension | Max |
|---|---|
| Core role match (does the resume's primary framing match the JD's primary track?) | 25 |
| Must-have technical coverage (JD's required tech is surfaced where truthfully supported) | 25 |
| Evidence strength from work/projects (concrete, JD-relevant work bullets carry weight) | 20 |
| JD framing / employer priority alignment (priority themes echoed in phrasing and ordering) | 15 |
| Natural keyword coverage (JD vocabulary present without stuffing) | 10 |
| Resume focus and clarity (one page, no filler, strong-first ordering) | 5 |
| **Total** | **100** |

Verdict band:
- **85–100** Strong Submit
- **70–84** Submit
- **55–69** Maybe
- **0–54** Weak Fit

### Gap classification (chat-only)

Classify each gap into one of three labels:

- **resume gap** — claim is in the brain dump/context but did not make it into the resume. Action: regenerate or adjust.
- **factbase gap** — claim is missing from the brain dump/context too. Real skill/project gap. Action: build or learn it later.
- **ignore** — optional, company-specific, or not required by the JD.

## Keyword match score (chat-only)

Separate, ATS-style coverage check that complements the JD Fit Score.

Procedure:
1. Extract the JD's **important keywords** — tools, technologies, methods, named platforms, and concrete priority phrases (e.g. "Python", "Azure DevOps", "automation", "AI-driven", "ownership", "documentation", "monthly releases"). Skip generic verbs and filler.
2. Split them into two buckets:
   - **Must-have** — required-qualifications and explicitly-named tools/methods.
   - **Nice-to-have** — preferred-qualifications, soft signals, or learning-outcome phrasing.
3. For each keyword, mark **present / missing** against the final tailored resume text.
4. Compute: `Keyword match: X/Y (NN%)` where Y = total important keywords (must-have + nice-to-have) and X = present.
5. List up to 5 missing keywords tagged with the same gap labels (`[resume gap]`, `[factbase gap]`, `[ignore]`).

Do **not** keyword-stuff the resume to inflate this score. The JD Fit Score still penalizes stuffing under "Natural keyword coverage" and "Resume focus and clarity".

## Final response format (chat output)

Reply with under 8 bullets in this shape:

- Base used: `base_resumes/<file>.tex`
- Output: `applications/<folder>/Tailored_Resume.tex`
- JD Fit Score: `XX/100 — Strong Submit | Submit | Maybe | Weak Fit`
- Keyword match: `X/Y (NN%)`
- Strong matches: 2–3 short phrases
- Missing keywords: up to 5 short phrases, each tagged `[resume gap]`, `[factbase gap]`, or `[ignore]`
- Avoided/missing: only if relevant (one short note on what was deliberately left out)

No long reasoning. No JD analysis prose. No mapping table. No file other than `Tailored_Resume.tex`.
