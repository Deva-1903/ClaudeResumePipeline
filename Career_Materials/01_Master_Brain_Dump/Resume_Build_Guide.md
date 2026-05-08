# Resume Build Guide

> **Open this doc every time you tailor a resume.** It chains together: (1) the brain dump (source of truth), (2) the customization workflow (process), and (3) every style + ATS + content rule you've adopted.
>
> **Last updated:** 2026-05-08

---

## How to use this doc

Read this file top-to-bottom on every new application. Don't skim — the most common mistakes (comma splices, "Built…Built…Built", inconsistent dates, naked acronyms, summary statements creeping back in) all come from skipping a section.

When something on this doc no longer reflects your standards, update it here first, then propagate.

---

## Step 0 — The two source docs

1. **`Career_Brain_Dump.md`** (sibling file in this folder) — the only place where new facts, bullets, metrics, and projects get added. Resumes pull *from* it; nothing flows the other way.
2. **The job description** — saved as `Applications/YYYY-MM-DD__Company__Role/Job_Description.md` with source URL and date.

If a fact you want isn't in the brain dump, **add it to the brain dump first**, then pull it into the resume. Never add to the resume directly.

---

## Step 1 — Set up the application folder

```
Applications/
└── YYYY-MM-DD__Company__Role/
    ├── Job_Description.md
    ├── Tailored_Resume.tex     (or .docx)
    ├── Tailored_Resume.pdf
    └── Notes.md
```

Naming rules:
- `YYYY-MM-DD` = the date you start drafting.
- `Company` = official name, no spaces, no abbreviations future-you won't recognize.
- `Role` = job title, PascalCase or camelCase, no spaces.

Append a row to `Applications/_Applications_Index.csv` once the folder exists.

---

## Step 2 — Read the JD with intent

In `Job_Description.md`, capture at top:
- Source URL + date saved
- Job ID (if any)
- Salary band (if listed)
- Top 8–12 keywords the JD repeats
- Conferral / visa / start-date constraints — confirm you qualify

---

## Step 3 — Pick the persona, tagline, and starting layout

- Persona: match the JD against `Career_Brain_Dump.md §2 Target Roles Seen Across Resumes`.
- Tagline: *the resume currently has no tagline below the name (this is intentional — keywords belong in bullets, not in a tagline).* If you decide to add one, pick from §1 of the brain dump; do not invent.
- Starting layout: copy the closest of the **Latest_6** as a `.tex` template:
  - ML / DL / research → `Latest_6/Deva_Anand_Resume_Adobe_ML_Intern.tex`
  - LLM / agents / eval → `Latest_6/Deva_Resume_Microsoft_CoreAI.tex`
  - SDE / Backend / Distributed Systems → use the AWS Data Services tailoring at `Applications/2026-05-08__Amazon__AWSDataServicesSDEIntern/Tailored_Resume.tex` (already has the cleaned style applied).
  - Generic SWE / Applied ML → `Latest_6/Deva_Resume.pdf` (PDF — derive a `.tex` from it once).

---

## Step 4 — Fill content from the brain dump

Per section, pull only from the brain dump:

| Section | Pull from brain dump |
|---|---|
| Education | §8 |
| Skills | §3 (reorder so the cluster matching the JD's loudest keywords comes first; trim to 4 rows of related skills, not a kitchen-sink list) |
| Experience | §4 (Wysa: pick 2–3 of the 5 bullet variants A–E; Cario: pick 2 of the 3 variants A–C) |
| Projects | §5 — pick 2–4 projects with **mutually distinct JD-coverage clusters** (don't pick two distributed-data projects; pick one distributed-data + one microservice/AI + one fundamentals-coverage) |
| Publication & Extracurriculars | §6, §7, §8 — keep tight |

---

## Step 5 — Apply every style rule below

These are the rules that came out of real recruiter / network feedback. Treat them as non-negotiable unless a JD's format constraints say otherwise.

### 5.1 Header

- **Full preferred name** at top.
- **No tagline / no summary statement / no objective / no professional photo / no references** line.
- **Phone:** drop the `+1` (write `(413) 315-1715`).
- **Email:** the actual email address as the visible text (`devaanand@umass.edu`), not "Email" as a label.
- **Portfolio / LinkedIn / GitHub:** show the **full URL as visible text** (e.g., `linkedin.com/in/devaaa`, `github.com/Deva-1903`, `devaanand.com`) — *not* just the word "LinkedIn" or "GitHub". Reason: in-person networking, recruiters with a printed copy on a desk, or someone reading an ATS-extracted plain-text version cannot search you up if all they see is a logo or label. Make it hassle-free for them.
- **No FontAwesome icons** in the header. They sometimes confuse ATS parsers. The visible URLs do all the labeling work.
- **Separator** between contact items: use `\enspace\textbar\enspace` (a vertical bar) — clean, neutral, no Unicode glyphs that ATS may drop.

### 5.2 Sections to include (in order, omit if irrelevant)

Education → Skills → Experience → Projects → Publication & Extracurriculars (combine if either is short). Optional only if relevant: Leadership, Research, Volunteering, Interests.

### 5.3 Education

- Include all higher education. **No high school.**
- Use **"Expected Graduation: Month YYYY"** or a span (e.g., `September 2025 -- May 2027 (Expected)`). Never "Present".
- Selective coursework, abbreviated, no course numbers (write "Advanced Machine Learning" not "CS689 Advanced Machine Learning").
- Limit coursework to 1–2 lines.
- Include GPA only if **3.3+** (or use a higher major GPA if applicable). Do not include if low.
- Spell out "Bachelor of Engineering" rather than "B.E." in the degree line.

### 5.4 Skills

- Group skills into 3–5 named rows (e.g., `Languages`, `Backend & Distributed`, `Databases & Cloud`, `AI / GenAI Tooling`).
- Each row is a comma-separated list of related items.
- **Soft skills do not go in the Skills section.** Demonstrate them in bullets instead.
- Reorder rows so the cluster the JD asks for first appears first.

### 5.5 Experience — bullet construction (STAR + verb discipline)

- Header: company, role, dates, location.
- **2–5 bullets per role.** STAR (Situation → Task → Action → Result), with metrics where the brain dump §6 supports them.
- **Strong action verb at the start of every bullet.** Use the CICS action verb list (Engineered, Architected, Owned, Designed, Implemented, Migrated, Profiled, Analyzed, Hardened, Constructed, Developed, Programmed, Optimized, Reduced, Led, Shipped, Investigated). Avoid weak verbs (Worked on, Helped, Was responsible for).
- **Vary verbs across bullets.** Never start three bullets with the same verb. Audit by reading the first word of each bullet top-to-bottom — they should all be different (with rare exceptions for parallelism).
- Match verb tense to dates: past tense for past roles, present tense only for current roles.
- If the employer or role isn't well-known, give one-line context in the first bullet or in the header.

### 5.6 Projects — bullet construction

- 2–4 projects. Each maps to a *distinct* JD signal cluster.
- **HARD RULE: do not surface a project on a resume unless it has a public GitHub repo with real code that the recruiter can open today.** Private GitHub Classroom repos, "no repo yet," and empty/stub repos all fail this check. Use `Career_Brain_Dump.md` Appendix C — GitHub repo inventory — as the single source of truth for which projects are eligible. If a strong project doesn't yet have a public repo, either (a) push a public version (scrub course identifiers if needed) before submitting, or (b) pick a different project that does.
- Why this rule exists: every project line on a resume is an implicit invitation to "go look." A reader who hits a 404 or a private-repo wall loses trust faster than if the project had been omitted entirely. In-person networkers and printed-resume readers also can't verify private projects.
- Header line: project name + **full URL as visible text** for the repo (no "Repo" label, no GitHub logo). Example: `github.com/Deva-1903/Spark-ETL-Optimization`.
- Tech stack on its own line under the project name.
- 2 bullets per project (one for what was built, one for results / instrumentation / hardening).
- Use varied verbs across projects: Profiled, Analyzed, Developed, Hardened, Implemented, Constructed, Designed. Do **not** open three project bullets with "Built".

### 5.7 Word discipline

- **Drop unnecessary articles and filler words:** `a`, `an`, `the`, `various`, `etc.`, `basic`, `simple`, `I`, `we`, `our`. Examples:
  - "Architected a full-stack ML platform" → "Architected full-stack ML platform"
  - "Integrated LLMs into a chat product" → "Integrated LLMs into chat product"
  - "Designed an inference microservice" → "Designed inference microservice"
- Use parallel structure across bullets (same verb pattern, same tense).
- A mix of one-line and two-line bullets is optimal — avoid all bullets being the same length.
- Avoid putting two distinct ideas in one bullet. Either split, or use a comma + "-ing" verb to chain them.

### 5.8 Acronyms

- Common acronyms (`ML`, `API`, `AWS`, `SQL`, `REST`, `CI/CD`, `URL`) — fine to use bare.
- Specialized acronyms — **spell out on first use, then use the acronym**. Examples:
  - `Vulnerability Assessment and Penetration Testing (VAPT)`
  - `Directed Acyclic Graph (DAG)`
  - `Extract-Transform-Load (ETL)` (when audience may be non-data)
  - `Denoising Diffusion Probabilistic Models (DDPM)`
  - `Reciprocal Rank Fusion (RRF)`
- After the spell-out, you can use the acronym freely in later bullets.

### 5.9 Date formatting

- **Spell out month names in full** for consistency: `September 2025`, `July 2023`, `November 2022`, `May 2023`. Never mix `Jul` with `May`.
- Date range separator: en-dash with spaces (`--` in LaTeX).
- Right-aligned dates in section headers.
- Match verb tense to date span (past for ended roles, present for current).

### 5.10 Vertical spacing & layout

- Section spacing must be **visually consistent**. After every `\section`'s content list, end with the same `\vspace{-4pt}` (or whatever the chosen value is). Do not let one section have `\vspace{-8pt}` while another has nothing.
- 1 page only (internships and most early-career roles). 2 pages allowed only when explicitly invited or for senior roles.
- Single column. No two-column layouts that ATS might split incorrectly.
- 11–12pt body, 10pt acceptable if needed for fit. Black text on white background.
- Regular fonts (sourcesanspro, Computer Modern, Latin Modern). No display fonts.
- Bullet endings: with or without periods, but **be consistent across the whole resume.**
- To buy more vertical space when tight: shrink left indent, reduce inter-bullet spacing, drop the secondary education entry's coursework line (keep degree + dates).

### 5.11 ATS hygiene

- Real text everywhere (no images of text, no rasterized headers).
- Real (selectable) text in headers and footers, never as image backgrounds.
- No tables that confuse parsers (the `tabularx` skills block is parser-friendly; nested `tabular*` for headers is also fine).
- No FontAwesome icons in critical text. Visible URLs do the job.
- File name on save: `Deva_Anand_Resume.pdf` (or `Deva_Anand_Resume_Company.pdf` if you want the version embedded). No `(1)`, no `_FINAL`, no `v2`.
- Save the source `.tex` (or `.docx`) in the application folder; submit only the `.pdf`.

### 5.12 Punctuation & grammar

- Comma splices are the most common mistake. Run a grep through your bullets for `, ` followed by a verb-form: replace with semicolon, period, or "and".
- Match verb tense to date.
- Spell-check (`chktex`, browser spellcheck on the rendered PDF, or read aloud).

---

## Step 6 — Pre-submit QA checklist

Run through this every time before exporting the PDF:

```
HEADER
[ ] Full name at top
[ ] No tagline / summary / objective
[ ] Phone has no +1
[ ] Email is the actual address (no "Email" label)
[ ] Portfolio / LinkedIn / GitHub shown as full visible URLs
[ ] No FontAwesome icons in header
[ ] Separators consistent

EDUCATION
[ ] All higher education listed (no high school)
[ ] Dates use full month names
[ ] Coursework relevant to JD, abbreviated, no course numbers
[ ] GPA included only if 3.3+

SKILLS
[ ] 3–5 named rows
[ ] Most JD-relevant cluster appears first
[ ] No soft skills here

EXPERIENCE
[ ] Strong action verb opens every bullet
[ ] No bullet starts with the same verb as the previous bullet (vary)
[ ] Verb tense matches date span
[ ] Specialized acronyms (VAPT, etc.) spelled out on first use
[ ] No "a / an / the" filler
[ ] Metrics traceable to brain dump §6

PROJECTS
[ ] Each project listed has a PUBLIC GitHub repo with real code (cross-check against Career_Brain_Dump.md Appendix C)
[ ] Each project covers a distinct JD signal cluster
[ ] Project header includes full repo URL (visible text), no GitHub logo
[ ] Project verbs vary (no three "Built")
[ ] Each project has 2 bullets
[ ] Click every project URL once and confirm it opens the repo (not 404, not private)

PUBLICATION & EXTRACURRICULARS
[ ] No comma splices
[ ] Open-source contributions listed by project name where possible
[ ] Tutoring / volunteer impact quantified if available

GLOBAL
[ ] Section spacing visually consistent
[ ] 1 page (verify after compile)
[ ] All hyperlinks click and resolve correctly
[ ] No "(1)" / "_FINAL" / "v2" in filename
[ ] Spell-checked
[ ] Read aloud once
[ ] (Optional) Have someone else read it
[ ] PDF saved as Deva_Anand_Resume.pdf
[ ] Application logged in Applications/_Applications_Index.csv
```

---

## Step 7 — When you discover a new fact / win / metric

1. Open `Career_Brain_Dump.md`.
2. Add the fact in the right section (experience / project / achievement / skill).
3. Update the brain dump's changelog with date + one-line note.
4. *Then* (and only then) pull it into a tailored resume.

This single habit is what stops resume sprawl from coming back.

---

## Anti-patterns (do not do)

- Editing a tailored PDF/docx and treating it as the new source of truth.
- Saving 4 versions of the same resume in one folder (`v1`, `v2`, `_FINAL`, `(1)`).
- Copy-pasting a previous role-tailored resume and tweaking for a different company without re-pulling from the brain dump.
- Adding metrics or claims that aren't in `Career_Brain_Dump.md §6 Achievement Bank`.
- Using a tagline / summary / objective at the top.
- Using just "GitHub" or "LinkedIn" as link labels.
- Putting GitHub logos / FontAwesome icons in critical text.
- Mixing date formats (`Jul` with `May`).
- Three project bullets that all start with "Built".
- Comma splices.
- Naked specialized acronyms (`VAPT`, `DAG`, `DDPM`) without first-use spell-out.
- Listing a project that has no public GitHub repo, a private GitHub Classroom repo, or an empty/stub repo. If the recruiter can't open the link, it shouldn't be on the resume.

---

## Reference: project → JD-cluster fit (quick lookup)

When picking 3–4 projects for a JD, use this table. Eligibility column reflects the public-repo rule (Build Guide §5.6) — only ✅ projects can go on a resume. Cross-reference `Career_Brain_Dump.md` Appendix C for the canonical URL list.

| Project (brain dump §5) | Eligible? | Best JD signal it covers |
|---|---|---|
| AgenticSearch | ✅ | Multi-stage service, 150+ tests, fault tolerance, agentic AI tooling, retrieval/ranking |
| AutoEval | ✅ | Evaluation rigor, agentic systems, anti-Goodharting, reproducibility |
| Generative Models (CS 689) | ✅ | DL fundamentals, "from scratch in JAX", research credibility |
| KG2RAG-Enhanced | ✅ | RAG, multi-hop QA, ranking/fusion, knapsack/optimization |
| Spark ETL Performance Optimization | ✅ | Data platforms, query/storage, partitioning/broadcast joins, Spark UI |
| Sonare (Sign↔Speech) | ✅ | Edge ML, multimodal, on-device, cross-platform full-stack, hackathon |
| cf ai research scout | ✅ | Cloudflare Workers, edge-native, Durable Objects, WebSockets, D1, distributed asynchronous messaging |
| Alzheimer's Disease Classification | ✅ | Transfer learning, medical imaging — usually surfaced as Publication, not Project |
| refusal-decay | ✅ | AI safety / mechanistic interpretability / red-teaming |
| ngvi-curvature-variance | ✅ | ML / optimization / Bayesian DL research |
| autoresearch-karpathy | ✅ | Auto-research agent, GenAI for development productivity |
| Scalar-Tensor Autograd | ❌ (empty repo) | Would cover C++, DSA (DAG), algorithms (toposort), OO design — push code first |
| Cache- and SIMD-Aware Matrix Multiplication (CS 690PF) | ❌ (private) | Would cover C++, AVX SIMD, cache-aware tiling, OpenMP, perf — push public mirror first |
| Performance Engineering Reproduction Study (CS 690PF) | ❌ (private) | Would cover Coz, Hoard, Mytkowicz, perf c2c, Cachegrind, TMA — push public mirror first |
| LLM Inference Service | ❌ (no repo) | Would cover microservice, async batching, p95 latency — push code first |
| Distributed Training Simulator | ❌ (no repo) | Would cover distributed systems, sync overhead — push code first |

---

## Appendix — Files in this folder

- `Career_Brain_Dump.md` — single source of truth (13 sections; every claim traceable to a resume).
- `Resume_Customization_Workflow.md` — the original short workflow doc; this Build Guide supersedes it but the workflow doc is preserved for reference.
- `Resume_Build_Guide.md` — *this file*; the master playbook to follow on every new application.
