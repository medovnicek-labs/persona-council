---
name: persona-research
description: Convert raw user-research notes (interview transcripts, support tickets, sales calls, in-product feedback) into a persona file the persona-council skill can convene. Walks through synthesis interactively. Use when standing up a new product's council, when an existing persona feels stale after real user contact, or when expanding into a new market segment.
---

# Persona Research — Synthesis Skill

Turns raw qualitative research into a structured persona file. Output drops directly into `<cwd>/docs/personas/council/<slug>.md` for the `/persona-council` skill to pick up.

## When to use

- **New product's first persona.** You have ~3+ user conversations and need a structured persona to start critiquing PRDs against.
- **Refreshing a stale persona.** Real users surprised the council — synthesize from the new evidence and update the file.
- **Expanding to a new segment.** New market (e.g., commercial vs residential customers) needs its own persona.
- **Combining noisy signal.** You have 50 support tickets and 4 NPS comments — synthesize a persona from the aggregated voice.

## Inputs accepted

The skill works with any of:

1. **Raw transcript** (paste, or a file path). Best when you have one rich conversation.
2. **Multiple sources** (transcripts + notes + tickets) — listed by source. Best for synthesizing across signal.
3. **A draft persona file** — to refine an existing draft against the canonical template.
4. **Quotes-only mode** — when you only have direct quotes (e.g., from sales calls), the skill leans heavily on voice and is conservative about inferred behavior.

## Process

1. **Inventory sources.** Ask the user for what they have. Note the date and source of each input — this becomes the persona's `_provenance` block (so future audits can trace claims back to evidence).

2. **Identify the unit of analysis.** Is this *one person* (a real user we keep talking to) or *a synthesized representative* (a composite from many)? The persona file's opening line says which — never blur the two.

3. **Extract structured fields** by asking the user (or inferring from the source) about:
   - Role / job context
   - How they talk (vocabulary, language, tone — quote actual phrases)
   - Top 3–5 things they want from the product
   - What they distrust or are confused by
   - What delights them (use sparingly — don't invent delight you didn't observe)
   - What they would VETO (their non-negotiables)

4. **Draft the council role** — the question battery this persona asks when convened. These should be answerable from the input alone (no leading questions).

5. **Write the persona file** in the canonical template format (see `research/persona-template.md`). Include a `_provenance` block with sources.

6. **Place the file:**
   - Default: `<cwd>/docs/personas/council/<slug>.md`
   - Ask before overwriting an existing file — and if overwriting, save the previous version to `<slug>.md.YYYYMMDD.bak` so the audit trail is preserved.

7. **Suggest next steps:**
   - Convene `/persona-council` against the next PRD to pressure-test the new persona's voice.
   - Schedule a calibration check (see `validation/CALIBRATION.md`) for ~30 days out.

## Anti-patterns

- **Don't fabricate.** If a field has no evidence, leave it blank or annotate it `[INFERRED — verify with next interview]`. Better a sparse persona than a confident lie.
- **Don't merge contradictory voices.** If two interviewees said opposite things, that's signal for two personas, not one wishy-washy composite.
- **Don't promote a single quote into a "what they always say."** A persona's voice should be patterns across multiple data points, not a memorable line from one call.
- **Don't write personas to fit a marketing narrative.** The council's value is critique. A persona engineered to validate the team's plan is useless.

## Output anatomy

The skill writes the persona file with:

```markdown
# <Name> — <one-line role>

**Real / Synthetic:** Real | Synthetic (from N sources, see _provenance)

[Body sections per template: How they talk, What they want, What they distrust, What delights them, Council role]

## _provenance

- 2026-04-18: Interview transcript, 45 min, recorded with consent.
- 2026-04-22: 12 support tickets across Q1.
- 2026-05-02: NPS verbatim, 4 comments scored ≤ 6.

Updated: 2026-05-09 by <author> — see CHANGELOG below for delta.

## CHANGELOG

- 2026-05-09: Added VETO on shared-link feature after sales-call signal (3 of 5 prospects).
- 2026-04-22: Initial draft from 1 interview + 12 tickets.
```

The `_provenance` and `CHANGELOG` blocks are non-optional. They are how `validation/CALIBRATION.md` traces drift over time.
