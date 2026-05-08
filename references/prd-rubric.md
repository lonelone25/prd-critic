# PRD Rubric — Intake Checklist

Used in Phase 1 of the skill to decide whether the PRD is ready for a useful red-team. A PRD missing two or more of these elements should be flagged back to the user before personas are dispatched, because the personas will only be able to surface the missing pieces (which the user already knows) instead of substantive concerns.

## The five elements

### 1. Problem
- Is there a clear statement of the user problem or business problem being solved?
- Is there evidence the problem exists (research, data, customer quotes, market signals)?

**Red flag:** "Users have asked for X" without evidence of frequency, severity, or willingness to pay.

### 2. Target user / segment
- Is the user named with enough specificity that you could find one to interview?
- If multiple segments are addressed, is the primary segment identified?

**Red flag:** "Users" with no further qualification. "SMB" without role, industry, or use case.

### 3. Scope (in / out)
- Is what's being built explicit?
- Is what's *not* being built also explicit (non-goals)?

**Red flag:** A scope section that lists features without saying which are MVP vs. follow-up.

### 4. Success metric
- Is there at least one quantitative success metric?
- Does it have a target value and a measurement window?
- Is the baseline known?

**Red flag:** "Increase engagement" or "improve conversion" without a number or window.

### 5. Non-goals / explicit cuts
- Does the PRD say what it deliberately *isn't* doing, and why?
- Are constraints (legal, technical, brand, timing) named?

**Red flag:** A PRD with no constraints listed — every real PRD has them.

## Optional elements (nice to have, not required)

- **Open questions** — explicit list of what the PM doesn't yet know
- **Risks** — named technical, market, or organisational risks
- **Dependencies** — teams, systems, or partners required
- **Timeline** — even rough phasing
- **Alternatives considered** — what was rejected and why

A PRD with these is a strong PRD. A PRD without them is fine for v1; the personas will surface what's missing.

## Decision rule

| Required elements present | Action |
|---|---|
| 5 / 5 | Proceed to persona dispatch immediately |
| 4 / 5 | Proceed; note the missing element in the review header |
| 3 / 5 | Proceed but warn the user that the review will be light on the missing dimensions |
| 2 / 5 or fewer | Stop. Ask the user to add the missing elements (or paste the answers in chat) before review |
