# Resume Customization Workflow

> **Last updated:** 2026-05-07
>
> **Purpose:** Stop the resume sprawl. Make every tailored resume a clean, traceable output of `Career_Brain_Dump.md` instead of a fork of a previous tailored resume.

---

## Core principles

1. **`Career_Brain_Dump.md` is the source of truth.** Every claim, bullet, metric, and project on a tailored resume must already exist in the brain dump. If you're tempted to add something new, **add it to the brain dump first**, then pull from the brain dump into the resume.
2. **Tailored resumes are outputs, not source.** Never edit a tailored resume directly to "save a new fact for later." That fact will get lost. Update the brain dump.
3. **One folder per application.** Don't dump 12 resumes for 12 jobs into one folder again. Use the structure below.
4. **No copy-pasting from old tailored resumes.** Always re-pull from the brain dump. Old phrasings drift; fresh pulls stay aligned with truth.
5. **Truthfulness check.** Every bullet you add must already appear in the brain dump *and* match how you'd describe the work in an interview.
6. **Don't randomly duplicate.** Avoid `Resume_v2.pdf`, `Resume (1).pdf`, `Resume_FINAL.pdf` patterns inside an application folder. Inside the per-application folder, keep one tailored `.docx` and one tailored `.pdf`.

---

## Future structure

```
Applications/
├── 2026-05-08__Stripe__BackendIntern/
│   ├── Job_Description.md          ← copy-paste of the JD + URL + salary if listed
│   ├── Tailored_Resume.docx        ← active editing copy
│   ├── Tailored_Resume.pdf         ← exported for submission
│   └── Notes.md                    ← interview notes, recruiter contact, follow-ups
├── 2026-05-12__Anthropic__MLEngineer/
│   ├── Job_Description.md
│   ├── Tailored_Resume.docx
│   ├── Tailored_Resume.pdf
│   └── Notes.md
└── _Applications_Index.csv         ← log every application here
```

`Applications/` lives **next to** `Career_Materials/` (i.e. inside `/Resume/`), not inside it. That keeps source-of-truth content (`Career_Materials/`) cleanly separated from per-application artifacts.

### Folder naming convention

`YYYY-MM-DD__Company__Role/`

- `YYYY-MM-DD` = the date you applied (or the date you started tailoring, if the application is multi-step).
- `Company` = official company name, no abbreviations the future-you won't recognize. PascalCase or no spaces.
- `Role` = the role title (no whitespace; use camelCase or PascalCase). Example: `BackendIntern`, `MLEngineerNewGrad`, `SREIntern`.

### Contents of each per-application folder

- **Job_Description.md** — The full JD. Copy-paste from the posting; include the source URL at top and the date you saved it. If the posting is taken down later, you'll still have the text.
- **Tailored_Resume.docx** — The .docx version you're actively editing. Use this as the active source for tweaks.
- **Tailored_Resume.pdf** — Exported PDF for submission. Re-export every time you make material edits; don't keep stale PDFs.
- **Notes.md** — Free-form: recruiter name, application portal, status updates ("recruiter call 2026-05-15"), interview prep notes, postmortem after the loop.

---

## Step-by-step workflow per application

### 0. Before opening anything

- [ ] Re-read `Career_Brain_Dump.md`'s **§13 Best Resume Material** so the strongest assets are top-of-mind.

### 1. Save the job description

- [ ] Make the application folder: `Applications/YYYY-MM-DD__Company__Role/`.
- [ ] Create `Job_Description.md` with:
  - Source URL
  - Date saved
  - Full JD text (copy-paste)
  - Salary band if listed
  - Key required-skills list at top
  - Visa / sponsorship language if any

### 2. Identify target role

- [ ] In `Job_Description.md`, list the top **5–8 keywords** the JD repeats.
- [ ] Match those keywords to the closest persona in `Career_Brain_Dump.md` **§2 Target Roles** (e.g., MLE, Backend, Full-Stack, IR/RAG, LLM Systems, Edge ML).
- [ ] Pick the matching tagline from §1 of the brain dump.

### 3. Pick relevant skills from the brain dump

- [ ] From **§3 Skills Bank**, pull the subset the JD asks for. Do **not** carry over skills the JD doesn't ask for unless they're foundational.
- [ ] From **§10 ATS keyword bank**, pick the keyword cluster matching this role.

### 4. Pick strongest matching bullets

- [ ] From **§7 Resume Bullet Bank**, pick 2–3 bullets per experience that best match the JD keywords.
- [ ] Reach for the verbatim phrasings — they're already battle-tested. Tweak only verbs/connectors, not the underlying claims.
- [ ] From **§5 Project Bank**, pick 2–4 projects ranked by the "Best fit for" tags.

### 5. Build the tailored resume

- [ ] Start from the closest of the **Latest_6** as a layout template (see `00_Latest_6_Resumes/README.md` for the role-by-role recommendation).
- [ ] Open the .docx; replace tagline → skills order → experience bullets → project list → keep undergrad in/out per role conventions.
- [ ] Add only truthful experience. If a JD asks for something not in the brain dump, **do not add it**. Add a "Skills I'm not claiming" note in `Notes.md` instead.
- [ ] Page-count check: 1 page for internships unless the role explicitly allows 2.

### 6. Final pass

- [ ] ATS check: real text in headers, no images-of-text, no exotic columns/tables.
- [ ] Read aloud — if a sentence sounds inflated, soften it.
- [ ] Check every metric against `§6 Achievement Bank`. If a metric isn't there, don't claim it.

### 7. Export

- [ ] Save Tailored_Resume.docx.
- [ ] Export Tailored_Resume.pdf.
- [ ] Re-open the PDF in a viewer to confirm rendering.

### 8. Log the application

- [ ] Open `Applications/_Applications_Index.csv`.
- [ ] Add a new row: `Date, Company, Role, JD URL, Folder, Status, Date_Applied, Recruiter, Outcome`.
- [ ] Status starts as `Drafted` → `Submitted` → `Recruiter Screen` → `Tech Screen` → `Onsite` → `Offer / Reject / Ghosted`.

---

## Quick checklist (printable)

```
[ ] Saved JD to Job_Description.md (with URL + date)
[ ] Listed top JD keywords
[ ] Identified matching persona from brain dump §2
[ ] Picked tagline from brain dump §1
[ ] Pulled relevant skills from brain dump §3
[ ] Pulled 2–3 bullets per experience from §7
[ ] Picked 2–4 projects from §5
[ ] Added only truthful experience (cross-checked §6 Achievement Bank)
[ ] ATS pass (text headers, no images-of-text)
[ ] Read aloud, softened inflated phrasing
[ ] Exported Tailored_Resume.pdf
[ ] Re-opened PDF to verify rendering
[ ] Logged in Applications/_Applications_Index.csv
[ ] Started Notes.md for follow-ups
```

---

## What you will NOT do anymore

- ❌ Edit a tailored PDF/docx and treat it as the new source of truth.
- ❌ Save 4 versions of the same resume (`v1`, `v2`, `_FINAL`, `(1)`) inside one folder.
- ❌ Copy a previous role-tailored resume and tweak it for a different company without re-pulling from the brain dump.
- ❌ Add metrics or claims you can't trace to **Career_Brain_Dump.md §6 Achievement Bank**.
- ❌ Mix tailored outputs into `Career_Materials/`. That folder is read-only source-of-truth.

---

## When you discover a new fact / win / number

1. Open `Career_Materials/01_Master_Brain_Dump/Career_Brain_Dump.md`.
2. Add the fact in the right section (experience, project, achievement, etc.).
3. Update the changelog with date + one-line summary.
4. *Then* (and only then) pull it into a tailored resume.

That single rule is what stops resume sprawl.
