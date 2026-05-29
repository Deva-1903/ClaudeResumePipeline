# LEAN_APPLY_PROMPT.md

> Paste the block below into a fresh Claude Code session in this repo, with the JD appended.
> This runs **inside Claude Code chat**, not in the terminal shell.

---

```
/lean-apply

JD:

[paste job description here]
```

---

That is all you need to start a run.

What `/lean-apply` actually does — the output files, the truth hierarchy, the JD framing pass, the mandatory truth-audit and independent-scoring passes, and the optional escalations (`/revise-resume`, `/skill-gaps`, `/compile-resume`, `/interview-prep`, `/refresh-base-resumes`, `/refresh-factbase`) — is defined canonically in:

- `.claude/skills/lean-apply/SKILL.md` — the operational spec the skill follows.
- `CLAUDE.md` — repo-wide policy (truth hierarchy, default flow, hard rules).
- `README.md` — orientation and repo layout.

This file is intentionally just the paste block, so the spec has a single source of truth and these docs cannot drift apart.
