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

### Weak-signal content — keep it off bullets (MANDATORY)

A claim being *true* is necessary but not sufficient. A bullet must also carry a signal a screener respects. Even when the fact is verified, do NOT surface these categories on resume bullets — they are interview color at most:

- **Process over accomplishment.** How the work was built is not the signal; what was built and its outcome is. Keep AI-assisted-development framing off bullets — no "AI-assisted", "vibe-coding", "Claude Code / Copilot / multi-agent workflow", "self-taught the stack", "prompt-engineered my way to". (Deva's real, measured AI/LLM *engineering* — align-ops post-training, agent pipelines, RAG — is accomplishment, not process, and is fine.)
- **Plans, designs, and intentions framed as done.** If it is design-doc'd, "decided", "planned", or "not yet integrated/shipped", it does not go on a bullet as an achievement. Only shipped, working, or measured work earns a bullet. (See the pre-launch / not-yet-shipped truth notes in `01_verified_claims.md`.)
- **Hobby-scale or small numbers that read *small*.** A number belongs on a bullet only when it reads as impressive to a screener. Tiny budgets, low costs, or small counts (e.g. a `$0–60/yr` hosting bill) read as unserious even when true — omit them. Prefer a strong verified metric (users, throughput, %, revenue, scale) or no number over a small one.

When one of these is the only "extra" available, cut it and lead with engineering substance instead; do not pad a bullet with weak-signal material to fill space (see Space management — fill with truthful *strong-signal* bullets only).

## Tailoring decisions

- Reorder skills to match JD priority — but only list skills already supported in `03_skills.md`.
- Reorder projects so the most JD-relevant project comes first within Projects.
- Replace weaker bullets with stronger relevant ones from `05_bullet_bank.md`.
- Adjust headline / summary line if the base resume has one.

## Mandatory JD framing pass

Every tailored resume must go through a JD framing pass after evidence is selected. The framing pass:

- Mirrors the JD's priority themes (ownership, quality, ambiguity, simple solutions, debugging mindset, AI-assisted development, security/reliability, product thinking) in bullet phrasing — using only truthful evidence already in the truth source.
- Replaces generic phrasing with JD-aligned phrasing wherever a more specific truthful version is available (see examples in `06_role_targeting.md`).
- Echoes the JD's vocabulary naturally — not as keyword stuffing.
- Cuts bullets that are strong in general but weak for this specific JD.
- Reorders sections and projects to put the team's likely focus area first.

Tailoring goal: **tailored AND identity-stable.** The reader should feel the resume was written for this role and team — but a side-by-side reader of two tailored versions of this resume should still recognize the same candidate, with the same claims, the same scope descriptors, and the same metric attributions. Framing changes emphasis, ordering, and vocabulary; it does NOT change the set of claims, their scope, or what each metric is attributed to. See `02_do_not_claim.md` "Tailoring stability" for the hard rules.

## Space management

- If space is tight, cut weaker project bullets first; never compress an experience bullet into something untrue.
- Education coursework can be trimmed to JD-relevant courses.
- Skills row can drop categories that the JD does not touch.
- Do not shrink the page font or margins to gain space.
- If there is significant bottom whitespace, fill it so the page looks full: add the smallest set of truthful, JD-relevant bullets from `05_bullet_bank.md` (split a combined bullet, restore a second bullet to a thin entry, or add a third bullet to the strongest project). Never pad with filler or invented claims. A correct but half-empty page is not finished.

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
- **No em-dashes (`---`) in body text.** LaTeX renders `---` as an em-dash. Use a comma instead. LaTeX section-marker comments (`%----------SKILLS----------`) are exempt — they don't render. **This rule applies to cover letters and every opt-in extra artifact too, not just resumes** — including recipient/address and "Re:" lines (write `Cosm, Software Engineering Internship`, never `Cosm --- Software Engineering Internship`).

## Mandatory skills coverage

- **Cloud row is always on.** Every tailored resume must include `AWS, GCP, Azure` in the Skills row under a Cloud / DevOps category, regardless of whether the JD mentions cloud. Reorder the cloud entries to put the JD-preferred provider first, but do not drop the row or any of the three providers.
- **Cloud row label must be `Cloud & DevOps`** (or an equivalent 2-part label like `Backend & Cloud`). Do NOT use 3-part compound labels like `Cloud, DevOps & Databases` or `Cloud, Data & Systems` — split databases and other categories into their own row.
- The "do not claim cloud production ownership" rule from `02_do_not_claim.md` still holds — listing these in the Skills row is resume-safe; bullets must not claim production cloud work.

### Skills-row label hygiene (MANDATORY — recruiters skim this section)

The Skills label column is a fixed ~1.36in. A label that exceeds it wraps to two lines and LaTeX hyphenates it ("Autod-iff", "Optimiza-tion"), which reads as overpacked and ugly. To prevent this:

- **Every category label must fit on ONE line** in the label column. Keep labels to **1–2 short words (target ≤ ~16 characters)**: `ML & Autodiff`, `Numerics`, `Performance`, `Backend & APIs`, `Cloud & DevOps`, `Data & Warehousing`. Avoid long 3+ word labels like `ML Frameworks & Autodiff` or `Numerical & Optimization` — abbreviate (`ML & Autodiff`, `Numerics`).
- **Base resumes carry a no-hyphenation safeguard**: the label column spec is `>{\bfseries\raggedright\arraybackslash}p{1.36in}` (ragged, never hyphenated). Preserve this when copying a base; never revert it to `>{\bfseries}p{1.36in}`. This stops mid-word hyphens but does NOT excuse long labels — a too-long label still wraps to two ragged lines, so the 1–2-word rule above still applies.
- **Post-compile visual check (runs with the one-page / page-fill check):** scan the rendered Skills section. If any category label wraps to a second line OR is hyphenated, shorten that label and recompile before scoring. Also keep value cells from looking like a keyword wall — if a row runs long, drop the lowest-signal items rather than letting the section bloat.
