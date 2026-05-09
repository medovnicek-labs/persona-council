# Changelog

## v0.1.0 — 2026-05-09

Initial public release.

- `/persona-council` skill: convenes auto-discovered personas from `<cwd>/docs/personas/council/*.md`. Routing rules via `_council.yaml`. Cross-portfolio overlay support.
- `/persona-council audit` mode: validates voice consistency, verdict diversity, specificity, veto traceability, persona drift. Proposes (never silently writes) persona-file edits.
- `/persona-research` skill: turns raw user-research notes into council-ready persona files.
- Research methodology (`research/`): METHODOLOGY, INTERVIEW_GUIDE, SYNTHESIS_TEMPLATE, persona-template.
- Insight quality framework (`validation/`): INSIGHT_QUALITY scorecard, CALIBRATION protocol against real user behavior.
- Portfolio mapping (`docs/PORTFOLIO_MAPPING.md`, `mapping.yaml`): how to share personas across multiple products.
- Examples: Ponkoid's Dušan (real carpenter) + Eva (synthetic consumer) with `_council.yaml`.
- MIT licensed.
