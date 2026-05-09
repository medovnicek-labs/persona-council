# Synthesis template

Use this when turning multiple raw sources into a single persona file. Copy this template into a working doc, fill in, then write the final persona using `persona-template.md`.

## 0 — Source inventory

| Source ID | Date | Type | Notes |
|-----------|------|------|-------|
| S1 | 2026-04-18 | 60-min interview | Real user, oak wardrobe project |
| S2 | 2026-04-22 | Q1 support tickets | 12 tickets, filtered by segment |
| S3 | 2026-05-02 | NPS verbatim | 4 comments scored ≤ 6 |

If your inventory has fewer than 3 rows OR fewer than 2 source types, the persona is too thin to convene. Collect more before continuing.

## 1 — Raw extraction

For each source, pull the following into a working doc (spreadsheet works well):

| Source | Quote / observation | Theme | Tag |
|--------|---------------------|-------|-----|
| S1 | "podla toho by som to nespravil" | distrust of AI hallucination | VOICE |
| S1 | needs cut list ready for CNC same day | wants | OUTCOME |
| S2 #91 | "missing right-side panel decor designation" | distrust of incomplete spec | TICKET-PAIN |

Tags to use (free to add more):
- `VOICE` — their actual phrasing, vocabulary
- `OUTCOME` — what they want to be true
- `WORKFLOW` — how they work today
- `TICKET-PAIN` — concrete failure mode they reported
- `SURPRISE` — they reacted in a way you didn't expect
- `VETO` — explicit dealbreaker
- `CONTRADICTION` — conflicts with another source

## 2 — Cluster

Group your tagged extractions by theme. Look for:

- **Multi-source agreement.** If 3+ sources independently say variants of the same thing, it's a high-confidence persona claim.
- **Single-source claims.** Mark `[SINGLE-SOURCE]` in the persona file. Verify in your next interview before promoting.
- **Contradictions across sources.** Two voices? Two personas. Don't average; split.

## 3 — Voice composite

Pull 5–10 verbatim phrases that represent how this persona talks. These go directly into the persona file's "How they talk" section, not paraphrased.

If you have <5 verbatim phrases, the voice is too thin — collect more. Do not invent.

## 4 — Outcome ranking

List every "wants" claim from the cluster. Rank by:
1. **Recency** — recent signals weigh more.
2. **Frequency** — how many sources surfaced it.
3. **Specificity** — concrete asks beat aspirational ones.

Top 3–5 go in the persona file's "What they want" section.

## 5 — Veto extraction

For every `VETO` tag, write a one-line operational criterion. Example:

- Source: "I wouldn't build it from this" (S1, on a generated spec missing right-side panel info)
- Veto criterion: "Spec missing edge-banding or visible-face designation."

Wherever possible, tie the veto to something falsifiable in your output (a missing field, a violated rule, a wrong dimension). Vague vetoes ("not professional enough") get pushed back into a follow-up interview for specificity.

## 6 — Council role

Translate the persona's perspective into 5–8 questions they'd ask when convened. Each question should:
- Be answerable from the artifact alone (the council session won't have the persona's full backstory).
- Use *their* vocabulary, not yours.
- Allow APPROVE / CONDITIONAL / VETO answers.

Bad: "Is this good?"
Good: "Will this output go straight to my CNC, or do I have to rework it?"

## 7 — Provenance block

For the persona file's `_provenance` section, list every source from your inventory with date and type. Don't list specific support ticket IDs in the public file if your tickets aren't open — keep an internal mapping if needed.

## 8 — Pressure-test

Before promoting the draft to `docs/personas/council/`:

1. Show it to one person who didn't do the synthesis (ideally a non-team-member familiar with the segment).
2. Ask: "Does this sound like one specific person?"
3. If they hedge, the persona is too smooth. Add the contradictions back in or split.

## 9 — Promote

Once the draft passes pressure-test:

- Save to `<project>/docs/personas/council/<slug>.md` (or wherever your project's discovery path is).
- Run `/persona-council` against a recent PRD or spec to dogfood the new voice.
- Schedule a calibration check 30 days out (`validation/CALIBRATION.md`).
