---
description: Generate a lean, truthful tailored LaTeX resume from a pasted job description. Use when the user says lean apply mode, pastes a JD, or asks for a tailored resume.
argument-hint: "[job description]"
---

# Lean Apply Resume Skill

## Goal

Given a pasted JD, generate the strongest truthful one-page LaTeX resume for Deva Anand, compile it to PDF, archive the JD, write a `meta.json` generation record, update the skill-gap aggregator, and report a JD Fit Score in chat.

Default output folder: `applications/{Company}_{Role}_{YYYY-MM-DD}/`

Files written into that folder:
- `Deva_Anand_{Company}.tex` — tailored resume
- `Deva_Anand_{Company}.pdf` — compiled via `tectonic`
- `job_description.md` — raw JD as pasted (so `/interview-prep` and `/revise-resume` can re-read it)
- `meta.json` — generation record (schema below)

Side effect on the repo:
- One or more entries upserted into `tracking/skill_gaps.jsonl` (one per `[factbase gap]` keyword, normalized via `tracking/aliases.md`).

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
- `Notes.md`
- cover letter
- interview prep notes
- JD-to-resume mapping table
- `_Applications_Index.csv` row
- a persistent compile log file (compile output is reported in chat only)
- long explanation in chat

Do NOT modify files in `base_resumes/` or `reference_resumes/`.
Do NOT edit historical application folders.
Do NOT read old application folders unless explicitly asked.
Do NOT read `raw/brain_dump_original.md` unless a needed fact is missing from `context/`.

DO (by default, per the goal section):
- compile the tailored `.tex` to PDF via `tectonic`
- save the raw JD as `job_description.md`
- write `meta.json`
- upsert `[factbase gap]` keywords into `tracking/skill_gaps.jsonl`

## Extra artifacts (opt-in only)

The default output is the four files above and nothing else. A cover letter (or any other non-default artifact) is created ONLY when the user explicitly asks for it in the same request — never inferred, never volunteered.

When the user does ask for an extra artifact:
- Create it in the same application folder, named `Deva_Anand_{Company}_{Artifact}.tex` / `.pdf` (e.g. `Deva_Anand_Snowflake_Cover_Letter.tex`). Compile it the same way.
- It is bound by the same truth hierarchy — a cover letter may not state anything the resume could not.
- Record it in `meta.json` under `extra_artifacts`, e.g. `[ { "file": "Deva_Anand_Snowflake_Cover_Letter.pdf", "type": "cover_letter", "requested": true } ]`.

This is the ONLY exception to the "Do NOT create" list above. An artifact present in a folder with no matching `extra_artifacts` entry is drift, not intent.

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

## Truth-audit pass (MANDATORY)

After tailoring the copied `.tex`, and BEFORE compiling or scoring, run a fresh truth audit. Drop the "author" framing and read as a skeptical fact-checker who did not write this resume and is trying to catch an unsupported claim.

1. Re-read ONLY the generated `.tex` and the truth-source files (`01`, `04`, `05`, `03`, `00`; brain dump only if a specific fact is in question). Do NOT consult reference resumes or the JD during this pass — references are style-only, and the JD can never license a claim.
2. Extract every concrete claim in the resume: each metric (number, %, count, revenue, latency, test count), each named tool/technology, each scope/scale word (production, multi-tenant, distributed, real-time), each client/user count, each role/responsibility, and each publication.
3. For each claim, mark it **traceable** (name the truth-source file/line it comes from) or **untraceable** (no backing anywhere in the truth source).
4. Fix every untraceable claim before continuing: replace it with the nearest truthful phrasing from the truth source, or cut it. Then re-audit the fixed lines.
5. Record the outcome in `meta.json` under `truth_audit`: `claims_checked`, `untraceable_found`, `untraceable_remaining` (which MUST be 0).

A resume may not be compiled or scored while any untraceable claim remains. This pass is how the truth hierarchy is enforced — it is not optional and not a formality.

## Application folder and file naming

Folder pattern: `applications/{Company}_{Role}_{YYYY-MM-DD}/`
Resume file pattern: `Deva_Anand_{Company}.tex`

- Underscores, no spaces.
- Strip punctuation from company / role.
- Date format: YYYY-MM-DD using today's date.
- `{Company}` in the filename uses the same sanitized form as the folder (e.g., `JPMorgan_Chase`, `Uber`, `Shopify`).

Example folder + file: `applications/Shopify_Software_Engineering_Intern_2026-05-08/Deva_Anand_Shopify.tex`

## Workflow

1. Parse the JD: extract company, role title, key requirements.
2. Run the JD framing pass: extract role family, priority themes, technical keywords, culture signals.
3. Classify role bucket (use `06_role_targeting.md` for tie-breakers; use the broad-internship strategy for Shopify-like JDs).
4. Select one base resume from `base_resumes/`.
5. Read required `context/` files in the order listed above.
6. Optionally inspect `reference_resumes/*.tex` for formatting/style only.
7. Read `04_project_bank.md` only if a needed phrasing is missing.
8. **Copy** the selected base resume to `applications/{Company}_{Role}_{YYYY-MM-DD}/Deva_Anand_{Company}.tex`. Do NOT edit the original `base_resumes/` file.
9. Tailor only the copied file: reorder skills/projects, swap bullets, rewrite phrasing to mirror JD priorities, cut weak-for-JD bullets.
10. **Truth-audit pass** (see section above): re-audit every claim against the truth source as a skeptical fact-checker; fix every untraceable claim before continuing. Untraceable-remaining must be 0.
11. Compile the `.tex` to PDF using `tectonic` (command shown below). If compile fails, leave the `.tex` in place and surface the error in chat — do not retry blindly. After a successful compile, confirm the PDF is one page (command below); if it spills to a second page, tighten before scoring.
12. **Independent scoring pass**: compute the JD Fit Score and Keyword match (rubrics below) against the final resume, scoring as an independent reviewer rather than the author.
13. Save the raw JD as `applications/{folder}/job_description.md`.
14. Write `applications/{folder}/meta.json` per the schema below (including `truth_audit` and `one_page`).
15. Update `tracking/skill_gaps.jsonl` — upsert one entry per `[factbase gap]` keyword, normalized via `tracking/aliases.md`. Do not aggregate `[resume gap]` or `[ignore]`.
16. Final response under 8 bullets in the format below.

## Compile command

Run from the application folder:

```
tectonic --keep-logs=false --chatter=minimal Deva_Anand_{Company}.tex
```

If `tectonic` is not installed or compile fails, do NOT fall back to creating a broken PDF; report the failure cleanly in chat and let the user run `/compile-resume` after fixing.

One-page check (run after a successful compile, from the application folder):

```
mdls -name kMDItemNumberOfPages Deva_Anand_{Company}.pdf
```

If the count is greater than 1, tighten the resume (compress bullets, trim coursework) and recompile before scoring. Record the final result as `one_page` (true/false) in `meta.json`.

## meta.json schema

```json
{
  "company": "Uber",
  "role": "Software Engineer Intern",
  "applied_date": "2026-05-09",
  "base_used": "sde_backend.tex",
  "role_bucket": "SDE",
  "fit_score": 82,
  "verdict": "Submit",
  "keyword_match": { "present": 14, "total": 18, "percent": 78 },
  "strong_matches": ["Python backend services", "150+ tests at Wysa", "multi-tenant SaaS"],
  "missing_keywords": [
    { "keyword": "Go", "tag": "factbase gap" },
    { "keyword": "Kafka", "tag": "factbase gap" },
    { "keyword": "Snowflake-specific stack", "tag": "ignore" }
  ],
  "jd_sha256": "<hex sha256 of the raw JD text>",
  "generated_at": "<ISO 8601 timestamp>",
  "truth_audit": { "claims_checked": 23, "untraceable_found": 1, "untraceable_remaining": 0 },
  "one_page": true,
  "extra_artifacts": [],
  "revisions": []
}
```

Notes:
- `role_bucket` ∈ `{ "SDE", "SRE", "ML", "AI", "Applied_Scientist" }`.
- `verdict` ∈ `{ "Strong Submit", "Submit", "Maybe", "Weak Fit" }`.
- `missing_keywords` includes ALL tagged keywords (resume gap, factbase gap, ignore) — useful later for `/revise-resume`. Only `factbase gap` items feed the aggregator.
- `truth_audit.untraceable_remaining` MUST be 0 at generation time. If it is not, the resume was not finished and must not be reported as submittable.
- `one_page` is the result of the post-compile page check (true/false).
- `extra_artifacts` lists any non-default file created in the folder on explicit request (e.g. a cover letter) — see "Extra artifacts" below. Empty by default.
- `revisions` is an empty list at generation time; `/revise-resume` appends `{ "at": "...", "summary": "..." }` entries.
- Some legacy folders predate this schema and instead carry `"backfilled": true` with null scores and a `backfill_note`. They were never run through the current pipeline; do not treat their null fields as a generation failure.

## Aggregator update procedure (`tracking/skill_gaps.jsonl`)

For each missing keyword tagged `[factbase gap]`:

1. **Normalize** using `tracking/aliases.md` (case-insensitive lookup). If no alias hit, keep the keyword as-typed in the JD but trim whitespace and strip surrounding punctuation.
2. **Lookup** the existing entry in `tracking/skill_gaps.jsonl` (one JSON object per line) by the normalized keyword.
3. **Upsert**:
   - If new: append a new line with `count: 1`, `roles: { <role_bucket>: 1 }`, `companies: [<company>]`, `first_seen` and `last_seen` set to today.
   - If existing: increment `count`, increment `roles[<role_bucket>]` (default 0), append `<company>` to `companies` if not already present, update `last_seen`.
4. Write the file back as JSONL (one entry per line, stable order: most recently updated last is fine).

Entry shape:

```json
{ "keyword": "Go", "count": 10, "roles": { "SDE": 4, "SRE": 5, "ML": 1 }, "companies": ["Uber", "Snowflake_Systems"], "first_seen": "2026-05-08", "last_seen": "2026-05-10" }
```

If `tracking/skill_gaps.jsonl` does not exist yet, create it. If `tracking/aliases.md` does not exist, skip normalization and use raw keywords.

## JD Fit Score (chat-only)

After the truth-audit pass and a successful compile, evaluate the final resume against the pasted JD using this rubric. Score as an **independent reviewer, not the author**: adopt a skeptical default, award credit only for coverage a hiring screener would actually recognize (not for your own phrasing), and round down on borderline dimensions. Do NOT do dumb keyword matching — score truthful coverage.

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
- Output: `applications/<folder>/Deva_Anand_<Company>.tex` + `.pdf` — 1 page, truth audit clean (`N` claims, 0 untraceable) (or note compile failure / page overflow / audit fixes made)
- JD Fit Score: `XX/100 — Strong Submit | Submit | Maybe | Weak Fit`
- Keyword match: `X/Y (NN%)`
- Strong matches: 2–3 short phrases
- Missing keywords: up to 5 short phrases, each tagged `[resume gap]`, `[factbase gap]`, or `[ignore]`
- Aggregator: short note like `+3 factbase-gap keywords logged to tracking/skill_gaps.jsonl` (or `0 logged` if all gaps were already counted)
- Avoided/missing: only if relevant (one short note on what was deliberately left out)

No long reasoning. No JD analysis prose. No mapping table. No files beyond those listed in the goal section.
