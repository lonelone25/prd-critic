# PRD Critic

An [Agent Skill](https://agentskills.io) that pressure-tests a PRD by dispatching six stakeholder personas — Staff Engineer, Staff Designer, CFO, Sales/GTM, Customer Success, Skeptical Exec — to challenge it from their lens. Produces a structured red-team review with ranked risks, unanswered questions, and suggested edits.

It reads the PRD the way each role would: the engineer hunts for scope creep and missing NFRs, the designer for user-flow gaps, the CFO for fuzzy economics, the GTM lead for buyer objections, CS for support burden, the exec for strategic fit. Every concern it raises is grounded in the PRD's own text — no generic PM aphorisms.

Compatible with any agent that implements the [agentskills.io](https://agentskills.io) specification: Claude Code, Cursor, Amp, OpenCode, and Codex CLI.

---

## Why this exists

Most PRDs die slowly in three meetings:

1. The eng review where the PM finds out the architecture isn't ready
2. The exec review where the strategic fit gets challenged
3. The sales review where positioning falls apart against a competitor

By the time you've sat through all three, you've burnt three weeks. **prd-critic** simulates those meetings in three minutes, against the same PRD, with a structured deliverable you can hand to the team.

It does not replace the actual stakeholder reviews. It catches the obvious gaps before you waste anyone's time.

---

## What it produces

A markdown file `prd-review-{prd-name}-{date}.md` with:

- **Summary** — 3–5 sentences a busy manager can read
- **What works well** — 2–4 specific bullets, no filler
- **The core tension** — the one structural issue (if any) that, if fixed, resolves a third of the concerns
- **Blockers** — concerns severe enough to delay shipping, with quoted PRD sections and one-sentence suggested edits
- **Serious concerns** — won't block ship but will hurt later
- **Unanswered questions, by persona** — the sharp questions each role would ask
- **Suggested next revision** — a prioritised action list
- **Nits** — small fixes for the next pass

See [`examples/sample-review.md`](examples/sample-review.md) for a full demo, run against the PetPantry sample PRD in [`examples/sample-prd.md`](examples/sample-prd.md).

---

## Installation

Clone the repo into the skills directory for your agent.

**Claude Code**

```bash
git clone https://github.com/lonelone25/prd-critic ~/.claude/skills/prd-critic
```

**Cursor**

```bash
# User-wide
git clone https://github.com/lonelone25/prd-critic ~/.cursor/skills/prd-critic

# Project (commit to share with your team)
git clone https://github.com/lonelone25/prd-critic .cursor/skills/prd-critic
```

**Amp**

```bash
# User-wide
git clone https://github.com/lonelone25/prd-critic ~/.config/agents/skills/prd-critic

# Project
git clone https://github.com/lonelone25/prd-critic .agents/skills/prd-critic
```

**OpenCode**

```bash
# User-wide
git clone https://github.com/lonelone25/prd-critic ~/.config/opencode/skills/prd-critic

# Project
git clone https://github.com/lonelone25/prd-critic .opencode/skills/prd-critic
```

**Codex CLI**

```bash
git clone https://github.com/lonelone25/prd-critic ~/.codex/skills/prd-critic
```

Then reload your agent.

---

## How to trigger it

The agent loads this skill automatically when your request matches. These phrases reliably trigger it:

```
red-team this PRD
pressure-test this PRD
challenge this PRD
stakeholder review of this PRD
what would [eng / design / sales / CFO] say about this?
stress-test this product brief
tear apart this one-pager
```

Point the agent at a markdown file containing your PRD. If the doc is missing critical pieces (no problem statement, no metrics, no audience), the skill will ask 1–3 sharpening questions before running personas — a red-team on a half-written PRD just produces noise.

---

## Try it without writing your own PRD

```
red-team the PRD at examples/sample-prd.md
```

The agent will produce a review against the fictional PetPantry vet-diet subscription. Compare it to [`examples/sample-review.md`](examples/sample-review.md) to see the structure and depth.

---

## What's in the box

```
prd-critic/
├── SKILL.md                    # main skill — 4-phase workflow
├── README.md                   # this file
├── references/
│   ├── prd-rubric.md           # intake checklist
│   ├── output-template.md      # review file structure
│   └── personas/
│       ├── staff-engineer.md
│       ├── staff-designer.md
│       ├── cfo.md
│       ├── sales-gtm.md
│       ├── customer-success.md
│       └── skeptical-exec.md
└── examples/
    ├── sample-prd.md           # PetPantry, fictional
    └── sample-review.md        # the agent's output for it
```

---

## Design choices, briefly

- **Six personas, fixed.** v1 keeps the persona list closed. Letting users define personas per run was tempting but dilutes the skill's opinion. If you need a Legal or Data Science lens, open an issue.
- **Markdown in, markdown out.** No connectors, no Notion / Confluence integration in v1. Paste your PRD into a file, run the skill, paste the review back into your tool of choice.
- **The file is the deliverable.** Chat gets a 3–5 sentence summary. The review file is what you share with the team.
- **No scoring.** Severity tags ([BLOCKER], [SERIOUS], [NIT]) are the only ranking. Numerical scores invite gaming.

---

## Roadmap

- [ ] **v2 (Claude Code edition)** — native subagents for parallel persona dispatch, MCP integration to pull PRDs from Notion, optional Jira ticket generation from the "Suggested next revision" section
- [ ] Configurable persona set (add Legal, Compliance, Data Science, Marketing)
- [ ] Multi-doc review (red-team a PRD against an existing roadmap or strategy doc)
- [ ] CLI wrapper for use outside an agent context

---

## Author

Built by [Cho Chan Myei Oo](https://linkedin.com/in/chochanmyei) — AI Product Manager. I make tools for PMs that I wished existed when I was the only person reviewing my own PRDs.

If you use it and have feedback — what worked, what was wrong, what persona you'd add — open an issue or message me on LinkedIn.

---

## Licence

MIT. Use it, fork it, ship it.
