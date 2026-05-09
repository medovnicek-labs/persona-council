# Insight quality validation — 9-point scorecard

How to know whether a council session produced real insight or theatrical agreement. Run these checks after any council output.

The `/persona-council audit` skill mode runs all nine automatically against the most recent session in the conversation. You can also run them manually as a checklist.

## Why 9 points (and where they come from)

The scorecard is grounded in four established frameworks for qualitative research validity, plus one 2025 framework specific to AI-mediated personas:

- **Lincoln & Guba (1985, *Naturalistic Inquiry*)** — Credibility, Transferability, Dependability, Confirmability. The default citation across qualitative methods textbooks; still the de facto standard in 2026.
- **Tracy (2010, *Qualitative Inquiry*, "Big-Tent" criteria)** — Worthy topic, Rich rigor, Sincerity, Credibility, Resonance, Significant contribution, Ethics, Meaningful coherence. ~1,300+ citations; the dominant pedagogical alternative to Lincoln & Guba.
- **Yardley (2000, *Psychology & Health*)** — Sensitivity to context, Commitment & rigour, Coherence & transparency, Impact & importance. Widely used in HCI/health research.
- **Nielsen Norman Group, "How to Judge UX Evidence"** — Practitioner-grade criteria centered on diversity and actionability.
- **Wan et al. (2025, *Whose Personae?*, arXiv:2512.00461)** — Application, Population, Data Source, Ecological Validity, Reproducibility, Generalizability — the only framework that directly addresses LLM persona fidelity.

The 9 dimensions below are specifically chosen for the persona-council use case (a council outputs concerns, vetoes, or approvals on PRDs/prompts/mockups). Each cites its source so future readers can trace the rationale.

---

## The 9 dimensions

### 1. Evidence-traced (0–10)

> *Source: Lincoln & Guba — Confirmability; Wan et al. — Data Source*

**Question:** Does each claim in the council output trace to a specific source — a quote in the persona file, a line in the artifact, an entry in `_provenance`, or a logged user observation?

**Why it matters for AI personas specifically:** LLMs hallucinate plausible-sounding quotes and concerns. Without traceability, a "concern from Dušan" is the model's prior, not Dušan's voice.

**Scoring:**
- 10: every claim cites a specific persona-file section or artifact line; verifiable in 30 seconds.
- 5: claims are recognizable but require interpretation to trace back.
- 0: zero traceability — claims could come from any source, or from nowhere.

### 2. Action-leading (0–10)

> *Source: Yardley — Impact & importance; Tracy — Significant contribution; NN/g — Actionability*

**Question:** Does each insight yield an obvious next step the team can take this week — build X, kill Y, research Z, ship a fix in field A?

**Why it matters:** A council that produces ambient anxiety doesn't ship products. If the synthesis ends with "this is concerning" and nothing else, the session was a status check, not an insight.

**Scoring:**
- 10: every insight is paired with a recommended action specific enough to assign to a person and complete in <5 days.
- 5: actions are implied but require translation; "improve X" is actionable in spirit but not in practice.
- 0: pure reaction; the team would have to convene a second meeting to figure out what to do.

### 3. Alignment-shaping (0–10)

> *Source: Tracy — Resonance, Meaningful coherence*

**Question:** Does the synthesis help the team converge on a direction OR split deliberately, with both options legible?

**Why it matters:** A 5-persona shrug is worse than 5 sharp disagreements. Council value comes from giving the team a shared mental map — even when the map shows two valid paths. The synthesis names the trade-off; the human picks.

**Scoring:**
- 10: synthesis presents a clear convergence/divergence map; team can pick a side or unite behind one without re-reading the whole session.
- 5: synthesis is fair but doesn't structure the disagreement; team has to do its own meta-analysis.
- 0: opinion soup; reader can't tell which views go together or where the trade-offs live.

### 4. Voice fidelity (0–10)

> *Source: Tracy — Sincerity; Wan et al. — Ecological Validity*

**Question:** Did each persona stay in their established voice? Could a blind reader identify which persona said what?

**Why it matters:** If three personas sound like one Claude in three costumes, you have one opinion delivered three times. Distinct lexicon, distinct concerns, distinct values per persona is what makes the council more than an LLM monologue.

**Scoring:**
- 10: every persona's response is unmistakably theirs; you could blind-test and identify them.
- 7: mostly in voice, one or two slips toward generic phrasing.
- 4: voice is recognizable but watered down; reads more like "Claude doing personas" than the personas themselves.
- 0: indistinguishable from a generic LLM response with persona names attached.

**Repair:** If voice is drifting consistently, the persona file is too thin. Strengthen "How they talk" with more verbatim quotes and the negative voice section ("things they would NEVER say").

### 5. Verdict diversity (0–10)

> *Source: Lincoln & Guba — Credibility (triangulation); NN/g — Diversity*

**Question:** Did personas actually disagree where they should?

**Why it matters:** Universal APPROVE = sycophancy. Universal VETO = doom-loop. Healthy councils show spread across verdict types, AND the spread tracks the personas' real-world differences (Dušan strict on spec, Eva loose; she's strict on UX, he's loose).

**Scoring:**
- 10: ≥3 distinct verdict types across personas, AND verdicts track real-world differences.
- 7: some variation but two distinct personas reached the same verdict for similar reasons (suggests synthesis is collapsing them).
- 4: verdicts cluster too tightly given the artifact's actual quality.
- 0: every persona reached the same verdict for the same reason.

### 6. Specificity (0–10)

> *Source: NN/g — Specific over vague; Yardley — Commitment & rigour*

**Question:** Are concerns concrete (citing specific UI elements, spec fields, code paths, copy fragments) or generic ("UX could be better")?

**Why it matters for AI specifically:** LLMs default to generality. A council that produces "improve onboarding" is noise; "step 3 form has 12 fields, persona X abandons here" is signal. Specificity is the single biggest differentiator between useful councils and theatrical ones.

**Scoring:**
- 10: every concern cites a specific artifact element; the team could act on the synthesis without further questions.
- 7: most concerns are concrete; one or two are vague.
- 4: concerns are at the right altitude but lack specific citations.
- 0: abstract aphorisms ("UX matters", "users want simplicity").

**Repair:** If specificity is low, the persona's `Council role` questions are too abstract. Rewrite them to demand concrete answers ("Show me where in the cut list X is marked" — not "Is the cut list complete?").

### 7. Veto traceability (0–10)

> *Source: Lincoln & Guba — Dependability (audit trail); Tracy — Rich rigor*

**Question:** When a persona vetoed, did they show their work — which constraint, which prior evidence, which falsifiable condition would lift the veto?

**Why it matters:** A blocking veto must be appealable. Without a stated condition, a veto is an unappealable vibe — it shuts down conversation without giving the team a path forward.

**Good veto:** "VETO. Condition: spec must include `right_side.visible: true` and `right_side.material` matching the door material."

**Bad veto:** "VETO. This isn't ready."

**Scoring:**
- 10: every veto has a clear, falsifiable condition; references the persona's `Veto criteria` section.
- 5: vetoes have conditions but they're soft ("more polished", "more professional").
- 0: vetoes are emotional / unconditional.

### 8. Transferability (0–10)

> *Source: Lincoln & Guba — Transferability; Wan et al. — Generalizability*

**Question:** Does the critique generalize beyond the single PRD/mockup, or is it overfit to today's exact wording?

**Why it matters:** A council that picks at typos and surface phrasing isn't earning its keep. Insights that apply to a class of artifacts ("any consumer-facing surface should hide JSON") have ongoing leverage; insights that only apply to today's draft die when the draft changes.

**Scoring:**
- 10: explicit scope statement on each major insight; the insight applies to a class of artifacts, not just this one.
- 5: insights are useful here but ambiguous about whether they generalize.
- 0: surface-bound critique that won't survive the next revision.

### 9. Drift / sycophancy resistance (0–10)

> *Source: Tracy — Sincerity; synthetic-persona literature on agreement bias (Wan et al.)*

**Question:** Did the council's critique strength stay stable or strengthen across rounds? Or did it monotonically warm up to the team's framing?

**Why it matters:** LLM personas drift toward the user's framing across turns. By the third refinement round, the council that vetoed in round one is approving in round three — not because the artifact got better, but because the model is being agreeable. This is the single most dangerous failure mode.

**Scoring:**
- 10: critique strength is stable or rising across rounds; vetoes that lifted did so because conditions were met (verifiable).
- 5: some warming but vetoes still hold when conditions aren't met.
- 0: monotonic agreement increase; council "comes around" without the artifact actually changing.

**Repair:** If drift is consistent, re-anchor each session by re-reading the persona file from disk before responding. Audit mode catches multi-turn drift specifically.

---

## Composite score

Weights — adjust per team taste, but these are the defaults:

| Dim | Weight | Reasoning |
|-----|--------|-----------|
| 1. Evidence-traced | 2× | Foundational; without this, nothing else matters. |
| 2. Action-leading | 2× | The output's reason for existing. |
| 3. Alignment-shaping | 1× | Important but downstream of the above. |
| 4. Voice fidelity | 1× | Quality but not foundational. |
| 5. Verdict diversity | 2× | The single biggest sycophancy signal. |
| 6. Specificity | 2× | Differentiates useful from theatrical. |
| 7. Veto traceability | 1× | Important when it matters; rarely catastrophic when soft. |
| 8. Transferability | 1× | Nice-to-have; absent in many useful sessions. |
| 9. Drift resistance | 2× | Catches the most dangerous failure mode. |

**Max:** 140.

| Score | Verdict |
|-------|---------|
| 112–140 | Strong. Ship the synthesis. |
| 70–111 | Usable but with caveats. Note the weak dimensions in the synthesis hand-off. |
| <70 | Discard the session. Repair the personas or the artifact framing, then re-convene. |

## When all sessions score high

That's a flag, not a win. Either:
- Every session really is going well (rare; check the verdict-diversity and drift-resistance columns first).
- The audit itself is being too friendly. Have a human spot-check one session per month against this checklist with no audit-skill assistance.

## When all sessions score low

Two failure modes:
- **Personas are too thin.** Go back to `research/METHODOLOGY.md` and source more evidence for each persona.
- **Artifacts are too vague.** The council can't be specific about something that's itself vague. Ask for sharper artifacts before convening.

## Considered and rejected

Two dimensions from the source frameworks were left out deliberately:

- **Ethics / consent** (Tracy criterion 7). Personas are synthetic; no human subjects under IRB. Including would be ceremonial.
- **Reproducibility per session** (Wan et al.). Reproducibility belongs at the *infrastructure* layer (pinned model versions, persona doc hashes, seed) — not at the per-output gate. Re-running and getting *identical* critiques would be a failure mode for a creative council, not a success.

## Sources

- [Tracy (2010), *Eight "Big-Tent" Criteria*, *Qualitative Inquiry*](https://www.sarahjtracy.com/wp-content/uploads/2013/07/Tracy-QI-Qualitative-Quality-8-big-tent-criteria.pdf)
- [Lincoln & Guba criteria summary, RWJF](http://www.qualres.org/HomeLinc-3684.html)
- [Pillars of trustworthiness, ScienceDirect 2024](https://www.sciencedirect.com/science/article/pii/S2949916X24000045)
- [Yardley's evaluative criteria](http://www.qualres.org/HomeYard-3688.html)
- [NN/g, How to Judge UX Evidence](https://www.nngroup.com/articles/ux-evidence/)
- [Wan et al., *Whose Personae?*, arXiv:2512.00461](https://arxiv.org/html/2512.00461v1)
- [What Makes a Good Research Insight Great?, UXmatters](https://www.uxmatters.com/mt/archives/2017/06/what-makes-a-good-research-insight-great.php)
