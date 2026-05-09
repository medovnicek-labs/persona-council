# Calibration

The council's predictions become wrong over time as the product, market, and personas evolve. Calibration is how we keep them honest.

## The basic loop

1. Council predicts: "Eva would VETO this onboarding because she'd bounce after 30 seconds."
2. Ship the onboarding.
3. Real Eva-segment users contact the product.
4. Compare reality to prediction.
5. Update the persona file with the contradicting signal.

Without step 5, personas calcify into folklore. With it, they become living documents.

## When to calibrate

### After every meaningful product ship

For each persona that issued a verdict on the shipped feature:

- Did real users in that persona's segment behave as the persona predicted?
- If yes: tag the persona file CHANGELOG with "2026-MM-DD: Verified prediction on ${feature} — ${observation}." This tells future sessions the persona is still grounded.
- If no: the persona predicted X, reality showed Y. Update the persona file with the contradicting signal. Don't delete the prior content — annotate it (`[contradicted by 2026-05-01 ship — see CHANGELOG]`).

### On a recurring cadence (monthly is healthy)

Even without major ships, run a calibration check:

1. Pull the most recent ~10 council sessions.
2. For each session, ask: did this prediction get tested in production? With what result?
3. Personas that consistently predict reality: leave alone (annotate the CHANGELOG).
4. Personas that consistently miss: update from current evidence.
5. Personas that haven't been tested at all: schedule a real-user touchpoint to test them (interview, support-ticket pull, NPS sweep).

### On request from any council session that flagged drift

The audit mode (`validation/INSIGHT_QUALITY.md` check #5) flags drift inside a single session. Calibration is the longer-horizon companion: drift across many sessions.

## What to calibrate against

In rough order of signal strength:

1. **Direct user contact post-ship.** A user from the segment uses the feature, reports back. Highest signal.
2. **In-product telemetry.** They didn't say anything, but they bounced at the predicted moment (or didn't). Medium-high signal.
3. **Support tickets in the time window.** People only open tickets when things break, so this is biased toward problems — fine for verifying VETO predictions, weak for verifying APPROVE.
4. **Sales-call pattern.** If 3 of 5 prospects raise the same concern the council didn't flag, that's a calibration miss.
5. **No user contact at all.** Can't calibrate without evidence. Schedule a touchpoint.

## How to record a calibration update

Update the persona's CHANGELOG:

```markdown
## CHANGELOG

- 2026-05-15 (calibration): Predicted Eva would VETO the JSON spec being visible.
  Real users (3 ticket signals + 1 interview) confirmed; VETO held. No file change.
- 2026-05-22 (calibration): Predicted Eva would APPROVE photo-realistic preview.
  Real users actually wanted a 360° spin (didn't predict). Added to "What delights"
  with provenance.
- 2026-06-01 (calibration): Dušan predicted veto on missing edge-banding. Real users
  in segment care more about hinge SKU (3 of 4 interview signals). Updated veto
  ranking — hinge SKU now top criterion, edge-banding second.
```

The CHANGELOG is what `validation/INSIGHT_QUALITY.md` reads to detect "this persona keeps shifting" patterns. Don't squash entries; the history matters.

## When a persona consistently fails calibration

If a persona keeps predicting wrong over 3+ calibration cycles, one of:

1. **The persona was never grounded enough.** Go back to `research/METHODOLOGY.md` — the original sources may have been too thin or too biased. Re-research.
2. **The market shifted.** The product or audience changed and the persona is now describing yesterday's user. Replace, don't patch.
3. **The artifacts they're reviewing are outside their actual perspective.** A user persona shouldn't be asked to review backend architecture. Add routing rules in `_council.yaml` so the persona is only convened for relevant artifacts.

## Forbidden moves

- **Updating a persona to fit the team's preferred narrative.** If you're tempted to soften a persona's veto because the team really wants to ship the feature: stop. The point of the council is to hold the team accountable to user reality, not to be a focus group you can tune until it agrees.
- **Deleting CHANGELOG entries.** Never remove evidence of past predictions, even when they were wrong. The history is what makes the current persona trustworthy.
- **Calibrating against the wrong segment.** If a feature was used predominantly by Power Users but you calibrate Eva against their feedback, you'll corrupt Eva. Make sure each calibration touchpoint actually represents the persona's segment.

## A worked example

Quarter 1 (2026-Q1): Council convened ~12 times on Ponkoid features. Dušan predicted VETO on 4 features citing missing CNC-ready details. We shipped 3 of those anyway (overrode his veto with eng compromises). Result:

- 2 of 3 generated tickets from carpenter-segment users in the next 30 days, citing exactly what Dušan flagged.
- 1 of 3 was actually fine — turns out his veto criterion was over-strict for that case.

Calibration response:
- Dušan's persona file CHANGELOG gets two "VERIFIED" entries (the 2 that bit us) and one "REFINED" entry (the 1 that didn't — added context to the veto criterion specifying which CNC paths it actually applies to).
- Council now has 3 more data points; future sessions are more grounded.

This is what calibration looks like in steady state. Ongoing, low-ceremony, traceable.
