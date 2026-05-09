# Interview guide

Question templates for user interviews that produce council-ready personas. Adapt freely; don't read the script.

## Setup (5 min)

- Record (with consent). Note-taking alone loses voice.
- State the goal: "We're trying to understand how you actually work, not pitch you on anything. There are no wrong answers."
- Confirm time budget. Aim for 60 min; have a 30-min escape hatch ready.

## Section 1 — Their world (15–20 min)

Goal: ground them in their real workflow before product-specific questions bias the conversation.

- "Walk me through your last [project / use case / typical day]. Start from the beginning — when did the work start? What triggered it?"
- "Where did things get hard? Tell me about the most frustrating moment."
- "Who else was involved? Where did handoffs happen?"
- "What tools did you use? Why those?"

What you're listening for:
- Their **vocabulary** (capture exact phrases — these go in the persona file).
- The **sequence** of their workflow (your product likely fits in *somewhere*; understand where).
- Adjacent **stakeholders** (sometimes the real persona is the person they hand off to, not them).

Anti-pattern: skipping this section "to save time." Without it, every later answer is colored by your product framing.

## Section 2 — The pain point (15 min)

Goal: pin down a specific recent failure of the status quo, in their words.

- "Tell me about the last time [the problem your product addresses] cost you real time or money."
- "What did you do? What was your workaround?"
- "If a friend in the same situation asked you for advice today, what would you tell them?"

What you're listening for:
- Whether the pain point is **acute** (worth changing tools for) or **chronic-but-tolerable** (people will say "yeah it's annoying" but won't switch).
- Their **current solution** — even a bad one is your real competitor. "I just do it manually" is more honest than "I use [competitor]."
- The **cost they actually paid** in time, money, or relationships. If they can't quantify, the pain may not be real.

Anti-pattern: leading with "wouldn't it be great if [your feature]?" — they will agree to be polite and you will misread it as demand.

## Section 3 — Their reality with the product (15 min)

Now you can get specific. If they've used the product, skip to (a). If they haven't, do (b).

### (a) Existing user

- "Show me how you actually use it. Share your screen — pretend I'm not here."
- (Watch them. Don't help. Note where they pause, swear, or close the tab.)
- "What did you expect to happen there?" (when behavior surprised them)
- "What do you wish it did that it doesn't?"
- "What does it do that you wish it didn't?" (negative space — often more revealing)

### (b) Prospective user

- "I'm going to walk you through a quick demo. Tell me what's confusing as I go."
- (Demo. Pause every ~2 minutes. Let them ask questions; don't preempt.)
- "If you were going to try this for a real project, what would have to be true?"

What you're listening for:
- The **moment they got lost** (this is where the UX needs work, not where they confirmed they were lost).
- Things they **assumed but were wrong about** (mismatched mental models = onboarding work).
- Words they used that don't match your UI's vocabulary.

## Section 4 — The veto question (5 min)

Goal: surface their non-negotiables.

- "What would have to happen for you to stop using this and go back to your old way?"
- "If we shipped one feature next week that was a complete deal-breaker for you, what would it be?"
- "Is there anything we showed you today that genuinely worried you?"

What you're listening for:
- Hard veto lines — these become the persona's `Veto criteria` section.
- Soft worries (often more real than hard vetoes — people understate dealbreakers in interviews).

## Section 5 — Close (5 min)

- "Anything I should have asked but didn't?"
- "Can I follow up if a specific question comes up later?"
- "Would you be willing to test an early version of [the next thing]?"

A "yes" to the third question turns a one-off interview into an ongoing relationship — the highest-signal source you can have. Treasure those people.

## Synthesis right after

Within 24 hours of the interview, while voice is fresh:

1. Re-listen to the recording at 1.5×.
2. Pull verbatim quotes for: vocabulary they use, things they want, things they distrust, veto criteria.
3. Update the relevant persona file (or draft a new one) — don't wait for "more interviews to be sure." Let the file evolve.

## Red flags during an interview

- They keep agreeing with everything. → You're leading. Try silence.
- They use jargon you didn't expect. → Don't translate it; ask them to explain. The phrasing is the value.
- They keep referring to a person who's not in the call. → That person may be the actual persona.
- They ask you a lot of questions about your roadmap. → They're a salesperson, not a user. Politely close out.
