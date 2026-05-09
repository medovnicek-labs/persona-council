# Install + project setup

## Install the skill globally

```bash
git clone --depth 1 https://github.com/medovnicek-labs/persona-council.git ~/.claude/skills/persona-council \
  && cd ~/.claude/skills/persona-council && ./setup
```

That installs both `/persona-council` and `/persona-research` into Claude Code. They're available in every session, every project. The `setup` script symlinks each skill into the per-skill directories Claude Code expects (`~/.claude/skills/<skill-name>/SKILL.md`); it's idempotent.

Update by running:

```bash
cd ~/.claude/skills/persona-council && git pull && ./setup
```

(The second `setup` re-runs the symlinks in case new skills were added in the update.)

To add the global skills section to your `~/.claude/CLAUDE.md` (so Claude knows to prefer the universal skill over any project-local copies):

```markdown
## persona-council

`~/.claude/skills/persona-council/` is installed. Use `/persona-council` for
multi-persona critique councils and `/persona-research` for synthesizing raw
user research into persona files. Personas auto-discover from
`<cwd>/docs/personas/council/*.md`.
```

## Set up a project to use the council

In your project repo, create the persona discovery path:

```bash
mkdir -p docs/personas/council
```

Drop one or more persona files there. Use `research/persona-template.md` (in this repo) as the structure. See `examples/ponkoid/` for two complete examples.

Optionally add a `_council.yaml` to configure default council composition + routing:

```yaml
# docs/personas/council/_council.yaml
product: my-product
description: Brief description of who's in the council.

default_personas:
  - persona-slug-1
  - persona-slug-2

routing:
  prd: [persona-slug-1, persona-slug-2]
  prompt: [persona-slug-1]
  ui-mockup: [persona-slug-2]
```

That's all. From your next Claude Code session in that repo, `/persona-council` will load those personas.

## Verify the install works

In any project with personas:

```
You:    /persona-council  Review this PRD section: "Add a 'Quote' button to the
        viewer toolbar that emails the cut list to the user's saved email."
Claude: [Loads docs/personas/council/*.md]
        [Convenes default personas]
        ... runs the council ...
```

If the skill responds, install is good. If not:

1. Check `~/.claude/skills/persona-council/skills/persona-council/SKILL.md` exists.
2. Restart Claude Code (sometimes needed to pick up new global skills).
3. Open an issue at github.com/medovnicek-labs/persona-council/issues.

## Discovery paths the skill checks (in order)

1. `<cwd>/docs/personas/council/*.md`
2. `<cwd>/personas/council/*.md`
3. `<cwd>/.persona-council/*.md`
4. `<this-repo>/examples/<product>/*.md` (fallback for first-time users; emits a warning)

The first path with `*.md` files wins. The skill won't merge across paths unless you explicitly use `cross_portfolio_path` in `_council.yaml` for cross-portfolio overlay.

## Where to put personas in different repo layouts

| Layout | Where personas go |
|--------|-------------------|
| Repo with `docs/` (recommended) | `docs/personas/council/` |
| Monorepo, multiple products | Each product subdir's `docs/personas/council/` (or root `personas/council/` for shared) |
| Personas-as-private-content (don't ship to public) | `.persona-council/` (gitignored) |
| Per-environment personas (rare) | Multiple `_council.yaml` configs gated by env var |

If your layout is unusual, the skill discovers from the current working directory — so symlinks work fine as a last resort.
