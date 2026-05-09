---
name: persona-council
description: Convene a multi-persona critique council for any feature, PRD, prompt, mockup, or shipped output. Auto-discovers personas from the current project's docs/personas/council/, falls back to bundled examples. Use when the team needs cross-persona pressure-testing, when a stakeholder review feels too friendly and you suspect groupthink, or before declaring a feature done. Includes /persona-council audit mode for insight-quality validation.
---

# Persona Council — Universal

Convenes a council of user/stakeholder personas to critique a piece of work. Each persona reviews from their own perspective and surfaces concerns, blind spots, or contradictions the team would otherwise ship past.

This skill is **portfolio-aware** and **project-agnostic** — it discovers personas from the current project's filesystem. Drop persona files in the right place and the skill picks them up automatically.

## Discovery order

When invoked, the skill loads personas from the **first** of these paths that contains `*.md` files:

1. `<cwd>/docs/personas/council/*.md` — preferred for repo-rooted projects (e.g., Ponkoid)
2. `<cwd>/personas/council/*.md` — alt path for monorepos with different layouts
3. `<cwd>/.persona-council/*.md` — fully opt-in, hides personas from the docs tree
4. The skill's bundled `examples/<product>/` — fallback for first-time users (with a console warning)

A `_council.yaml` in the same directory configures the council. See "Council config" below.

## Modes

### Default — convene a council

Invocation: `/persona-council` (with the artifact in the conversation), or proactively when you notice a review needs pressure-testing.

1. **Load personas.** Read every `*.md` in the discovered persona directory. Each persona's `Council role` section is the question battery for this session.

2. **Quote the input verbatim.** Do not paraphrase what the council is reviewing — quote it directly so personas react to the actual artifact, not your summary.

3. **For each persona in turn, IN THEIR VOICE:**
   - Open with one sentence reacting to the input from their perspective.
   - Run their `Council role` questions against the input. Answer each in-character (1–2 sentences each).
   - Issue a verdict: **APPROVE**, **CONDITIONAL** (state the condition), or **VETO** (state what would have to change).

4. **Synthesize across personas:**
   - **Agreement** — what every persona endorses (safe directions).
   - **Conflict** — where personas pull opposite ways. Name the trade-off explicitly. **Do NOT resolve it yourself; flag it for the human.**
   - **Unique surfaces** — concerns only one persona raised (often the most valuable signal).

5. **Hand back to the human** with a one-line decision prompt, e.g. "Council is split on X. Pick a direction and I'll proceed."

### Audit mode — validate insight quality

Invocation: `/persona-council audit` (after a recent council session in the same conversation).

Runs the checks documented in `validation/INSIGHT_QUALITY.md` against the most recent council output:

- **Voice consistency** — did each persona stay in their established voice? If Dušan started saying "the user experience could be better," that's drift.
- **Verdict diversity** — did personas actually disagree where they should? An all-APPROVE result usually means the council was rubber-stamping.
- **Specificity** — are concerns concrete (citing specific UI elements / spec fields) or generic ("should be more polished")?
- **Veto traceability** — when a persona vetoed, was the falsifiable condition stated?
- **Persona drift** — does any persona's voice in this session contradict their persona file? If so, propose a persona-file update rather than re-running with a "corrected" voice.

Outputs a quality scorecard (0–10 per check) and a **proposed list of persona-file edits** if drift was detected. The human approves or rejects the edits — the skill never silently rewrites a persona.

### Research handoff

This skill does NOT do persona research itself. Use the sibling `/persona-research` skill (in the same repo) to convert raw user-research notes into persona files compatible with this skill's discovery format.

## Council config (`_council.yaml`)

Optional file in the persona directory that configures defaults:

```yaml
# personas/council/_council.yaml
product: ponkoid
description: Consumer + carpenter personas for the Ponkoid wardrobe designer.

# Default council composition. Omit to convene every persona file in this dir.
default_personas:
  - dusan-carpenter
  - eva-consumer

# Optional: artifact-type → persona subset routing.
# Lets you skip irrelevant personas based on what's being reviewed.
routing:
  prd: [dusan-carpenter, eva-consumer]
  prompt: [dusan-carpenter]               # eva won't see raw prompt engineering
  ui-mockup: [eva-consumer]               # dusan only cares about cut lists
  cut-list: [dusan-carpenter]
  marketing-copy: [eva-consumer]

# Optional: cross-portfolio overlay. If set, this skill will additionally
# load personas from <cross_portfolio_path>/<persona-name>.md before the
# project-local ones (the latter override). Useful for personas shared
# across multiple Medovnicek products (e.g., the founder persona).
cross_portfolio_path: ~/my-git/persona-council/examples/_shared
```

Routing rules let you avoid wasting Eva's tokens on a JSON spec she'd never see. The skill picks routing keys from your invocation phrasing — "review this PRD" → `prd`, "review this prompt" → `prompt`, etc. Default if no match: convene `default_personas`.

## Anti-patterns

- **Don't water down their voice.** If Dušan would say "podla toho by som to nespravil," write that — not "this needs improvement."
- **Don't resolve conflicts in the synthesis.** The point of a council is to surface disagreement. If every persona agrees, you weren't pressure-testing — you were rubber-stamping.
- **Don't invoke the council for trivial decisions.** Naming a CSS variable doesn't need it. Use it for input that would meaningfully affect a real persona's experience.
- **Don't run the council against itself** ("should we add a third persona?") — that's a meta-decision for the human.
- **Don't silently update persona files.** When `audit` mode finds drift, it proposes edits. The human approves.

## When to update a persona file

After a real user does something the persona did not predict (positive or negative), update the persona file with the contradicting signal **before** the next council session. The file is a living record, not a write-once artifact. See `validation/CALIBRATION.md` for the protocol.

## Repo

This skill ships from [`medovnicek-labs/persona-council`](https://github.com/medovnicek-labs/persona-council). Run `cd ~/.claude/skills/persona-council && git pull` to update. PRs and forks welcome.
