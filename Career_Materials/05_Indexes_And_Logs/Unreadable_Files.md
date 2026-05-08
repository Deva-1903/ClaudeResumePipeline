# Unreadable Files

Files that could not be parsed as text (so their content does NOT contribute to `Career_Brain_Dump.md`).

## As of 2026-05-07

**None.** Every PDF in the `/Resume/` tree was successfully parsed via `pdftotext -layout`. All 29 PDFs produced extracted text in `04_Extracted_Text/`.

## Notes

- The `.tex` and `.log` source files in `Latest_6/` and `By_Role/Research_CIIR/` and `By_Role/ML/` are LaTeX source / build logs, not unreadable. They were not extracted because their corresponding PDFs already produced clean text.
- The `Coding Best Practices Powered By Amazon's Day 1 Tech Prep (DTP) .ics` file is a calendar event, not a resume — intentionally excluded.
- If new files become unreadable in the future (encrypted PDFs, image-only scans), append them here with the reason and any OCR attempt notes.
