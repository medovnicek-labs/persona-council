# <Persona name> — <one-line role>

> The first line below MUST declare whether this is a real person or a synthetic composite. If you can't decide, the persona is too thin to convene yet — collect more research first.

**Real / Synthetic:** Real (one person, ongoing contact) | Synthetic (composite from N sources, see `_provenance`)

## Quick orientation
- **Role:** Their job context. Specific enough to be falsifiable ("owner-operator of a 2-person carpentry workshop" — not "a craftsman").
- **Domain:** What domain knowledge they bring. ("EU furniture standards, Blum/Hettich hardware, CNC routing.")
- **Volume of contact:** How much real signal we have. ("3 calls + 12 support tickets + 1 in-person visit" — not "we know him well.")

## How they talk
- Vocabulary they actually use (quote real phrases when you have them).
- Language(s) and which one for which context.
- Tone — direct? hedged? sarcastic? Affect drives how Claude voices them.
- Things they would NEVER say (negative voice — keeps Claude from drifting).

## What they want from the product
List 3–5 desires, ranked. Each desire should be:
- Phrased as the outcome they care about, not the feature you'd build.
- Specific enough to test (e.g., "a cut list that goes straight to my CNC the same day" — not "it should be useful").
- Sourced — if you have a quote, footnote it.

## What they distrust
What sets off their bullshit detector. Each item should describe:
- The behavior or output that would violate trust.
- Why — usually a past incident or a strong professional norm.

## What confuses them
Vocabulary, UI patterns, workflows that they will not parse. Not "things they don't understand" — *things they would silently fail to use*.

## What delights them
Use sparingly. Better to leave this thin than to fabricate. Record only delights you have **observed** (a quote, a behavior, a verbatim comment) — not the delights you wish they'd express.

## Council role

The question battery this persona asks when convened. Each question should be:
- Specific enough to answer from the artifact alone, no leading.
- Anchored in *their* world ("Will this go straight to my CNC?" not "Is this technically rigorous?").
- Falsifiable — they can issue an APPROVE / CONDITIONAL / VETO based on the answer.

5–8 questions is the right range. Too few and the council is shallow; too many and the synthesis becomes noise.

## Veto criteria

Explicit list of things that would cause this persona to VETO an artifact. These should mirror their real-world non-negotiables. Examples:

- "Hardware that doesn't exist as a buyable SKU."
- "Cut list missing edge-banding designation on visible faces."
- "Any English-language UI on a Czech-market product."

When a session yields a VETO that doesn't match this list, that's a signal: either the criterion was wrong, or the persona has drifted. Audit mode catches both.

## Cross-references

Link to:
- Source documents (interview notes, transcripts, support tickets) — keep paths private if needed.
- Adjacent project docs that informed the persona (specs they shaped, prompts written for them).

## _provenance

Date-stamped sources for every claim above. Examples:

- `2026-04-18` — 45-min interview (recording archived in [private link]).
- `2026-04-22` — Q1 support tickets #89, #91, #103 (filtered for this customer segment).
- `2026-05-02` — NPS verbatim, 4 comments scored ≤ 6.

If you can't source a section, mark it `[INFERRED — verify next interview]`.

## CHANGELOG

Reverse-chronological. Every meaningful edit gets a line.

- `2026-05-09 by pavol`: Added VETO on shared-link after sales-call signal (3 of 5 prospects independently raised it).
- `2026-04-22 by pavol`: Initial draft from interview + tickets.

The CHANGELOG is what `validation/CALIBRATION.md` reads to detect "this persona keeps shifting" patterns.
