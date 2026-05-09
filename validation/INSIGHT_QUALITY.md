# Insight quality scorecard — 5-dimension MECE framework

How to know whether a council session produced real insight or theatrical agreement. Five dimensions, mutually exclusive, collectively exhaustive. Run after any council output.

The `/persona-council audit` skill mode runs all five automatically against the most recent session. You can also run them manually as a checklist.

## Why 5, not 9

An earlier draft gave 9 dimensions drawn from Lincoln & Guba, Tracy, Yardley, NN/g and Wan et al. Honest re-read: those 9 weren't MECE — "coherence", "resonance", and "meaningful coherence" were three labels for one underlying construct, and several dimensions double-counted what others already measured.

This v2 framework collapses the field along a single spine: **inputs → interpretation → epistemic form → consequence → bias structure**. Every meaningful failure mode of qualitative insight (and the LLM-specific one) lands in exactly one dimension. See **MECE check** below for the proof.

## Why these sources

- **Geertz (1973), "Thick Description"** — the canonical statement of what makes ethnography ethnographic (winks vs twitches). [PDF](https://people.ucsc.edu/~ktellez/geertz1973.pdf)
- **Spradley (1979), *The Ethnographic Interview*** — the Developmental Research Sequence; "informant talk" priority. [Publisher](https://www.waveland.com/browse.php?t=688)
- **Wolcott (1990), "Making a Study More Ethnographic"** — distinguishes ethnographic *intent* from *technique*. [JSTOR](https://journals.sagepub.com/doi/10.1177/089124190019001003)
- **Indi Young, *Listening Deeply*** — interior cognition and emic logic surfacing. [Essay](https://indiyoung.com/explanations-listening-deeply/)
- **Teresa Torres, *Continuous Discovery Habits*** — opportunity solution trees, assumption→hypothesis translation. [Book site](https://www.producttalk.org/) · [Trees post](https://www.producttalk.org/opportunity-solution-trees/)
- **Tony Ulwick, Outcome-Driven Innovation** — desired-outcome statements (verb + metric + object + context, "stable, measurable, solution-free"). [JTBD piece](https://jobs-to-be-done.com/inventing-the-perfect-customer-need-statement-4fb7de6ba999)
- **Eric Ries, *The Lean Startup*** — leap-of-faith assumptions, validated learning. [Site](https://theleanstartup.com/book)
- **Heath & Heath, *Decisive* (WRAP)** — "consider the opposite," reality-test assumptions. [Site](https://heathbrothers.com/books/decisive/)
- **Nielsen Norman Group** — practitioner insight quality writing.
- **Lincoln & Guba (1985), *Naturalistic Inquiry*** — confirmability + credibility (still the textbook baseline). [Summary](http://www.qualres.org/HomeLinc-3684.html)
- **Wan et al. (2025), *Whose Personae?*, arXiv:2512.00461** — synthetic-persona LLM validity.

---

## The 5 dimensions

### 1. Grounding (0–10)

> *Governs: inputs (where claims come from)*
>
> *Sources: Lincoln & Guba — confirmability + credibility; Spradley — informant talk priority (DRS steps 2–4); NN/g — diversity over volume*

**Definition:** Every claim in the council output is traceable to a specific person, utterance, behavior, or artifact rather than to the LLM's prior.

**Why it matters specifically for AI personas:** LLMs hallucinate plausible quotes. Without grounding, a "concern from Dušan" is the model's prior wearing Dušan's name. The single highest-leverage anti-slop check.

**Rubric:**
- **10** — every non-trivial claim cites a specific input (transcript line, support ticket, prior session, observed behavior); the persona could not have produced this claim without that input.
- **5** — mixes grounded fragments with confident generalizations.
- **0** — ungrounded assertions only; could be the base model talking.

### 2. Thickness (0–10)

> *Governs: interpretation depth (how meaning is constructed from inputs)*
>
> *Sources: Geertz — thick description (the wink); Wolcott — ethnographic intent; Indi Young — interior cognition*

**Definition:** Findings explain the **meaning, intent, and context** behind behavior — not just the behavior itself.

**Why it matters specifically for AI personas:** LLMs default to thin description ("user wants faster checkout"). Thickness forces the council to surface the *why* — emic logic, emotional reaction, guiding principle — which is where real product moves live. A thin council output describes the twitch; a thick one explains the wink.

**Rubric:**
- **10** — behavior + intent + context + at least one emic frame the team could not have written from memory.
- **5** — behavior plus one motivational layer.
- **0** — pure behavioral surface; no interpretation.

### 3. Falsifiability (0–10)

> *Governs: epistemic form (how a claim could be wrong)*
>
> *Sources: Ries — leap-of-faith assumptions, validated learning; Torres — assumption→hypothesis translation; Popper underneath both*

**Definition:** Each insight is stated such that a future observation could prove it wrong.

**Why it matters specifically for AI personas:** Persona output trends toward unfalsifiable poetry ("users feel a deep desire for craft"). Falsifiability is the gate between insight and experiment — the line between Lean Startup *validated learning* and aspirational consensus. Without it, the council is theatre.

**Rubric:**
- **10** — each major claim is paired with the specific observation, metric, or threshold that would disconfirm it.
- **5** — claims are testable in principle but no metric/threshold given.
- **0** — no testable claims.

### 4. Actionability (0–10)

> *Governs: consequence (what the team does next)*
>
> *Sources: Ulwick — desired-outcome statement format; Torres — opportunity solution tree*

**Definition:** Findings convert into a concrete product move — opportunity, outcome statement, or experiment — with the unit of work named.

**Why it matters specifically for AI personas:** Council output that doesn't change next week's roadmap is decoration. Actionability makes "so what?" answerable in one sentence, in a form the team can put on the board.

**Rubric:**
- **10** — each major finding yields a named opportunity, JTBD outcome statement, or experiment with success criteria, traceable to a specific finding.
- **5** — generic implications ("we should improve onboarding").
- **0** — pure observation; nothing to do.

### 5. Adversariality (0–10)

> *Governs: bias structure (what the council resists agreeing with)*
>
> *Sources: Heath & Heath — WRAP "consider the opposite"; Kahneman pre-mortem; Wan et al. on synthetic-persona agreement bias*

**Definition:** The council surfaces disconfirming evidence, persona disagreement, and at least one finding that contradicts the team's prior or business interest.

**Why it matters specifically for AI personas:** Multi-persona LLMs collapse to consensus by default — the same base model agreeing with itself in five voices. Without an adversariality score, the council systematically launders confirmation bias as validation. This is the most dangerous failure mode and the one most invisible to the team that built it.

**Rubric:**
- **10** — at least one persona produces a finding that, if true, would kill the proposed feature, AND the team cannot easily dismiss it.
- **5** — personas disagree on minor points; major direction unanimously approved.
- **0** — unanimous, flattering; the council "loved" the artifact.

---

## MECE check

Each dimension governs a distinct layer of the insight pipeline:

| Layer | Dimension | Question it answers |
|-------|-----------|---------------------|
| Inputs | **Grounding** | Where do the claims come from? |
| Interpretation | **Thickness** | How was meaning constructed from those inputs? |
| Epistemic form | **Falsifiability** | How could the claim be proven wrong? |
| Consequence | **Actionability** | What does the team do next? |
| Bias structure | **Adversariality** | What did the council resist agreeing with? |

**Mutually exclusive:** no dimension's score depends on another's. A council can be:
- highly grounded but thin (transcript quotes, no meaning)
- thick but unfalsifiable (rich ethnography, no test)
- falsifiable but unactionable (testable but trivial)
- actionable but ungrounded (decisive but invented)
- adversarial but ungrounded (theatrical disagreement)

Any of these failure modes is recoverable by improving exactly one dimension.

**Collectively exhaustive:** the four canonical failure modes of qualitative insight work are (1) thin source material, (2) shallow interpretation, (3) untestable claims, (4) unimplementable conclusions — covered by Grounding / Thickness / Falsifiability / Actionability. The fifth, Adversariality, is the LLM-specific failure mode (consensus collapse) that doesn't appear in pre-AI frameworks because human research subjects don't all share the same base model. With those five, every meaningful way a council output can be wrong is named.

---

## Composite score

Equal weighting unless your team has a reason to skew. Max: 50.

| Score | Verdict |
|-------|---------|
| 40–50 | Strong. Ship the synthesis. |
| 25–39 | Usable but flag the weakest dimension explicitly in the hand-off. |
| <25 | Discard the session. Repair personas, sharpen the artifact, or improve the prompt before re-convening. |

**When to skew weights:** if the team has a recurring failure mode (e.g., consistently high specificity but low adversariality), double-weight the failing dimension for the next 30 days to force attention there. Reset to equal weights after recalibration.

## When all sessions score high

That's a flag, not a win. Either:
- The council really is producing strong insight — verify by checking whether shipped features were predicted correctly (see `CALIBRATION.md`).
- The audit is being too friendly. Spot-check one session per month with a human reading the rubric directly, no audit-skill assistance.

## When all sessions score low

Two failure modes to investigate first:
- **Personas are too thin.** Most low-Grounding sessions trace here. Go back to `research/METHODOLOGY.md` and source more evidence.
- **Artifacts are vague.** The council can't be specific about something that's itself vague. Insist on sharper PRDs/prompts before convening.

---

## What changed from the 9-dim v1

| v1 dimension | v2 home | Notes |
|---|---|---|
| Evidence-traced | **Grounding** | Renamed; identical concept. |
| Specificity | **Grounding + Actionability** | Was doing two jobs — split between input quality and output usefulness. |
| Voice fidelity | dropped | Belongs in council *mechanism* QA (is the persona file rich enough?), not *insight* quality. Tracked separately in `CALIBRATION.md`. |
| Verdict diversity | **Adversariality** | Sharpened — diversity isn't enough; need *productive* disagreement. |
| Veto traceability | **Falsifiability** | A veto needs a falsifiable lift condition; same construct. |
| Action-leading | **Actionability** | Renamed. |
| Alignment-shaping | dropped | Was a softer restatement of Actionability + Adversariality combined. |
| Transferability | dropped | Important for academic work; not how product councils get used (each session is bound to a specific artifact). |
| Drift / sycophancy resistance | **Adversariality** | Folded in — drift is the multi-turn version of consensus collapse. |

Honest note: the v1 framework rewarded vocabulary, not signal. v2 is shorter because it stopped re-stating the same construct in three different academic dialects.

## Considered and rejected for v2

- **Novelty** (does the council surface something the team didn't already know?) — tempting, but it's a *function of* Grounding × Thickness × Adversariality. Scoring it separately double-counts.
- **Persona fidelity** (does each persona stay in character?) — matters for council *mechanism* QA, not *insight* quality. Belongs in `CALIBRATION.md`.
- **Coherence / Resonance / Meaningful coherence** (Tracy / Yardley) — three labels for one writing-quality construct. Dropped: not insight quality.
- **Ethical reflexivity** — important separately (governance, IRB-equivalent), but not a per-output gate for synthetic personas.
- **Reproducibility per session** — belongs at infrastructure (pinned model versions, persona doc hashes), not the per-output gate. Re-running and getting *identical* critiques would be a failure mode for a creative council.
