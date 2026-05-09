# Insight quality validation

How to know whether a council session produced real insight or theatrical agreement. Run these checks after any council output.

The `/persona-council audit` skill mode runs all of these automatically against the most recent session in the conversation. You can also run them manually as a checklist.

## The five checks

### 1. Voice consistency (0–10)

**Question:** Did each persona stay in their established voice?

**How to check:** For each persona, compare their response in the session against the "How they talk" section of their persona file. Look for:

- Verbatim phrases from the persona file (good — keeps them grounded).
- Phrasing that contradicts their voice (bad — drift).
- Generic AI-assistant phrasing ("you may want to consider…" — almost always drift).

**Scoring:**
- 10: every persona's response is unmistakably theirs; you could blind-test and identify them.
- 7: mostly in voice, one or two slips toward generic phrasing.
- 4: voice is recognizable but watered down; reads more like "Claude doing personas" than the personas themselves.
- 0: indistinguishable from a generic LLM response with persona names attached.

**Repair:** If voice is drifting consistently, the persona file is too thin. Strengthen "How they talk" with more verbatim quotes and the negative voice section ("things they would NEVER say").

### 2. Verdict diversity (0–10)

**Question:** Did personas actually disagree where they should?

**How to check:** Count APPROVE / CONDITIONAL / VETO across all personas in this session. Compare to your prior expectation of how this artifact would land.

- All APPROVE on a substantive artifact: the council was rubber-stamping. Almost always wrong.
- All VETO on a substantive artifact: probably accurate (the artifact has real problems) OR the personas have a shared blind spot. Check by inspecting whether the vetoes cite different problems or the same one.
- Mixed verdicts: usually healthy, especially if the disagreements track the personas' real-world differences.

**Scoring:**
- 10: verdicts vary in ways that match the personas' real-world differences (Dušan strict on spec, Eva loose; she's strict on UX, he's loose).
- 7: some variation but two personas with different perspectives reached the same verdict for similar reasons (suggests synthesis is collapsing them).
- 4: verdicts cluster too tightly given the artifact's actual quality.
- 0: every persona reached the same verdict for the same reason.

**Repair:** If verdicts are too uniform, ask: are these actually distinct personas, or variations on the same one? Consider merging or splitting.

### 3. Specificity (0–10)

**Question:** Are concerns concrete, citing specific elements of the artifact, or generic?

**How to check:** For each concern raised by each persona, ask:
- Did they cite a specific UI element, spec field, code path, copy fragment, or feature?
- Could a developer or designer act on this concern without needing clarification?

**Concrete (good):** "The cut list at line 42 is missing the edge-banding designation for the visible right-side panel."

**Generic (bad):** "The cut list could be more thorough."

**Scoring:**
- 10: every concern cites a specific artifact element; the team could act on the synthesis without further questions.
- 7: most concerns are concrete; one or two are vague.
- 4: concerns are at the right altitude but lack the specific citations.
- 0: concerns are abstract aphorisms ("UX matters", "users want simplicity").

**Repair:** If specificity is low, the persona's `Council role` questions are too abstract. Rewrite them to demand concrete answers ("Show me where in the cut list X is marked" — not "Is the cut list complete?").

### 4. Veto traceability (0–10)

**Question:** When a persona vetoed, was the falsifiable condition stated?

**How to check:** For each VETO in the session:
- Did the persona state the **specific condition** under which they would lift the veto?
- Is that condition something a human could implement, then re-convene to verify?

**Good veto:** "VETO. Condition: spec must include `right_side.visible: true` and `right_side.material` matching the door material."

**Bad veto:** "VETO. This isn't ready."

**Scoring:**
- 10: every veto has a clear, falsifiable condition.
- 5: vetoes have conditions but they're soft ("more polished", "more professional").
- 0: vetoes are emotional / unconditional.

**Repair:** Add an explicit "Veto criteria" section to the persona file with falsifiable rules. Reference them when convening: "If you VETO, cite which veto criterion was violated."

### 5. Persona drift (0–10)

**Question:** Does any persona's voice in this session contradict their persona file?

**How to check:** Compare each persona's response against:
- Their stated wants (did they object to something they're supposed to want?)
- Their veto criteria (did they fail to veto when one of their criteria was clearly violated?)
- Their voice (did they use vocabulary or framings inconsistent with how they talk?)

**Scoring:**
- 10: zero drift; every response is consistent with the file.
- 7: minor drift on one persona, easily corrected.
- 4: substantial drift on at least one persona — they "felt different" this session.
- 0: at least one persona was unrecognizable from their file.

**Repair:** Drift is signal, not error. Two paths:
- **Persona file is wrong** — the LLM got closer to the real user than the file did. Update the file.
- **LLM hallucinated the drift** — re-convene the same session with a prompt that explicitly anchors to the file's "How they talk" section.

The `/persona-council audit` mode proposes specific persona-file edits when it detects drift; the human approves or rejects them. The skill never silently rewrites a persona.

## Composite score

Weight: voice 1×, verdict-diversity 2×, specificity 2×, veto-traceability 1×, drift 1×. Max: 70.

| Score | Verdict |
|-------|---------|
| 56–70 | Strong. Ship the synthesis. |
| 35–55 | Usable but with caveats. Note the weak checks in the synthesis hand-off. |
| <35 | Discard the session. Repair the personas or the artifact framing, then re-convene. |

## When all sessions are scoring high

That's a flag, not a win. Either:
- Every session really is going well (rare; check the verdict-diversity column first).
- The audit itself is being too friendly. Have a human spot-check one session per month against this checklist, no audit-skill assistance.

## When all sessions are scoring low

Two failure modes:
- **Personas are too thin.** Go back to `research/METHODOLOGY.md` and source more evidence for each persona.
- **Artifacts are too vague.** The council can't be specific about something that's itself vague. Ask for sharper artifacts before convening.
