# Contributing

This repo is small and opinionated. PRs welcome — the contribution rules below keep that opinion intact.

## What we want

1. **Real-world persona files for `examples/<product>/`** from your own work. The most valuable contribution is a persona file from a domain we don't yet cover (B2B SaaS, gaming, edtech, healthcare, anything beyond furniture). Strip company-confidential details; keep voice and structure.

2. **Methodology improvements** to `research/` and `validation/`. If you've used the framework on a real project and found a step that didn't work, open an issue with what you'd change.

3. **Bug fixes** in the skill files when discovery, routing, or audit mode behaves unexpectedly. Include a minimal repro.

## What we don't want

1. **Static personas with no provenance.** Every persona file in `examples/` must include the `_provenance` block from the template. Made-up personas don't help anyone.

2. **Marketing-style personas.** "Sarah, 32, lifestyle: yoga + craft beer" — useless for council critique. We will close these PRs.

3. **Feature creep on the skill.** The two skills (`persona-council`, `persona-research`) are deliberately small. Adding a third skill, a UI, a database, a cloud sync — none of this. Open an issue first if you think there's an exception.

4. **AI-generated persona files.** Personas built by asking an LLM "give me a persona for X" are anti-personas — they reflect the LLM's training data, not your users. Hard "no" on these.

## How to contribute a persona

1. Fork.
2. Add `examples/<your-product-or-domain>/<persona-slug>.md` using `research/persona-template.md` as the structure.
3. Optionally add `examples/<your-product-or-domain>/_council.yaml` with routing rules.
4. Add a one-line entry in this repo's `mapping.yaml` (under a new `external_examples:` section if needed).
5. Open a PR. In the description, briefly note:
   - Domain (B2B SaaS, consumer, etc.)
   - Whether the persona is real, synthetic, or hybrid
   - What sources fed it (high-level — no need to dox your customers)

We'll review for fit (does it follow the template?) and quality (does it sound like a real person?). We won't gatekeep on domain — every domain teaches the framework something.

## How to contribute a methodology improvement

1. Fork.
2. Edit `research/*.md` or `validation/*.md`.
3. Open a PR with a brief "why" — ideally citing what went wrong on a real project that motivated the change.

We bias toward concrete, opinionated guidance. We push back on:
- "It depends" without saying what it depends on.
- Adding optional steps. If a step is optional we'll usually delete it instead.
- Defensive prose ("of course every team is different" — yes, and our methodology is for the teams who follow it).

## Skill changes

The skill files (`skills/persona-council/SKILL.md`, `skills/persona-research/SKILL.md`) are the API surface. Changes there affect every install.

- **Documentation tweaks:** open a PR.
- **Behavior changes:** open an issue first to discuss. We need to weigh "improvement" vs "breaking everyone's workflow" before merging.
- **New modes / flags:** strong default-no. The skill's value is its small, opinionated surface.

## Code of conduct

Standard "be decent" rules. We'll close PRs and issues that violate basic professionalism. The maintainers (Medovnicek Labs, 2 people) reserve the right to be the final arbiter on what's mergeable.

## License

By contributing, you agree your contribution is licensed under the same MIT license as the rest of the repo.
