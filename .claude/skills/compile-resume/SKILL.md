---
description: Compile an existing Tailored_Resume.tex into PDF only when explicitly requested.
argument-hint: "[path to Tailored_Resume.tex]"
---

# Compile Resume Skill

## Goal

Compile an existing Tailored_Resume.tex into PDF.

Use only when the user explicitly asks to compile, generate PDF, or invokes /compile-resume.

## Rules

- Do not tailor or rewrite the resume unless explicitly asked.
- Do not create Notes.md.
- Do not create Job_Description.md.
- Do not create jd_snapshot.md.
- Do not create interview prep.
- Only compile the specified .tex file.
- If no path is provided, ask for the path or infer the most recent Tailored_Resume.tex only if obvious.
- Keep final response short.

## Output

Generate PDF in the same folder as the .tex file.

Final response:
- PDF path
- Any compile warning/error that matters
