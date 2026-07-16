---
description: Compile an existing tailored resume .tex (Deva_Anand_{Company}.tex) into PDF only when explicitly requested.
argument-hint: "[path to Deva_Anand_{Company}.tex]"
---

# Compile Resume Skill

## Goal

Compile an existing tailored resume `.tex` file (named `Deva_Anand_{Company}.tex` under `applications/<folder>/`) into PDF.

Use only when the user explicitly asks to compile, generate PDF, or invokes /compile-resume.

## Rules

- Do not tailor or rewrite the resume unless explicitly asked.
- Do not create Notes.md.
- Do not create Job_Description.md.
- Do not create jd_snapshot.md.
- Do not create interview prep.
- Only compile the specified .tex file.
- If no path is provided, ask for the path or infer the most recent `applications/{YYYY-MM}/*/Deva_Anand_*.tex` only if obvious (applications are grouped into month subfolders).
- Keep final response short.

## Output

Generate PDF in the same folder as the .tex file. PDF filename matches the .tex stem (e.g., `Deva_Anand_Uber.pdf`).

Final response:
- PDF path
- Any compile warning/error that matters
