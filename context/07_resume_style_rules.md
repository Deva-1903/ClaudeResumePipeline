# Resume Style Rules

Final-output rules for any tailored resume.

## Layout

- One page. Always.
- Use the chosen base resume from `base_resumes/`. Do not rebuild from scratch.
- Preserve the LaTeX style of the base resume: fonts, colors, section formatting, spacing macros, custom commands.
- Make targeted edits: reorder skills, swap or tighten bullets, reorder projects.
- Keep section order as it appears in the base resume unless the JD strongly justifies reordering (e.g., research role wants Education and Publication earlier).

## Truth and content

- Use only verified claims from `01_verified_claims.md`. Cross-check `02_do_not_claim.md` before adding any number, scale, or scope claim.
- Do not invent metrics, users, deployment scale, publications, employment history, or tooling.
- Do not promote coursework to research output or POCs to production deployments.
- Prefer adjacent truthful phrasing over stretching a claim to match a JD keyword.
- If a claim is in the "Needs verification" section, treat it as off-limits.

## Bullet quality

- Use strong, concrete engineering verbs (Built, Engineered, Designed, Optimized, Hardened, Implemented, Profiled, Benchmarked).
- Lead with the action and outcome; tools come after the action.
- Each bullet should pass a recruiter scan in under 3 seconds.
- One verified metric per bullet is enough; do not stack metrics for density.
- Do not keyword-stuff. ATS-friendly does not mean comma-separated keyword salad.
- Cut filler ("passionate", "hardworking", "team player", "dedicated", "results-driven").
- Avoid jargon a hiring manager would not recognize at a glance unless the JD signals deep expertise.

## Tailoring decisions

- Reorder skills to match JD priority — but only list skills already supported in `03_skills.md`.
- Reorder projects so the most JD-relevant project comes first within Projects.
- Replace weaker bullets with stronger relevant ones from `05_bullet_bank.md`.
- Adjust headline / summary line if the base resume has one.

## Space management

- If space is tight, cut weaker project bullets first; never compress an experience bullet into something untrue.
- Education coursework can be trimmed to JD-relevant courses.
- Skills row can drop categories that the JD does not touch.
- Do not shrink the page font or margins to gain space.

## Defaults that stay off

- Do not produce a PDF unless `/compile-resume` is invoked.
- Do not generate Notes.md, Job_Description.md, jd_snapshot.md, cover letter, interview prep, JD mapping, or index updates by default.
- Do not include URLs that are not already in the verified facts.
- Do not include a photo, address line, or visa-status line unless the user adds them.

## Formatting hygiene

- Keep contact info exactly as in the base resume; do not invent a different phone or email.
- Use the same date format as the base resume.
- Spell company names exactly as on the base resume (e.g., "Bengaluru, India" — not "Banglore").
- Escape LaTeX special characters in any new text (`%`, `$`, `&`, `_`, `#`).
