# Organization Report (Dry-Run)

> **Status:** DRY-RUN — only non-destructive analysis files have been created so far. **No resume PDFs have been copied or moved by this pass.** File copies (Phases 3, 4, 5 of your spec) are awaiting your explicit approval.
>
> **Date:** 2026-05-07
>
> **Prepared in response to:** your "PHASE 1 → PHASE 9" detailed instructions.

---

## What's already been done (non-destructive)

| Phase | Output | Path | Status |
|---|---|---|---|
| 1 | File inventory CSV | `Career_Materials/05_Indexes_And_Logs/Resume_Index.csv` | ✅ Created (35 rows) |
| 2 | Empty folder structure | `Career_Materials/{00..99}/` | ✅ Created |
| 6 | Extracted text for every PDF | `Career_Materials/04_Extracted_Text/*.txt` | ✅ 29 files (every PDF parsed) |
| 6 | Unreadable-files log | `Career_Materials/05_Indexes_And_Logs/Unreadable_Files.md` | ✅ Empty (none unreadable) |
| 7 | Master career brain dump | `Career_Materials/01_Master_Brain_Dump/Career_Brain_Dump.md` | ✅ Created (13 sections) |
| 8 | Future-customization workflow | `Career_Materials/01_Master_Brain_Dump/Resume_Customization_Workflow.md` | ✅ Created |
| 9 | This report | `Career_Materials/05_Indexes_And_Logs/Organization_Report.md` | ✅ Created |

## What's pending your approval

| Phase | Action | Why pause |
|---|---|---|
| 3 | Copy every Deva-authored resume + cover letter into `Career_Materials/99_Original_Backup/` | First file-copy operation; want your sign-off before touching files. |
| 4 | Copy the latest 6 resumes into `Career_Materials/00_Latest_6_Resumes/` (renamed clearly, originals untouched) + write README.md inside it | Same — file-copy. |
| 5 | Copy remaining resumes into `02_Resume_Bank/{General, Role_Specific, Company_Specific}` and `03_Archived_Resumes/By_Year/{2025,2026}` with clear renamed copies | Same — file-copy. |

---

## Summary numbers

| Metric | Count |
|---|---|
| Total files scanned | **35** (under `/Resume/`, excluding `.DS_Store`) |
| Deva-authored resume PDFs | **24** |
| Cover letters (PDF) | **5** |
| Source files (.tex / .log) | **4** |
| Other people's resumes | **0** *(was 3 in earlier pass — no longer present in the folder; user may have removed them outside of this session)* |
| Calendar files (`.ics`) | **1** (Amazon DTP — left in place, not a resume) |
| Markdown brain-dump files | **1 existing** (`Career_Master_Document.md`) **+ 2 new** in `01_Master_Brain_Dump/` |
| PDFs that were unreadable | **0** |
| Possible duplicates flagged | **3 pairs** (see below) |
| Major inconsistencies identified | **11** (see Career_Brain_Dump §11) |

---

## Latest 6 resumes selected (by file modified date)

> Per your rule: use file-modified date unless the filename contains a clearly newer date. None of these filenames carry a date that overrides their mtime, so mtime wins.

| # | File | Modified | Tailored for | Current path |
|---|---|---|---|---|
| 1 | `Deva_Resume_coreAI.pdf` | 2026-04-30 18:52 | Microsoft Core AI | `Latest_6/` |
| 2 | `Deva_Resume (1).pdf` | 2026-04-30 18:43 | Generic / latest catch-all | `Latest_6/` |
| 3 | `Deva_Resume_Adobe_ML.pdf` | 2026-04-26 20:40 | Adobe ML | `Latest_6/` |
| 4 | `Deva_Anand_Resume_Adobe_ML_Intern.pdf` | 2026-04-26 16:37 | Adobe ML Intern | `Latest_6/` |
| 5 | `Deva_Resume.pdf` | 2026-04-26 16:27 | Generic SWE / Applied ML | `Latest_6/` |
| 6 | `Deva_Resume_SDE.pdf` | 2026-04-22 17:18 | SDE / Backend / Full-Stack | `Latest_6/` |

> **Companion source files** in `Latest_6/` (not counted in the "6 resumes" — they're build artifacts):
> - `Deva_Anand_Resume_Adobe_ML_Intern.tex` + `.log` (LaTeX source + build log)
> - `Deva_Resume_Microsoft_CoreAI.tex` (LaTeX source for `Deva_Resume_coreAI.pdf`)

---

## Files that could not be read

**None.** All 29 PDFs (24 resumes + 5 cover letters) extracted cleanly via `pdftotext -layout`.

---

## Possible duplicates / near-duplicates

| Pair | Reason | Recommendation |
|---|---|---|
| `By_Role/SDE_Backend/Deva_Anand_Resume.pdf` ↔ `By_Role/SDE_Backend/Deva_Resume_SRE.pdf` | Identical byte count (220 089 B); identical extracted text | Keep both for now; verify with `cmp` before deciding to drop one. |
| `By_Role/Older_Versions/Deva_Resume_FullStack_Dec10.pdf` ↔ `By_Role/Older_Versions/Deva_Resume_FullStack_Jan19_dup.pdf` | MD5-identical (`8fb2f8758877020c1e540851bc2e2b7b`) | True duplicate. Per your "do not delete" rule, will not delete; flagged for your manual cleanup if desired. |
| `Latest_6/Deva_Resume_Adobe_ML.pdf` ↔ `Latest_6/Deva_Resume (1).pdf` | Body text near-identical; same tagline; possibly the "(1)" version is a re-download | Verify; if same, retire the "(1)" copy by manually deleting it later. |

---

## Major inconsistencies found

Captured fully in `Career_Brain_Dump.md §11`. Highlights:

1. **Wysa client count drift:** "6+ UK clients" (early) vs "8+ UK clients" (later) — pick one.
2. **Wysa city spelling:** "Banglore" → "Bengaluru" in newer.
3. **Cario LLM phrasing:** four distinct phrasings (integration / fine-tune / auto-comment / supporting features). Lock one.
4. **Annotation-platform framing:** four variants ("ML training-data" / "data" / "data and review" / "primary data labeling platform").
5. **Freelance role title:** four variants.
6. **Tagline drift:** 13 distinct taglines across resumes.

---

## Recommended next actions

### Immediate (need your approval)
1. **Approve Phase 3 backup** — produce `99_Original_Backup/` containing copies of every PDF. Lossless safety net.
2. **Approve Phase 4** — copy the Latest 6 into `00_Latest_6_Resumes/` and write its README.md (keeps the existing `Latest_6/` folder untouched as the live working set, while `00_Latest_6_Resumes/` becomes a frozen "as of 2026-05-07" snapshot inside `Career_Materials/`).
3. **Approve Phase 5** — populate `02_Resume_Bank/General_Resumes/`, `Role_Specific_Resumes/`, `Company_Specific_Resumes/` and `03_Archived_Resumes/By_Year/{2025,2026}/` with clearly renamed copies (format: `YYYY-MM-DD__Company__Role__Resume.pdf`).

### After approval
4. **Resolve §11 inconsistencies** — pick canonical phrasings; update `Career_Brain_Dump.md` to mark "canonical" vs "alternate" in each section.
5. **Backfill metric gaps** — see brain dump §12 for the prioritized list (LLM Inference Service p95, Spark ETL %, Sonare hackathon placement, etc.).
6. **Set up `Applications/` parent folder** at `/Resume/Applications/` (separate from `Career_Materials/`) per `Resume_Customization_Workflow.md`, with `_Applications_Index.csv` initialized.
7. **Manually delete the two duplicate file pairs** from your Mac (filesystem permissions blocked deletion from this session). Specifically:
   - `By_Role/Older_Versions/Deva_Resume_FullStack_Jan19_dup.pdf` (MD5 dup of Dec10).
   - Optionally one of `Deva_Anand_Resume.pdf` / `Deva_Resume_SRE.pdf` after you've verified they're identical.
   - `Resumes/` and `Resumes/Full Stack/` empty leftover folders + their `.DS_Store` files.

---

## Proposed Phase 3 — Backup mapping (preview)

When you approve, the following copies will be made into `Career_Materials/99_Original_Backup/`. Original folder structure preserved.

```
99_Original_Backup/
├── Latest_6/
│   ├── Deva_Resume (1).pdf
│   ├── Deva_Resume.pdf
│   ├── Deva_Resume_Adobe_ML.pdf
│   ├── Deva_Resume_SDE.pdf
│   ├── Deva_Resume_coreAI.pdf
│   ├── Deva_Anand_Resume_Adobe_ML_Intern.pdf
│   ├── Deva_Anand_Resume_Adobe_ML_Intern.tex
│   ├── Deva_Anand_Resume_Adobe_ML_Intern.log
│   └── Deva_Resume_Microsoft_CoreAI.tex
├── By_Role/
│   ├── ML/                    (5 files)
│   ├── SDE_Backend/           (4 files)
│   ├── Research_CIIR/         (3 files)
│   ├── Cloudflare/            (1 file)
│   └── Older_Versions/        (7 files)
└── Cover_Letters/             (5 files)
```

Total backup: **38 files** (24 resumes + 5 cover letters + 4 source files + 5 archive PDFs already inside Older_Versions).

## Proposed Phase 4 — Latest_6 mapping (preview)

```
00_Latest_6_Resumes/
├── README.md                                         (auto-generated — see preview below)
├── 2026-04-30__Microsoft__CoreAI__Resume.pdf         (← Deva_Resume_coreAI.pdf)
├── 2026-04-30__General__LatestCatchAll__Resume.pdf   (← Deva_Resume (1).pdf)
├── 2026-04-26__Adobe__ML__Resume.pdf                 (← Deva_Resume_Adobe_ML.pdf)
├── 2026-04-26__Adobe__MLIntern__Resume.pdf           (← Deva_Anand_Resume_Adobe_ML_Intern.pdf)
├── 2026-04-26__General__SWEAppliedML__Resume.pdf     (← Deva_Resume.pdf)
└── 2026-04-22__General__SDEBackendFullStack__Resume.pdf (← Deva_Resume_SDE.pdf)
```

> Originals will not be renamed. Only the copies in `00_Latest_6_Resumes/` get the cleaner naming.

## Proposed Phase 5 — Resume_Bank + Archive mapping (preview)

```
02_Resume_Bank/
├── General_Resumes/
│   ├── 2026-04-26__General__SWEAppliedML__Resume.pdf      (← Latest_6/Deva_Resume.pdf — also in Latest_6 — same file copied twice on purpose)
│   ├── 2026-04-30__General__LatestCatchAll__Resume.pdf    (← Latest_6/Deva_Resume (1).pdf)
│   └── 2025-11-21__General__Earliest__Resume.pdf          (← Older_Versions/Deva_Resume_Nov21.pdf)
├── Role_Specific_Resumes/
│   ├── 2026-04-22__General__SDEBackendFullStack__Resume.pdf  (← Latest_6/Deva_Resume_SDE.pdf)
│   ├── 2026-04-22__General__SREBackend__Resume.pdf           (← By_Role/SDE_Backend/Deva_Resume_SRE.pdf)
│   ├── 2026-04-22__General__BackendInfraDistributed__Resume.pdf (← By_Role/SDE_Backend/Deva_Anand_Resume.pdf)
│   ├── 2026-04-20__General__MLAgenticAI__Resume.pdf          (← By_Role/ML/Deva_Resume_ML.pdf)
│   ├── 2026-04-08__General__MLE__Resume.pdf                  (← By_Role/ML/Deva_Resume_V2.pdf)
│   ├── 2026-03-26__General__MLE_v1__Resume.pdf               (← By_Role/ML/Deva_Resume_ML_v1.pdf)
│   ├── 2026-03-25__General__MLE_v0__Resume.pdf               (← By_Role/ML/Deva_Resume_v1.pdf)
│   ├── 2026-03-26__General__SDEBackendSystems__Resume.pdf    (← By_Role/SDE_Backend/Deva_Resume_SDE_v1.pdf)
│   └── 2026-03-24__General__SDEFullStack__Resume.pdf         (← By_Role/SDE_Backend/Deva_Resume_SDE_FullStack_FINAL.pdf)
├── Company_Specific_Resumes/
│   ├── 2026-04-30__Microsoft__CoreAI__Resume.pdf          (← Latest_6/Deva_Resume_coreAI.pdf)
│   ├── 2026-04-26__Adobe__ML__Resume.pdf                  (← Latest_6/Deva_Resume_Adobe_ML.pdf)
│   ├── 2026-04-26__Adobe__MLIntern__Resume.pdf            (← Latest_6/Deva_Anand_Resume_Adobe_ML_Intern.pdf)
│   ├── 2026-03-29__Cloudflare__SWEIntern__Resume.pdf      (← By_Role/Cloudflare/Deva_Resume_CF_v1.pdf)
│   ├── 2026-03-26__UMassCIIR__SWE__Resume.pdf             (← By_Role/Research_CIIR/Deva_CIIR_AIX_Resume.pdf)
│   ├── 2026-03-26__UMassCIIR__SWE_v2__Resume.pdf          (← By_Role/Research_CIIR/Deva_CIIR_AIX_Resume_v2.pdf)
│   ├── 2026-01-15__PayPal__BackendFullStack__Resume.pdf   (← Older_Versions/Deva_Resume_PayPal.pdf)
│   └── 2026-01-19__Verkada__BackendDistributed__Resume.pdf (← Older_Versions/Deva_Resume_Verkada.pdf)
└── (Cover letters stay in Cover_Letters/ but ALSO get a copy here under Company_Specific_Resumes/ if you want — please confirm)

03_Archived_Resumes/By_Year/
├── 2025/
│   ├── 2025-11-21__General__Earliest__Resume.pdf         (← Older_Versions/Deva_Resume_Nov21.pdf)
│   ├── 2025-12-10__General__FullStack__Resume.pdf        (← Older_Versions/Deva_Resume_FullStack_Dec10.pdf)
│   └── 2025-12-15__General__MLDataPlatforms__Resume.pdf  (← Older_Versions/Deva_Resume_ML_Dec15.pdf)
└── 2026/
    └── (every other PDF, with YYYY-MM-DD__Company__Role__Resume.pdf naming)

03_Archived_Resumes/Unknown_Date/
└── (none — every file has a clear modified date)
```

> **Question for you:** Do you want me to also create renamed cover-letter copies under `02_Resume_Bank/Company_Specific_Resumes/` (alongside the resumes for those companies) so each application has its resume + CL co-located? Or keep cover letters strictly in the existing `Cover_Letters/` folder + a backup copy in `99_Original_Backup/`?

---

## Verification: how I'll prove I haven't deleted/overwritten anything

After Phases 3–5 run, I will:

1. Re-run `find /Resume -type f ! -name '.DS_Store' | wc -l` and `md5sum` every original to confirm none were modified.
2. Append a "Phase 3–5 execution log" section to **this report** with the before/after file count + an MD5 manifest of all originals.
3. Confirm `99_Original_Backup/` md5s match `Latest_6/`, `By_Role/`, `Cover_Letters/` md5s file-for-file.

If any md5 changes, I will halt and flag it.

---

## Approval needed

Please reply with one of:

- **"Approved — proceed with Phases 3, 4, 5"** → I'll run the copies, then update this report with the execution log.
- **"Approved with changes"** → tell me what to change in the proposed mapping above and I'll re-issue the dry-run.
- **"Hold — review brain dump first"** → I'll wait while you read `Career_Brain_Dump.md` and adjust.
