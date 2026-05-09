# Persona research methodology

How Medovnicek Labs builds personas that survive contact with reality.

## Principles

1. **Real people first.** A persona traceable to one specific human in your CRM beats a clever synthetic composite. Real personas have a phone number you can call again.
2. **Synthesize only when you have to.** When the segment is too large for one human to represent (a "consumer" persona for a B2C product), synthesize from at least 5 distinct data points across at least 3 source types.
3. **Source every claim.** If you can't trace a sentence to evidence (interview, ticket, telemetry, observed behavior), it's not in the persona — or it's marked `[INFERRED]` so the next interview can verify or kill it.
4. **Voice over demographics.** "She's a 34-year-old marketing manager in Brno" tells you nothing useful. "She'll bounce on a 30-second loading state" is operationally actionable.
5. **Vetoes over approvals.** The persona's value is what they would refuse, not what they tolerate. Lead with veto criteria.

## Sources, ranked by signal density

1. **In-depth interviews (60+ min)** — best signal-to-noise. Recorded with consent. 3 interviews ≈ enough for a v0.1 persona.
2. **Sales call transcripts** — strong on objections and unmet needs; weak on day-to-day behavior.
3. **Support tickets / chat logs** — strong on pain points, weak on positive desires (people don't open tickets when things work).
4. **In-product telemetry** — what they actually do (vs what they say they'd do). Crucial calibration when synthesized desires diverge from observed behavior.
5. **NPS verbatim / survey free-text** — high volume, low depth. Useful for confirming patterns, dangerous as a sole source.
6. **Public reviews (App Store, social, forums)** — last resort. Heavily skewed toward extreme experiences.

A persona built only on (5) and (6) is a marketing persona, not a council persona. Don't convene it.

## The minimum viable persona

You can ship a v0.1 persona file with:

- 3 interviews from people in the segment, OR
- 1 interview + ~20 support tickets + ~5 sales calls, OR
- 1 deep ongoing relationship (an actual user you ship to weekly)

Below that threshold, you're convening a fiction. Collect more first.

## Interview protocol

See `INTERVIEW_GUIDE.md` for the full template. Core moves:

1. **Open with their world, not your product.** "Walk me through your last project from start to finish" before "what do you think of feature X?"
2. **Watch them work.** A live screen-share of them attempting a real task is worth 30 minutes of self-report.
3. **Push past the first answer.** If they say "the UI could be better," ask: "Tell me about the last time the UI got in your way. What were you trying to do?"
4. **Capture their exact vocabulary.** Their words go into the persona file's "How they talk" section verbatim.
5. **End with the veto question.** "What would cause you to stop using this entirely?" — this is gold for the persona's veto criteria.

## Synthesis protocol (multi-source)

When you're combining several sources into one persona:

1. **Tag every claim with its source.** Spreadsheet, doc, sticky notes — any structure works as long as you can trace later.
2. **Cluster claims by theme.** Group "wants" together, "distrusts" together, etc.
3. **Drop singletons.** A claim from one source is hypothesis, not fact. Either find a second source or mark `[SINGLE-SOURCE — verify]`.
4. **Identify contradictions.** When two sources say opposite things, that's not noise to be averaged — it's signal that you may have **two personas**, not one.
5. **Write the persona file.** Use `persona-template.md` as the structure. Fill in the `_provenance` block with every source you used.
6. **Pressure-test before convening.** Show the draft to a third party (a non-team-member, ideally) and ask "does this sound like one coherent person?" Iterate until yes.

## Re-research triggers

Update a persona (don't write a new one) when:

- A real user contradicts a council prediction in production.
- The persona's CHANGELOG has been static for >90 days AND your product/market has materially changed.
- An audit (see `validation/INSIGHT_QUALITY.md`) flags drift in the persona's voice.

Write a NEW persona (don't update an existing one) when:

- A new market segment opens up that doesn't fit any current persona.
- The existing persona was synthesized from sources that disagreed, and you now have evidence to split them.
- A real user emerges who doesn't fit any persona — they may be the seed for a new one.

## What this methodology refuses to produce

- **Marketing personas.** "Eva, 34, lifestyle: artisanal coffee, Pinterest, weekend hikes." Useless for council critique. Drop the lifestyle, keep the workflow.
- **Aspirational personas.** Personas that describe who you wish your users were. The council's job is to surface what real users will actually do, not what your team hopes for.
- **Validation personas.** Personas constructed (consciously or not) to APPROVE of your team's plan. The audit step in `validation/INSIGHT_QUALITY.md` exists to catch these.

If you find yourself in any of those failure modes, the fix is more research, not more iteration on the persona file.
