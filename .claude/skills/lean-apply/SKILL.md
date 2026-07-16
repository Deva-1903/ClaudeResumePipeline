---
description: Generate a lean, truthful tailored LaTeX resume from a pasted job description. Use when the user says lean apply mode, pastes a JD, or asks for a tailored resume.
argument-hint: "[job description]"
---

# Lean Apply Resume Skill

## Goal

Given a pasted JD, generate the strongest truthful one-page LaTeX resume for Deva Anand, compile it to PDF, archive the JD, write a `meta.json` generation record, update the skill-gap aggregator, and report a JD Fit Score in chat.

Default output folder: `applications/{YYYY-MM}/{Company}_{Role}_{YYYY-MM-DD}/` (applications are grouped into month subfolders by applied date)

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

## Role classification (drives tailoring emphasis, NOT which base file)

Every generated resume now uses ONE fixed base — the canonical dense-Charter template embedded in "Canonical template & fixed structure" below. Role classification no longer selects a different `.tex`; it only decides which truthful angle to emphasize inside that fixed template.

Pick exactly one bucket (used for `meta.json.role_bucket` and the skill-gap aggregator):

1. SDE / Backend / Platform
2. SRE / Systems / Infrastructure
3. ML Engineer / ML Systems
4. AI Engineer / LLM Engineer / Agentic AI / RAG
5. Applied Scientist / Research Intern / Research Engineer

(Secondary angles: Full-stack, Data/Systems/Infra, Security/Healthcare/Compliance, General SWE.) Use `context/06_role_targeting.md` "Ambiguous Role Rules" and "Broad SDE Internship Strategy" to break ties. For broad multi-track internships (Shopify-like: Software + Data + Applied ML + Infra + Security with ownership/quality/ambiguity language), default to SDE/Backend unless the JD is clearly ML/research/infra-specific.

## Canonical template & fixed structure (MANDATORY — supersedes old base selection)

The output is ALWAYS produced from the embedded template below. Write it verbatim into `applications/{folder}/Deva_Anand_{Company}.tex`, then tailor ONLY the parts listed under "Tailor" — nothing else.

### Hard structure rules (never violate)

- **Sections, in this exact order, no reordering and no additions:** Header, Education, Professional Experience, Projects, Publications, Skills, Open Source & Community. The final **Open Source & Community** section is the ONE removable section (optional lowest-priority fill block — see its rule below); no other section may be dropped, and none may be reordered or added.
- **Do NOT touch the template's visual layout**: margins, `bitstream-charter`/`mathdesign` font, header styling, `\section` styling + rule, `\linespread`, bullet indentation, entry macros (`\eduItem`, `\expItem`, `\projItem`, `\skillLine`, `\inlineBlock`). The generated resume must look identical to this base.
- **Header** — do not change name, email, phone, website, LinkedIn, or GitHub.
- **Education** — do not touch at all (degrees, schools, dates, coursework unchanged).
- **Publications** — do not touch (same text, same `(Paper)` link).
- **Open Source & Community — OPTIONAL, lowest-priority fill block (default: include):**
  - **Default: include it**, with the existing GirlScript + tutoring entries in their current order and wording.
  - **Drop the entire section** when a higher-signal truthful line fills the page better (an extra Wysa bullet, a current-role 3rd bullet, or Cario) **AND** the JD does not reward community / open source / mentorship / teaching / mission-impact.
  - **Always keep it** when the JD names community, open source, mentorship, teaching, or mission/impact — there it is a plus, not filler.
  - **Content is otherwise frozen:** never edit, reorder, or invent entries. The only allowed content change is optionally prepending the one-line **Underdogs Fitness** entry (see Underdogs guard).
  - **Underdogs guard:** the Underdogs one-liner is prepended here when Freelance is not shown as a full experience. If the section is dropped and Freelance is not shown as a full experience, promote Underdogs to a **full Freelance experience** for full-stack / product / payments JDs; otherwise Underdogs may be omitted.
  - When kept, it stays the last section, after Skills.
- **Professional Experience — flexible selection from a fixed pool (facts fixed; membership and counts flexible):**
  - Choose **3–4 experiences (default 3)** from the Experience pool below. Never invent a company, title, location, date, or bullet — every entry and claim traces to `01_verified_claims.md`.
  - **Always include Wysa** (the only quantified backend anchor).
  - **Include at least one current role** — TherAlign Health and/or CAM Lab (both current, both differentiating). Default shows both current roles + Wysa.
  - **Cario is optional** — include only when its REST-API / TS-migration backend evidence materially strengthens the specific JD (as a 4th entry, or by swapping out the weaker current role).
  - **Freelance / Open Source (Underdogs) is optional** — by default it moves to a one-line Open Source & Community entry; show it as a full experience only for full-stack / product / MERN / payments JDs.
  - **Bullet counts are flexible, not fixed:** each shown experience gets **2–3 bullets**, except **Wysa which may carry up to 4** (Cario 1–2; Freelance 1 if shown), for a total of **~6–9** experience bullets, tuned to fill exactly one page. Recent/primary roles get 3, secondary get 2. **Deepen Wysa (the quantified anchor) before padding elsewhere** — its 3rd/4th bullets (security/reliability, leadership/ownership, production debugging — all pre-written in the template comments) are usually the strongest fill available.
  - **Current-role truth guard:** TherAlign and CAM Lab bullets are **responsibility-framed only — NO metrics, no shipped-to-production, no adoption/clinical-validation claims** (per the truth notes in `01_verified_claims.md`). CAM Lab's verified code-facts (99 constructs / 38 questionnaires, the 40-test suite, the $600→$0–60/yr infra *plan*) may be stated as-is; do not add adoption numbers.
  - You may reword any bullet to mirror the JD (shift emphasis to backend / ML / systems / cloud / security / data / full-stack / healthtech / research), but never change a metric, its attribution, the company, or invent tools.
- **Projects — always exactly 3 projects, each with exactly 1 bullet.** Select the 3 most JD-relevant from the project pool below and reword the single bullet to the JD. Keep the `Name (link) … tech-stack-right` format.
- **Links** — `\href` with visible compact labels only (`GitHub`, `Demo`, `Website`, `Report`, `Paper`); never raw URLs, no icons, no colors, no underlines. One label per project title; if the title line overflows, move the label into that project's bullet instead. Only use links that exist in the pool below — never invent a URL.
- **Skills** — keep the 5-row label format and appearance; tailor the values/order to the JD (truthful skills only, no stuffing). The Cloud row must always keep `AWS, GCP, Azure`.
- One page, compiles clean. Experience membership and bullet counts are chosen per JD within the ranges above; the final resume must still be exactly one full page. Manage fit via experience/project selection, bullet wording, and the page-fill pass — never by shrinking the font, changing margins, or dropping a required element (Wysa, ≥1 current role, 3 projects).

### Tailor (the ONLY things you may change)

1. Which experiences appear (3–4 from the Experience pool, default 3; always Wysa + ≥1 current role) and the wording of each experience's 2–3 bullets, per the selection + count rules above.
2. Which 3 projects appear + the wording of each project's single bullet.
3. Skills row values and order.
4. Whether the Open Source & Community section appears at all (optional lowest-priority fill block — default include; drop per its rule above when a higher-signal truthful line fills the page better and the JD doesn't reward community/OSS/mentorship; always keep when the JD names community/OSS/mentorship/teaching/mission), and — when kept — optionally prepending the one-line Underdogs entry (added ONLY when Freelance is not shown as an experience).

Do NOT tailor Education, Publications, the Header, or any company name/title/date/location, and do NOT alter the template's macros or visual style. When Open Source & Community is kept, its content may change ONLY by adding the one allowed Underdogs line (never edit/reorder/invent other entries); the section itself may be dropped entirely per its rule above.

### Experience pool (choose 3–4; default 3; facts are fixed — never invent)

| Experience (as shown) | Title | Location | Dates | Bullets | Best for / notes |
|---|---|---|---|---|---|
| TherAlign Health | Founding Software Engineer Intern | Remote | Jul 2026 -- Present | 2–3 | **Current.** Healthtech, full-stack (Next.js), backend (Firebase/GCP), grounded/clinical AI, SMART on FHIR, RxNorm/Gemini. **Responsibility-framed, NO metrics.** |
| Culture \& Morality Lab, UMass Amherst | Lab Assistant | Amherst, MA | Jul 2026 -- Present | 2–3 | **Current.** ML/NLP (sentence-transformers, CCR), applied science / research, data/systems, backend (FastAPI), sole-ownership. **Pre-launch — verified code-facts only, no adoption metrics.** |
| Wysa | Backend Engineer | Bengaluru, India | Jul 2023 -- Jul 2025 | 2–4 | **Always include.** Backend, security, healthcare, full-stack, cloud. The quantified anchor (8+ clients, 10K+ submissions, $340K+, 60%, 20+ VAPT). Optional 3rd/4th bullets pre-written in the template: security/reliability, leadership/ownership + Copilot pilot, production debugging. |
| Cario Growth Services | Backend Developer Intern | Chennai, India | Nov 2022 -- May 2023 | 1–2 | **Optional.** REST-API backend, JS→TS migration, production LLM feature. Include when API-depth strengthens the JD. |
| Freelance / Open Source | Full-Stack Engineer | Remote | Jul 2022 -- Aug 2023 | 1 | **Optional.** Underdogs Fitness MERN + Stripe + cron, live 3+ yrs. **Default: demote to the one-line Open Source & Community entry**; show as a full experience only for full-stack/product/payments JDs. |

Selection order of operations: (1) always place Wysa; (2) add the current role(s) that fit the JD — TherAlign for healthtech/full-stack/backend/AI, CAM Lab for ML/NLP/research/data/systems (default both); (3) if a slot remains and Cario's API evidence helps, add Cario; (4) if Freelance is not shown, add its one-line Underdogs entry to Open Source & Community. Stay within 3–4 experiences and one page.

### Project pool (pick 3; use these exact links — do not invent)

| Project (title as shown) | Tech stack (right side) | Link label(s) → URL | Best for |
|---|---|---|---|
| AgenticSearch -- Provenance-First Entity Discovery | Python, FastAPI, OpenAI / Groq, SQLite | GitHub `https://github.com/Deva-1903/ciir_agentic_search` \| Demo `https://agentic-search-negglszkwa-uc.a.run.app` | AI/LLM/RAG, backend, agents |
| Refusal Decay -- LLM Safety / Mechanistic Interpretability | PyTorch, Llama-3.1-8B, AdvBench | GitHub `https://github.com/Deva-1903/refusal-decay` | Applied science, safety, research |
| KG2RAG-Enhanced -- Multi-Hop QA on HotpotQA | Python, Ollama / LLaMA-3, sentence-transformers, RRF | GitHub `https://github.com/Deva-1903/KG2RAG-685-NLP` | ML, RAG, IR, research |
| Spark ETL Performance Optimization | PySpark, Spark UI, SQL, NYC TLC Dataset | GitHub `https://github.com/Deva-1903/Spark-ETL-Optimization` | Data / systems / infra / performance |
| AutoEval -- Retrieval Evaluation Improvement Agent | Python, IR evaluation, Git automation | GitHub `https://github.com/Deva-1903/AutoEval` | AI eval, agents, research tooling |
| cf-ai-research-scout -- Edge-Native AI Assistant | TypeScript, Cloudflare Workers AI, Durable Objects, D1 | GitHub `https://github.com/Deva-1903/cf_ai_research_scout` | Full-stack, edge/systems, agents |
| Sonare -- Offline Sign / Speech App | React, Electron, FastAPI, MediaPipe, whisper.cpp | GitHub `https://github.com/Deva-1903/Qualcomm-Sep25-Team-Sonare` | Full-stack, edge ML, product |
| ngvi-curvature-variance -- Natural-Gradient VI Study | Python, PyTorch, NumPy | GitHub `https://github.com/Deva-1903/ngvi-curvature-variance` | Applied science, optimization, research |
| Cache- and SIMD-Aware Matrix Multiplication | C++, AVX/SIMD, OpenMP, Linux perf | GitHub `https://github.com/Deva-1903/cs690pf` | Systems / performance / low-latency C++ / HFT / database internals / SDE |
| align-ops -- LLM Post-Training + Serving Ops | PyTorch, TRL (SFT/DPO/GRPO), vLLM, FastAPI, Docker | (no public repo yet — list with NO link) | ML/AI infra, LLM post-training / RLHF, model serving, MLOps, distributed training, observability. **Has user-confirmed measured metrics (71% win-rate over base / 500 prompts, 54→72% accuracy, 1.9x throughput, 640 ms p95 TTFT, 52→84% GPU util) — see `01_verified_claims.md` align-ops results; no public repo link yet.** |

Link preference when a project has more than one URL: GitHub for code-heavy/backend roles, Demo/Website for product/full-stack roles, Report/Paper for research-heavy roles. AgenticSearch is the only pool entry with two labels — keep both only if the title line still fits, else drop Demo.

Every project bullet must trace to `context/04_project_bank.md` / `context/01_verified_claims.md`. Do not invent project outcomes, metrics, or links.

### Embedded template (write verbatim, then tailor per the rules above)

```latex
\documentclass[letterpaper,11pt]{article}

\usepackage[T1]{fontenc}
\usepackage[utf8]{inputenc}
\usepackage[bitstream-charter]{mathdesign}
\usepackage[top=0.17in,bottom=0.22in,left=0.38in,right=0.38in]{geometry}
\usepackage{titlesec}
\usepackage{enumitem}
\usepackage[hidelinks]{hyperref}
\usepackage{fancyhdr}
\usepackage[english]{babel}
\usepackage{tabularx}
\usepackage{array}
\usepackage[protrusion=true,expansion=false]{microtype}
\ifdefined\pdfgentounicode\input{glyphtounicode}\fi

\pagestyle{fancy}
\fancyhf{}
\renewcommand{\headrulewidth}{0pt}
\renewcommand{\footrulewidth}{0pt}
\setlength{\footskip}{12pt}

\urlstyle{same}
\raggedright
\setlength{\tabcolsep}{0in}
\linespread{0.97}
\ifdefined\pdfgentounicode\pdfgentounicode=1\fi

%----------SECTION STYLE: bold serif title + gap + full-width rule below----------
\titleformat{\section}
  {\large\bfseries}
  {}{0em}{}
  [\vspace{2pt}\titlerule]
\titlespacing*{\section}{0pt}{4pt}{2pt}

%----------LIST STYLE: small bullet, hanging indent, target line height----------
\renewcommand\labelitemi{$\vcenter{\hbox{\scriptsize$\bullet$}}$}
\setlist[itemize]{
  leftmargin=0.18in,
  labelsep=0.08in,
  itemsep=0pt,
  topsep=1.5pt,
  parsep=0pt,
  partopsep=0pt
}

%----------ENTRY COMMANDS----------
% Education: bold degree + school left, dates right
\newcommand{\eduItem}[3]{%
  \begin{tabular*}{\textwidth}{@{}l@{\extracolsep{\fill}}r@{}}
    \textbf{#1}, #2 & #3 \\
  \end{tabular*}\par
}

% Experience: Company (bold), Role, | Location (italic) left; Dates right
\newcommand{\expItem}[4]{%
  \vspace{2pt}
  \begin{tabular*}{\textwidth}{@{}l@{\extracolsep{\fill}}r@{}}
    \textbf{#1}, #2 \textit{| #3} & #4 \\
  \end{tabular*}\par\vspace{-3pt}
}

% Project: name (bold) left, tech stack right, same line
\newcommand{\projItem}[2]{%
  \vspace{2pt}
  \begin{tabular*}{\textwidth}{@{}l@{\extracolsep{\fill}}r@{}}
    \textbf{#1} & #2 \\
  \end{tabular*}\par\vspace{-3pt}
}

% Skills: bold label run-in
\newcommand{\skillLine}[2]{\textbf{#1:} #2\par\vspace{1.5pt}}

% Compact inline block with slight left indent (publications, open source & community)
\newcommand{\inlineBlock}[1]{{\setlength{\leftskip}{0.18in}\small #1\par}}

\begin{document}

%----------HEADING----------
\begin{center}
    {\fontsize{18}{20}\selectfont\bfseries DEVA ANAND}\\ \vspace{3pt}
    {\small
    \href{mailto:devaanand@umass.edu}{devaanand@umass.edu}
    \enspace$\bullet$\enspace
    (413) 315-1715
    \enspace$\bullet$\enspace
    \href{https://devaanand.com}{devaanand.com}
    \enspace$\bullet$\enspace
    \href{https://linkedin.com/in/devaaa/}{linkedin.com/in/devaaa}
    \enspace$\bullet$\enspace
    \href{https://github.com/Deva-1903}{github.com/Deva-1903}}
\end{center}
\vspace{-8pt}

%----------EDUCATION----------
\section{Education}
\eduItem{MS, Computer Science}{University of Massachusetts Amherst}{2025--2027}
{\small\textit{Advanced NLP, Advanced Machine Learning, Optimization in CS, Systems for Data Science, Performance Engineering}}\par
\vspace{3pt}
\eduItem{BE, Computer Science and Engineering}{Vels Institute of Science, Technology and Advanced Studies}{2019--2023}

%----------EXPERIENCE----------
\section{Professional Experience}

\expItem{TherAlign Health}{Founding Software Engineer Intern}{Remote}{Jul 2026 -- Present}
\begin{itemize}
  \item Founding engineer on a provider-facing \textbf{SMART on FHIR} clinical decision support app (Next.js + Firebase/GCP) that surfaces covered, guideline-backed medication alternatives in the EHR prescribing flow to prevent prior authorization.
  \item Extending a \textbf{Firebase Cloud Functions} backend that builds alternatives from \textbf{RxNorm} normalization, formulary/prior-auth logic, and PubMed/guideline evidence, with \textbf{Gemini} constrained to synthesis while the backend deterministically controls eligibility and coverage.
\end{itemize}

\expItem{Culture \& Morality Lab, UMass Amherst}{Lab Assistant}{Amherst, MA}{Jul 2026 -- Present}
\begin{itemize}
  \item Sole engineer building the lab's CCR (Contextualized Construct Representations) text-analysis platform (Python, \textbf{FastAPI}, sentence-transformers, React), productionizing a published NLP method into a self-serve web tool for researchers.
  \item Built a YAML model registry, a versioned construct library (\textbf{99 constructs from 38 questionnaires}), and a structured data-quality warning system; grew the backend suite to \textbf{40 tests} (hermetic CI).
\end{itemize}

\expItem{\href{https://www.wysa.io}{Wysa}}{Backend Engineer}{Bengaluru, India}{Jul 2023 -- Jul 2025}
\begin{itemize}
  \item Engineered a multi-tenant NHS eTriage backend (Node.js, MongoDB) for \textbf{8+ UK clinical clients}, processing \textbf{10{,}000+ monthly triage submissions} via Mayden iaptus REST integrations; contributed to \textbf{\$340K+} in revenue.
  \item Architected a full-stack ML training-data annotation platform (React, Node.js, MongoDB) used daily by the AI team, cutting manual annotation by \textbf{100+ hours/month} and lifting labeling throughput by \textbf{60\%}.
% Wysa 3rd/4th bullets — Wysa may carry up to 4 bullets (it is the quantified anchor; deepen it before padding elsewhere). Uncomment per JD, keeping one page:
% (security/reliability — for security/backend/healthcare JDs:)
% \item Owned backend security and reliability for the eTriage stack, implementing \textbf{AWS KMS} encryption for clinical PII, hardening authentication and rate limiting, and remediating \textbf{20+ VAPT findings} with regression-tested fixes.
% (leadership/ownership + AI-assisted dev — for ownership/mentorship-leaning JDs:)
% \item Served as primary technical point of contact for the eTriage backend; ran structured knowledge transfer that onboarded a second engineer to on-call readiness in \textbf{$\sim$6 weeks}, and piloted a COO-sponsored GitHub Copilot productivity experiment across migrations and tech-debt PRs.
% (production debugging — alternative 4th bullet for classic-SWE/debugging-heavy JDs:)
% \item Diagnosed and resolved production issues across tenants, monitoring logs during releases and client integrations and shipping targeted fixes for tenant-specific incidents to keep the multi-tenant eTriage service stable.
\end{itemize}

%----------PROJECTS----------
\section{Projects}

\projItem{AgenticSearch -- Provenance-First Entity Discovery {\normalfont\small(\href{https://github.com/Deva-1903/ciir_agentic_search}{GitHub} $\vert$ \href{https://agentic-search-negglszkwa-uc.a.run.app}{Demo})}}{Python, FastAPI, OpenAI / Groq, SQLite}
\begin{itemize}
  \item Built a multi-stage agentic web-discovery service turning open-ended queries into structured entity tables via typed retrieval planning, reranking, and deterministic extraction with LLM fallback and \textbf{cell-level provenance}; hardened with \textbf{150+ tests}.
\end{itemize}

\projItem{Refusal Decay -- LLM Safety / Mechanistic Interpretability {\normalfont\small(\href{https://github.com/Deva-1903/refusal-decay}{GitHub})}}{PyTorch, Llama-3.1-8B, AdvBench}
\begin{itemize}
  \item Studied how prefilling attacks weaken refusal in Llama-3.1-8B-Instruct, extracting the residual-stream refusal direction via difference-in-means (refusal \textbf{0.92$\to$0.32} at $k{=}3$) with causal patching, bootstrap 95\% CIs, and McNemar's test.
\end{itemize}

\projItem{KG2RAG-Enhanced -- Multi-Hop QA on HotpotQA {\normalfont\small(\href{https://github.com/Deva-1903/KG2RAG-685-NLP}{GitHub})}}{Python, Ollama / LLaMA-3, sentence-transformers, RRF}
\begin{itemize}
  \item Built the multi-view retrieval component of a KG-guided RAG pipeline (query-side decomposition, RRF fusion, cross-encoder reranking, MMR), lifting supporting-fact recall \textbf{+2.68\%} over the KG\textsuperscript{2}RAG baseline on a 4{,}905-question evaluation.
\end{itemize}

%----------PUBLICATIONS----------
\section{Publications}
\vspace{2pt}
\inlineBlock{- \textit{``Alzheimer's Disease Classification using Transfer Learning,''} IEEE CONIT 2023, first author, deep transfer learning on neuroimaging data. {\normalfont\small(\href{https://ieeexplore.ieee.org/document/10205760}{Paper})}}

%----------SKILLS----------
\section{Skills}
\skillLine{Languages \& Databases}{Python, TypeScript, JavaScript, C++, Java, SQL, Bash, MongoDB, PostgreSQL, SQLite}
\skillLine{Frameworks / Tools}{FastAPI, Node.js, Express, React, Docker, Git, GitHub Actions, Cloudflare Workers, REST APIs}
\skillLine{ML \& AI}{PyTorch, JAX, Hugging Face Transformers, sentence-transformers, LLM agents, RAG, MCP, evaluation}
\skillLine{Retrieval / Search}{RRF, cross-encoder reranking, MMR, knapsack token budgeting, Brave Search, cell-level provenance}
\skillLine{Cloud / Platforms}{AWS, GCP, Azure, Linux, MongoDB Atlas}

%----------OPEN SOURCE & COMMUNITY (OPTIONAL — lowest-priority fill block)----------
% Default: keep this whole section. Drop it entirely (delete the \section + \inlineBlock) only when a
% higher-signal truthful line fills the page better AND the JD doesn't reward community/OSS/mentorship/
% teaching/mission. Always keep it when the JD names those. If dropped and Freelance is not shown as a
% full experience, promote Underdogs to a full Freelance experience for full-stack/payments JDs (else omit).
\section{Open Source \& Community}
\inlineBlock{- Selected for \textbf{GirlScript Summer of Code 2023}; contributed to Linkfree, Freehit, and ProjectsHut. - Tutored \textbf{30+ underprivileged students} in programming at Sayur, a non-profit in Tamil Nadu.}
% Space permitting (see Experience pool rules), prepend the Underdogs one-liner when the section is kept and Freelance is not shown as an experience:
% - Built \textbf{Underdogs Fitness} (\href{https://www.underdogsfitness.in/}{Website}), a production MERN platform with Stripe payments; live \textbf{3+ years}.

\end{document}
```

## JD framing pass (MANDATORY)

After evidence is selected, before writing the resume, extract from the JD:

1. **Role family** — which of the five buckets, plus any secondary track angles.
2. **Employer priority themes** — ownership, quality, ambiguity, fast-paced execution, simple solutions to complex problems, debugging/research mindset, infra/platform scale, product thinking, AI-assisted development, security/reliability.
3. **Technical keywords** — APIs, distributed systems, pipelines, databases, ML models, data products, infra, security, plus company-stack keywords. Only surface keywords supported by the truth source.
4. **Behavioral / culture signals** — constant learner, takes ownership, enjoys research, quality-focused, resilient in ambiguity, uses AI tools effectively.

Then, while editing the copied resume in `applications/` — within the fixed structure only (section order is locked; see "Canonical template & fixed structure"):

A. Select 3–4 experiences from the Experience pool (default 3; always Wysa + ≥1 current role; Cario/Freelance optional per the selection rules) and reword each experience's bullets (2–3 each; Wysa up to 4) to echo JD language while preserving truth. Keep TherAlign and CAM Lab responsibility-framed (no metrics). Decide whether to keep the optional Open Source & Community section (default keep; drop when a higher-signal truthful line fills the page better and the JD doesn't reward community/OSS/mentorship/teaching/mission; always keep when the JD names those). If the section is kept and Freelance is not shown, add its one-line Underdogs entry; if the section is dropped and Freelance is not shown, promote Underdogs to a full Freelance experience for full-stack/payments JDs (else omit).
B. Select the 3 most JD-relevant projects from the pool and reword each project's single bullet; projects appear in JD-relevance order within the (fixed-position) Projects section.
C. Reorder/adjust the Skills row values so JD-relevant tools appear first (truthful skills only).
D. Make the resume feel written for this company/role — without inserting the company name unless natural.
E. Do NOT reorder sections or add sections, and do NOT touch Education, Publications, or the Header. The ONLY removable section is Open Source & Community (optional lowest-priority fill block — keep/drop per its rule); when kept, do not edit its entries beyond the one allowed Underdogs line.

Tailoring goal: **tailored AND identity-stable.** The reader should feel the resume was written for this role; but a side-by-side reader of two tailored versions should still recognize the same candidate, same claims, same scope descriptors, same metric attributions. Framing changes emphasis and vocabulary, NEVER the set of claims, the scope, or what a metric is attributed to. See `context/02_do_not_claim.md` "Tailoring stability" for the hard rules and `context/06_role_targeting.md` "Bullet rewriting examples" for the vocabulary-only rewrite pattern.

## Resume quality rules

- Stay one page in intent.
- Preserve the canonical template's preamble, custom commands, and visual style exactly (see "Canonical template & fixed structure").
- Use truthful verified evidence only.
- Be ATS-friendly without keyword stuffing.
- Prefer concrete engineering verbs.
- Prefer JD-relevant projects and bullets.
- Avoid vague filler.
- Avoid fake metrics, production claims, cloud/Kubernetes claims, or model-scale claims that aren't in the truth source.
- **Always-on Cloud row**: every tailored resume must surface `AWS, GCP, Azure` somewhere in the Skills row (in a Cloud / DevOps category), even when the JD does not mention cloud. The "do not claim cloud production ownership" rule still holds — these are listed as resume-safe skills only.
- **No em-dashes (`---`)** in bullet or item text. LaTeX renders `---` as an em-dash; use a comma instead. (LaTeX section-marker comments like `%----------SKILLS----------` are fine — they don't render.)

Allowed edits to the **copied file** in `applications/` (fixed structure — see "Canonical template & fixed structure"):
- Select which 3–4 experiences appear (from the Experience pool; default 3; always Wysa + ≥1 current role) and reword each experience's 2–3 bullets to the JD (counts flexible per the selection rules; TherAlign and CAM Lab stay responsibility-framed).
- Keep or drop the Open Source & Community section (optional lowest-priority fill block — default keep; drop only when a higher-signal truthful line fills the page better and the JD doesn't reward community/OSS/mentorship; always keep when the JD names community/OSS/mentorship/teaching/mission). When kept and Freelance is not shown as an experience, add the one-line Underdogs entry; if dropped and Freelance is not shown, promote Underdogs to a full Freelance experience for full-stack/payments JDs (else omit).
- Select which 3 projects appear (from the pool) and reword each project's single bullet; order them by JD relevance.
- Reorder/tailor the Skills row values (truthful skills only).
- Tighten or compress bullet wording without distorting meaning (a primary lever for one-page fit, alongside experience/project selection).
- Add JD-relevant keywords into Experience/Projects/Skills ONLY when supported by `01_verified_claims.md` or `03_skills.md`.

Forbidden (in addition to the fixed-structure rules):
- Showing fewer than 3 or more than 4 experiences, dropping Wysa, showing zero current roles, adding a company not in the Experience pool, exceeding 3 bullets on any experience, or using more/fewer than 3 projects.
- Adding metrics, shipped-to-production, or adoption/clinical-validation claims to the TherAlign or CAM Lab (current-role) bullets.
- Editing Education, Publications, or the Header, or editing Open Source & Community's entries beyond the one allowed Underdogs line (dropping the whole Open Source & Community section is allowed per its optional-fill rule; editing/reordering/inventing its entries is not).
- Reordering sections, adding sections, or removing any section other than the optional Open Source & Community block; changing margins, font, or macros.
- Raw URLs, invented links, icons, colors, or underlined links.
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

Folder pattern: `applications/{YYYY-MM}/{Company}_{Role}_{YYYY-MM-DD}/`
Resume file pattern: `Deva_Anand_{Company}.tex`

- Underscores, no spaces.
- Strip punctuation from company / role.
- Date format: YYYY-MM-DD using today's date.
- `{YYYY-MM}` is the month subfolder derived from the same date (create it if it does not exist yet).
- `{Company}` in the filename uses the same sanitized form as the folder (e.g., `JPMorgan_Chase`, `Uber`, `Shopify`).

Example folder + file: `applications/2026-05/Shopify_Software_Engineering_Intern_2026-05-08/Deva_Anand_Shopify.tex`

## Workflow

1. Parse the JD: extract company, role title, key requirements.
2. Run the JD framing pass: extract role family, priority themes, technical keywords, culture signals.
3. Classify role bucket (use `06_role_targeting.md` for tie-breakers; use the broad-internship strategy for Shopify-like JDs). This drives tailoring emphasis only — the base is always the canonical template.
4. Read required `context/` files in the order listed above.
5. Optionally inspect `reference_resumes/*.tex` for formatting/style only.
6. Read `04_project_bank.md` to pick and word the 3 JD-relevant projects (see the project pool).
7. **Write the embedded canonical template verbatim** to `applications/{YYYY-MM}/{Company}_{Role}_{YYYY-MM-DD}/Deva_Anand_{Company}.tex` (create the month subfolder if needed).
8. Tailor ONLY the allowed parts per "Canonical template & fixed structure": (a) select 3–4 experiences from the Experience pool (default 3; always Wysa + ≥1 current role) and reword each experience's bullets to the JD (2–3 each, Wysa up to 4; TherAlign/CAM Lab stay responsibility-framed, no metrics), (b) select the 3 most JD-relevant projects and reword each project's single bullet, (c) tailor the Skills row values/order, (d) decide whether to keep the optional Open Source & Community section (default keep; drop when a higher-signal truthful line fills the page better and the JD doesn't reward community/OSS/mentorship/teaching/mission; always keep when the JD names those) and, when kept, add the Underdogs one-liner if Freelance is not shown (if dropped and Freelance is not shown, promote Underdogs to a full Freelance experience for full-stack/payments JDs, else omit). Do NOT touch Education, Publications, the Header, section order, or the template macros; touch Open Source & Community's entries only via the one allowed Underdogs line (the section as a whole may be dropped per its optional-fill rule).
9. **Truth-audit pass** (see section above): re-audit every claim against the truth source as a skeptical fact-checker; fix every untraceable claim before continuing. Untraceable-remaining must be 0.
10. Compile the `.tex` to PDF using `tectonic` (command shown below). If compile fails, leave the `.tex` in place and surface the error in chat — do not retry blindly. After a successful compile, confirm the PDF is one page (command below). The default template is tuned to one full page (default: TherAlign 2 + CAM Lab 2 + Wysa 2 bullets); if the tailored version spills to a second page, tighten wording, drop an optional experience/bullet (Cario, Freelance, a current-role 3rd bullet), or trim within the count ranges — never shrink font/margins or drop a required element. See "Page-fill check".
11. **Independent scoring pass**: compute the JD Fit Score and Keyword match (rubrics below) against the final resume, scoring as an independent reviewer rather than the author.
12. Save the raw JD as `applications/{folder}/job_description.md`.
13. Write `applications/{folder}/meta.json` per the schema below (including `truth_audit` and `one_page`).
14. Update `tracking/skill_gaps.jsonl` — upsert one entry per `[factbase gap]` keyword, normalized via `tracking/aliases.md`. Do not aggregate `[resume gap]` or `[ignore]`.
15. **Sync to Notion** — run the `/sync-notion` procedure (see `.claude/skills/sync-notion/SKILL.md`) to upsert this application as a lean row in the `Summer 2026 Internship Applications` database (writes only Company, Position Title, Status, Date Applied, Match Score=`fit_score`). Status is score-gated: `Applied` if `fit_score >= 70`, else `Researching`. Then write the returned `notion` block back into this folder's `meta.json`. If the Notion MCP connection is unavailable, skip this step and note it in the final response (the row can be synced later with `/sync-notion`) — never fail the run over it.
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

## Page-fill / one-page check (MANDATORY, runs after compile)

The final PDF must be **exactly one page AND visually fill it like the base template** — dense and compact, ending close to the bottom margin. Projects (3 × 1 bullet) and the 5 skill rows are locked, but Experience is flexible (3–4 experiences, 2–3 bullets each within the pool rules). Page fill is managed by **experience/project selection, bullet counts within the allowed ranges, bullet wording, links, and tiny spacing — never by adding a 4th project, dropping a required element (Wysa, ≥1 current role, 3 projects), or changing font/margins.**

Target: no more than roughly **0.25in–0.35in** of unused vertical space after Open Source & Community. Measure the bottom gap (best-effort) from the application folder:

```
python3 - <<'PY'
from pypdf import PdfReader
r = PdfReader('Deva_Anand_{Company}.pdf'); ys=[]
r.pages[0].extract_text(visitor_text=lambda t,cm,tm,f,s: ys.append(tm[5]) if t.strip() else None)
h = float(r.pages[0].mediabox.height)
print('bottom gap ~', round(min(ys),1), 'pt (', round(min(ys)/72,2), 'in ) — aim <= ~0.35in incl. margin')
PY
```

If `pypdf` is unavailable, judge visually: content should reach near the bottom rule, with no obvious empty band under the last section (Open Source & Community when kept, otherwise Skills). If the page ends too high, the simplest fix is usually to keep the (default) Open Source & Community section rather than drop it — only drop it when a higher-signal line genuinely fills the space better.

### If it ends too high (underfilled) — fix naturally, in this priority order

1. **Re-select projects whose bullets naturally wrap to 2 lines** — prefer pool entries whose truthful bullet is fuller for this JD over ones that render as a single short line.
2. **Slightly expand the project bullets** with relevant, truthful technical detail already in `04_project_bank.md` / `01_verified_claims.md` (more specific tools, methods, or a verified metric) — no new claims.
3. **Add a bullet or an experience within the allowed ranges** — deepen Wysa first (its pre-written 3rd/4th bullets: security/reliability, leadership/ownership, production debugging), then give a current role a 3rd bullet, add Cario, or show Freelance as a full experience — using only truthful detail from `05_bullet_bank.md` / `01_verified_claims.md` (stay within 3–4 experiences; 2–3 bullets each, Wysa up to 4; current roles responsibility-framed).
4. **Add or preserve visible link labels** (`GitHub`, `Demo`, `Website`, `Report`, `Paper`) where a real URL exists in the pool — these add a line's worth of width/parity and value.
5. **Increase tiny vertical spacing only subtly** — e.g. `+0.5pt` to `+1pt` on `\projItem`'s `\vspace` (between project blocks) or a section's `titlespacing` "before". This is the last resort and must stay subtle.

Never create fake whitespace or artificial empty gaps. Never enlarge the header or section headings, add new sections, exceed the experience ranges (4 experiences; 3 bullets each, Wysa 4), add a 4th project, or rewrite Education / Publications to fill space. (Keeping the optional Open Source & Community section — the default — is a legitimate fill choice, but do not edit its entries beyond the one allowed Underdogs line to pad space.) Do not change margins to fill space unless absolutely necessary.

### If it overflows to a 2nd page — tighten, in this priority order

1. **Tighten the project bullets** slightly (shorter phrasing, drop a low-signal clause).
2. **Tighten the experience bullets** slightly (same, truth preserved).
3. **Drop the optional Open Source & Community section** if the JD does not reward community/OSS/mentorship/teaching/mission and the freed space is better spent on higher-signal content (apply the Underdogs guard: if Freelance is not shown as a full experience, promote Underdogs to a full Freelance experience for full-stack/payments JDs, else omit). If the JD does reward those signals, keep the section and tighten elsewhere.
4. **Drop an optional experience or bullet** — remove Cario, show Freelance as a full experience only where warranted, or trim a Wysa 4th/3rd or current-role 3rd bullet (stay ≥3 experiences with Wysa + ≥1 current role, each ≥2 bullets).
5. **Reduce the tiny spacing adjustments** (undo any `\vspace` bumps first).
6. If a project title line with a link label overflows, move that label into the project's bullet (per the link rules).

Never shrink the font, never change margins, never delete a required element (Wysa, ≥1 current role, 3 projects), and never exceed the experience ranges. Recompile and re-confirm exactly one page after any change.

### Final visual check

Dense, compact, and full like the base template — no obvious empty band at the bottom, and not stretched or artificially spaced. "One page but half-empty" and "one page but padded" are both failures.

## meta.json schema

```json
{
  "company": "Uber",
  "role": "Software Engineer Intern",
  "applied_date": "2026-05-09",
  "base_used": "dense_charter (canonical template)",
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
  "revisions": [],
  "notion": { "page_id": "<notion page id>", "url": "<notion page url>", "synced_at": "<ISO 8601>", "action": "created" }
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
- `notion` is written by the Notion sync step (step 16) and links this folder to its row in the `Summer 2026 Internship Applications` database. It makes re-syncs idempotent. Absent until the first successful sync.
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

### Score calibration (mandatory, applied last)

The fit score is a judgement, not an applause meter. Apply these caps as the final step before writing `meta.json`:

- **Cap at 84 (Submit, not Strong Submit) if any JD must-have keyword is a `factbase gap`.** A Strong Submit means every must-have is truthfully covered. A real skill hole in the must-haves caps the score regardless of narrative fit.
- **If `fit_score` exceeds `keyword_match.percent` by more than 20 points, write a one-line `score_rationale` field in `meta.json` justifying the gap** (e.g. "narrative fit strong; JD lists 8 named tools, 3 nice-to-haves missing"). The divergence is allowed; the unexplained divergence is not.
- **Round borderline scores DOWN, not up.** An 85 is a claim a hiring screener would call this Strong Submit; if you would not bet on that, score 84.

### Gap classification (chat-only)

Classify each gap into one of three labels:

For each missing keyword: BEFORE labeling `factbase gap`, search `01_verified_claims.md`, `03_skills.md`, `04_project_bank.md`, `05_bullet_bank.md`, and the brain dump for the keyword (or an alias). If a backing claim exists in the truth source but you did not surface it on the resume, the correct label is `resume gap`, NOT `factbase gap`. Defaulting everything to `factbase gap` is a known failure mode that hides under-inclusion.

- **resume gap** — claim IS in the truth source but did not make it onto this resume. Action: regenerate or adjust to surface it (often a one-bullet swap).
- **factbase gap** — claim is missing from the truth source too. Real skill / project gap. Action: build or learn it later.
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

- Base used: canonical dense-Charter template (fixed structure)
- Output: `applications/<folder>/Deva_Anand_<Company>.tex` + `.pdf` — 1 full page, truth audit clean (`N` claims, 0 untraceable) (or note compile failure / page overflow / audit fixes made)
- Projects chosen: the 3 selected (of the pool), in JD-relevance order
- JD Fit Score: `XX/100 — Strong Submit | Submit | Maybe | Weak Fit`
- Keyword match: `X/Y (NN%)`
- Strong matches: 2–3 short phrases
- Missing keywords: up to 5 short phrases, each tagged `[resume gap]`, `[factbase gap]`, or `[ignore]`
- Aggregator: short note like `+3 factbase-gap keywords logged to tracking/skill_gaps.jsonl` (or `0 logged` if all gaps were already counted)
- Avoided: **mandatory** one-line note on what was deliberately left out (a bullet, a project, a skill row category) — write "nothing notable" if there genuinely was none, but never omit the line

No long reasoning. No JD analysis prose. No mapping table. No files beyond those listed in the goal section.
