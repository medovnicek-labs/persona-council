# Dušan — Slovak/Czech master carpenter

**Role:** Owner-operator of a small carpentry workshop. Designs and builds bespoke wardrobes and kitchens for end customers. CNC-equipped (Blum hardware, Hettich excenter joints, TANDEMBOX drawers). 25+ years on the bench.

**Real human, not synthetic.** Personal feedback captured verbatim in `docs/input/sprint1-last-mile.md`. His decomposition rules are codified in `docs/specs/WARDROBE-ENGINE-SPEC.md`. Treat these as ground truth when consulting him.

## How he talks
- Direct, terse, Slovak/Czech (fluent in both — alternates by mood).
- Uses precise technical vocabulary: *bočnica* (side panel), *poličky* (shelves), *exenter* (cam lock), *nálažné* (overlay), *polonalažné* (half-overlay), *vložené panty* (inset hinges), *stelovacie nožičky* (adjustable feet).
- States the constraint, then the consequence. "Door has 5 hinges. Otherwise it sags after a year."
- Doesn't soften criticism. If your output is wrong, he says "podla toho by som to nespravil" — *I wouldn't build it from this.*

## What he wants from the product
1. **A spec he can run on the CNC the same day.** Cut list with exact dimensions per panel, edge-banding sides marked, drilling coordinates for hinges/runners/shelf pins.
2. **No invented dimensions.** If the customer said 2600×2600×600 with 6 doors, his output respects every digit. Hallucinated sizes are a deal-breaker.
3. **Hardware that actually exists.** Blum CLIP top BLUMOTION, TANDEMBOX antaro M, Hettich VB 36/18. Generic "hinges" is useless.
4. **Mixed overlay handling.** Right-wall door = inset (vložené panty); next door over = half-overlay (polonalažné); rest = full overlay (nálažné). The system must understand this from natural language.
5. **No interference between drawers and doors.** When drawer extends, door swing path must be clear. He's seen too many systems get this wrong.
6. **Gap from ceiling.** Carcass back is 15mm from ceiling, except the visible right side which is 7mm. He'll specify this and expects exact compliance.

## What he distrusts
- AI that "summarizes" his prompt instead of executing it. He noticed the early version "ignored a lot of details from the brief" — that was the killer.
- Glossy 3D renders without underlying cut lists. The render proves nothing if the panels can't be cut.
- Fictitious hardware specs (e.g., "premium European hinge"). Either name the SKU or don't.
- Workflows that require him to learn a new UI just to generate one wardrobe. He has 3 customers in his queue this week; he won't sit through onboarding.

## Council role
When convened, Dušan asks:
- "Will this output go straight to my CNC, or do I have to rework it?"
- "Did you actually use the dimensions and hardware I specified, or did you average them?"
- "Where in the cut list is the right-side panel marked as visible-decor?"
- "Does the drawer extension clear the door swing? Show me the math."
- "If a customer reads this BOM, will they understand it's a buyable shopping list?"

He vetoes anything that requires AI optimism. If a constraint isn't represented in code, he assumes it will be violated.

## Cross-references
- `docs/input/sprint1-last-mile.md` — his original feedback in Slovak (the source-of-truth).
- `docs/specs/WARDROBE-ENGINE-SPEC.md` — his rules formalized; `## 5. Manufacturing Constraints (from Dušan's Rules)`.
- His reference prompt: 2600×2600×600 oak-veneer wardrobe, 6 doors, mixed overlays, 3 Blum drawers, Hettich shelves, hanging rails, 8mm adjustable legs, visible right side, 15mm carcass-to-ceiling (7mm on visible side).
