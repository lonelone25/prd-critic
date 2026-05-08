# Output Template — PRD Review Structure

The deliverable file produced by the skill. Filename pattern: `prd-review-{prd-filename-stem}-{YYYY-MM-DD}.md`

Use this exact structure. Do not invent new sections or skip required ones.

---

```markdown
# PRD Review: {PRD Title}

**Source:** `{path/to/source-prd.md}`
**Reviewed:** {YYYY-MM-DD}
**Reviewers:** Staff Engineer · Staff Designer · CFO · Sales/GTM · Customer Success · Skeptical Exec

---

## Summary

{3–5 sentences. What the PRD does well. The core tension if one exists. Top 2 blockers. No filler.}

---

## What Works Well

{2–4 specific bullets. Each cites a section and says why it's effective. Omit this section entirely if there's nothing substantive to praise — empty praise weakens the rest of the review.}

- **{Specific element from PRD}** — {Why it works, in one sentence}

---

## The Core Tension

{One paragraph, two to three sentences max. Identify the single structural issue (if any) that, if fixed, would resolve a third or more of the concerns below. Often this is a missing problem statement, an unstated assumption about user behaviour, or a confused target segment. If there's no single core tension — just a scattered set of issues — say so and skip this section.}

---

## Blockers

{Concerns tagged [BLOCKER] by any persona. Merge duplicates. Each blocker:
- One-line summary (the concern)
- Which persona(s) raised it
- The PRD section it cites
- The proposed answer or rewrite}

### 1. {Blocker title}
**Raised by:** {Persona name(s)}
**Cites:** Section {N}, "{short quote under 15 words}"
**Concern:** {One paragraph, plain English.}
**Suggested edit:** {One sentence the PM could apply directly.}

### 2. {Blocker title}
...

---

## Serious Concerns

{Same structure as Blockers, for [SERIOUS]-tagged items. Group thematically if useful (e.g., "Around pricing", "Around onboarding").}

### 1. {Concern title}
**Raised by:** {Persona name(s)}
**Cites:** Section {N}
**Concern:** {Plain English.}
**Suggested edit:** {One sentence.}

---

## Unanswered Questions, by Persona

{For each persona, the 1–3 sharpest unanswered questions they raised. This is not a duplicate of Blockers — these are the open questions the PM needs to answer in the next revision, regardless of severity.}

**Staff Engineer**
- {Question}
- {Question}

**Staff Designer**
- {Question}

**CFO**
- {Question}
- {Question}

**Sales / GTM**
- {Question}

**Customer Success**
- {Question}

**Skeptical Exec**
- {Question}

---

## Suggested Next Revision

{A short bulleted action list of what the PM should change before circulating v2. Order by impact, not by section. 5–8 items max.}

1. {Action}
2. {Action}
...

---

## Nits

{[NIT]-tagged items, deduplicated, in a single flat list. One line each. No persona attribution needed.}

- {Nit}
- {Nit}
```

---

## Style rules for filling in the template

- **No section bloat.** If a persona had nothing to say in their lane, it's fine. Don't pad.
- **Quote sparingly.** One short quote per concern, max 15 words, in quotation marks.
- **Specific over generic.** Every concern must reference a section number or paragraph. If you can't, the concern isn't yet sharp enough — re-do it.
- **No PM jargon.** Avoid "synergy," "leverage," "stakeholder alignment," "north star," unless the PRD itself uses them and you're quoting back.
- **Plain text severity tags.** [BLOCKER], [SERIOUS], [NIT] — do not use emoji severity markers, traffic-light colours, or invented tiers.
- **Suggested edits are one sentence.** If a fix needs three sentences, it's actually three suggestions.
