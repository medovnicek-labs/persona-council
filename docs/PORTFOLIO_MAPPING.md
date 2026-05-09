# Portfolio mapping

How to share personas across multiple products without losing per-product voice.

A studio that ships several products will accumulate personas over time. Some are product-specific (Dušan only matters for Ponkoid), but others span the portfolio (the founder persona, the investor persona, the recruiting persona). This doc covers how to organise both.

## Two layers

### Product-local personas

Live in the product repo at `<repo>/docs/personas/council/*.md`. The council skill picks them up automatically when invoked from inside that repo.

Examples:
- `ponkoid/docs/personas/council/dusan-carpenter.md` — Ponkoid-specific carpenter.
- `ponkoid/docs/personas/council/eva-consumer.md` — Ponkoid-specific consumer.
- `crm/docs/personas/council/marek-sales-lead.md` — CRM-specific (when CRM is built).

Product-local personas are the default. Most personas should live here.

### Cross-portfolio personas

Live in a central location that the skill loads as an overlay. Configured via `_council.yaml`:

```yaml
# product-repo/docs/personas/council/_council.yaml
cross_portfolio_path: ~/my-git/persona-council/examples/_shared
```

When the council loads, it merges the product-local personas with the personas at `cross_portfolio_path`. Product-local files override central ones with the same slug — so a product can override a central persona's emphasis without rewriting the whole file.

Use cross-portfolio personas for:
- **The founder.** "Would Pavol or Dominik approve this?"
- **The studio's investor / advisor pool.** "Would our seed investor see this as on-strategy?"
- **The default reseller / partner persona.** Common across multiple products if the studio has a unified GTM motion.

Don't use them for:
- Per-product user personas. Those should be product-local even if the segments look similar — keeping them separate prevents accidental cross-contamination.

## The Medovnicek mapping

`mapping.yaml` at the root of this repo declares Medovnicek's actual portfolio:

```yaml
products:
  ponkoid:
    repo: github.com/medovnicek-labs/ponkoid
    persona_path: docs/personas/council/
    domain: consumer + B2B furniture design
    primary_personas: [dusan-carpenter, eva-consumer]

  crm:
    repo: github.com/medovnicek-labs/crm
    persona_path: docs/personas/council/
    domain: studio-internal CRM (gbrain pattern)
    primary_personas: [pavol-founder, dominik-tech-lead]
    status: scaffold-pending
```

Anyone outside Medovnicek can fork this repo and write their own `mapping.yaml` for their own portfolio. The skill itself doesn't read this file — it's documentation for human navigation.

## Routing rules

A `_council.yaml` in any product's persona directory can route artifacts to specific personas. Example:

```yaml
default_personas: [dusan-carpenter, eva-consumer]
routing:
  prd: [dusan-carpenter, eva-consumer]
  prompt: [dusan-carpenter]               # Eva won't see raw prompt engineering
  ui-mockup: [eva-consumer]               # Dušan only cares about cut lists
  cut-list: [dusan-carpenter]
  marketing-copy: [eva-consumer]
  pricing: [dusan-carpenter, eva-consumer, pavol-founder]   # everyone has a stake
```

The skill chooses a routing key from your invocation phrasing — "review this PRD" → `prd`, "review this prompt" → `prompt`. If no key matches, the default council convenes.

Routing is the cheap version of attention budgets — Eva costs the same tokens as Dušan, but if she's irrelevant to the artifact, leaving her out keeps the synthesis tight.

## When a persona graduates from product-local to cross-portfolio

You'll know it's time when:
- Two or more products are using a persona with substantially the same content.
- The persona's voice would be the same regardless of which product they're reviewing.

Move via:
1. Copy the file from the product repo to the central `examples/_shared/` (or wherever `cross_portfolio_path` points).
2. Edit any product-specific references out of the central version.
3. Each product repo can keep a thin local override if needed (same slug; the overlay merges them).
4. Update `mapping.yaml` to note that the persona is now cross-portfolio.

## When NOT to share

Resist the urge to share personas to "save research effort." If two products' carpenter personas have meaningfully different vocabularies, contexts, or vetoes, they should stay separate. The cost of duplicating a persona file is small; the cost of merging two distinct voices into one weak average is high.
