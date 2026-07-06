---
description: Write a concise, human cold email + LinkedIn DM for a referral or recruiter outreach. Use when the user wants to message a person (engineer, recruiter, alum) about a role — "cold email", "DM this person", "ask for a referral", "outreach to X".
argument-hint: "[role + company + JD] / [person name + title + connection]"
---

# Cold Outreach Skill

## Goal

Produce three things, in this order:

1. **A polished email** (under 180–220 words).
2. **A shorter LinkedIn DM** (under 120–150 words).
3. **A subject line** for the email (place it directly above the email).

The output is a chat message, not a file. Do NOT create an application folder, `.tex`, or any artifact unless the user explicitly asks.

## Voice

Human, direct, specific. Sounds like one engineer messaging another.

Banned — never use these or anything in their spirit:
- Generic enthusiasm: "I am passionate about technology", "I admire your mission".
- Hype / intensity: "not just demos", "resume into the void", "aren't slogans to me", "for real", emoji-driven openers.
- Corporate fluff and filler. No exaggeration of any claim.

Rules:
- Short enough for a busy person to skim.
- Clear and professional, but not stiff or over-formal.
- Ground every claim in real work. Do not inflate scope, metrics, or seniority.
- The **first paragraph must be specific to the company/team/person** — name the team's actual area and tie it to a real reason for reaching out. If a UMass / school / mutual connection exists, lead with it naturally.

## Structure (email)

1. **Opening (1–2 sentences):** who I am + why I'm reaching out, specific to this company/person.
2. **One specific hook:** one reason the role/team caught my attention, connected to a concrete piece of my experience. Pick the single most relevant project — do not list several here.
3. **3–5 background bullets:** my most relevant work, tightest phrasing, one line each. Do not over-explain any project.
4. **One bridge sentence:** connect the background to this specific role.
5. **Simple ask:** referral, quick chat, or next step — low-pressure, give an easy out.
6. **Clean signature.**

The DM compresses 1–3 into a sentence or two, keeps 1–2 of the strongest bullets inline, and keeps the same ask. Even shorter.

## Selecting background

Pull only from the truth hierarchy in `CLAUDE.md` (`context/01_verified_claims.md`, `04_project_bank.md`, `05_bullet_bank.md`, `03_skills.md`, `00_resume_factbase.md`; `raw/brain_dump_original.md` as fallback). Same off-limits rules as `/lean-apply` (`context/02_do_not_claim.md`). If the role's application folder already exists under `applications/`, its `meta.json` `strong_matches` is a good shortlist of what to emphasize — but do not invent anything beyond the truth source.

Choose the 3–5 bullets and the one hook that are **most relevant to this specific JD/team**, not the most impressive in general. Reorder for the role: backend role → lead with Wysa / production services; agent/AI infra role → lead with cf-scout / AgenticSearch; data role → lead with the Spark pipeline.

Reusable background facts (still verify against the truth source before using):
- MS CS student at UMass Amherst.
- 2 yrs backend engineer at Wysa — production services, secure APIs, multi-tenant systems, auth/rate limiting, audit logging, production debugging, internal tools.
- Full-stack annotation platform for AI/data teams — cut 100+ hrs/month of manual work.
- AgenticSearch — retrieval, deterministic extraction, LLM fallback, verification, cell-level provenance.
- cf-scout — edge-native AI research agent; persistent server-side state, WebSocket streaming, recovery from tool/process failures.
- Underdogs Fitness — production full-stack platform, solo-maintained, live 3+ years.
- Spark pipeline over ~1.4B rows, tuned for runtime and data quality.
- Stack: Node.js, Python, React/Next.js, MongoDB, Redis, Docker, GitHub Actions, CI/CD, cloud deploy.

## If inputs are missing

If the user has not pasted the role/company/JD or the target person, ask for them before writing — the first paragraph cannot be specific without them. Do not fabricate the person's name, title, or connection.

## After writing

Offer to adjust tone (more/less casual), trim further, add the job-posting link, or swap which project leads.
