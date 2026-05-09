# persona-council

> Multi-persona critique councils for AI-native product development.

Convene a council of synthesized + real user personas as critics. Pressure-test PRDs, prompts, mockups, and shipped output before the rubber-stamp instinct kicks in. Built as a [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skill.

```
You:    /persona-council  [shares the latest PRD]
Claude: [Loads docs/personas/council/*.md]
        [Convenes Dušan (carpenter) + Eva (consumer) in their own voices]
        Dušan: "Podla toho by som to nespravil — kde je rozmer pravej bočnice?"
                VETO. Condition: spec must include right-side panel as visible-decor.
        Eva:    "Vypadá jako engineering tool. Nešla bych dál než na první obrazovku."
                CONDITIONAL. Condition: hide the JSON spec from the consumer surface.
        SYNTHESIS: Conflict — Dušan wants more spec detail; Eva wants less. Trade-off
                   is who the surface targets. Pick a direction and I'll proceed.
```

## What's in the box

- **`/persona-council`** — convenes personas; auto-discovers from `docs/personas/council/*.md`. Routing rules let you skip irrelevant personas (Eva doesn't need to see prompt engineering).
- **`/persona-council audit`** — validates the council's own output for voice consistency, verdict diversity, specificity, and persona drift. Proposes (never silently writes) persona-file edits.
- **`/persona-research`** — converts raw interview transcripts / support tickets / NPS comments into structured persona files compatible with the council.
- **Research methodology** (`research/`) — interview guides, synthesis templates, the canonical persona file structure.
- **Insight quality validation** (`validation/`) — anti-sycophancy checks, calibration protocol against real user behavior.
- **Portfolio mapping** (`docs/PORTFOLIO_MAPPING.md`) — how to share personas across multiple products without losing per-product voice.
- **Examples** (`examples/<product>/`) — Ponkoid's Dušan + Eva as a working reference.

## Why this exists

Most "persona" workflows either:
- Use static, fictional personas that drift away from reality and become groupthink.
- Skip personas entirely and let the loudest voice in the room win.

This skill bets on:

1. **Real-user-rooted personas.** Files are versioned, sourced (`_provenance` block), and updated when real users contradict them.
2. **Cross-persona conflict surfacing.** Synthesis names trade-offs explicitly instead of resolving them — humans pick the side.
3. **Self-auditing.** The council's outputs are graded for sycophancy, drift, and specificity. A council that always APPROVE-s is broken.
4. **Portable across the portfolio.** One install, every project benefits. Personas live next to the code they're critiquing.

## Install

Requires [Claude Code](https://docs.anthropic.com/en/docs/claude-code).

```bash
git clone --depth 1 https://github.com/medovnicek-labs/persona-council.git ~/.claude/skills/persona-council \
  && cd ~/.claude/skills/persona-council && ./setup
```

That's it. Both `/persona-council` and `/persona-research` are now available in any Claude Code session. The `setup` script symlinks each skill into Claude Code's discovery layout; re-run after `git pull` to update. See `docs/INSTALL.md` for project-specific setup (where to put your persona files, optional `_council.yaml` config).

## Use it without running it

Even if you don't install the skill, the methodology stands on its own:

- `research/METHODOLOGY.md` — how to interview users and turn the notes into a persona file.
- `research/persona-template.md` — the canonical structure.
- `validation/INSIGHT_QUALITY.md` — checks any team can run on any council output.
- `validation/CALIBRATION.md` — how to keep personas honest as real users ship feedback.

Read these standalone, apply them with whatever tooling you already use.

## Status

`v0.1` — usable, opinionated, not yet battle-tested at scale. Ponkoid (Medovnicek Labs' first product) is the daily-use partner that drives feature work. Expect API-level changes through `v0.x`; lockdown at `v1.0`.

## Contributing

PRs welcome — see `docs/CONTRIBUTING.md`. The most valuable contribution is a **persona file from your own product** that we can include in `examples/` to help others see the pattern in domains beyond furniture.

## License

[MIT](LICENSE) — use anywhere, fork anywhere, no attribution required (though appreciated).

## Built by

[Medovnicek Labs](https://medovnicek.com) — a 2-person studio shipping AI-native products. We use this in our own work; we're sharing it because the same tooling should be available to every tiny team trying to ship like a big one.
