# `DATA/` — the source of truth (schema v2)

This folder **is** the graph. [`../build.mjs`](../build.mjs) compiles it into `graph.json`
(the viewer's data) **and** `analysis.json` (computed graph metrics). Edit the source here,
run the build, commit all three. Never hand-edit the outputs — they are build artifacts.

```
DATA/
  clusters/<id>.md          one file per cluster
  tags/<id>.md              one file per tag
  tactics/<id>.md           one file per tactic   ← cited write-ups live in the body
  nodes/<id>.md             one file per identity (and per exit anchor)
  edges/<from>__<to>.md     one file per relation
  meta.yml                  informational header
build.mjs                   DATA/ → graph.json + analysis.json (validates, then emits)
```

## Two parts to every file

- **YAML frontmatter** — the machine payload the graph reads (the "teaser").
- **Markdown body** — long-form documentation, analysis, and full citations. Ignored by
  the build. Write as much as you want; the graph never gets heavier.

A file's **id is its filename**. Slugs must match across files; `build.mjs` fails on any
broken reference and refuses to emit.

## The model in one screen

**Six identity `kind`s (the hexad)** — what a node *is*, so edges can be checked against it:
`movement · community · belief_state · genre · self_id · synthetic_agent`.
Plus `exit_state` for loose off-ramp anchors (not an identity).

**`volatility: static | liquid`** — and it governs where tactics attach. *Static* identities
(masses frozen in place) carry manipulation intrinsically → put tactics on the **node**.
*Liquid* identities (driven by a leader / trend) are shaped in the move → put tactics on the
**edge**. Both are allowed; volatility tells you which dominates.

**Harm is three axes, not one number:** `harm_to_self` (0–5), `harm_to_others` (0–5),
`reversibility` (1–5, how escapable). The viewer's node size uses a derived
`risk_level = harm_to_self + harm_to_others`.

**Every edge is a typed, sourced claim:**
- `type` — `progression · recruitment · gateway · rebrand · audience_overlap · ideological_kinship · amplify · exit`
- `confidence` — epistemic status, **required**: `documented` (study) → `reported`
  (journalism) → `observed` (your digital observation) → `intuited` (personal/experiential).
  Intuition is welcome — it just has to be *labelled* as such, never dressed as a study.
- `sources[]` — `{ref, kind}` attached to the claim itself (`kind`: study · journalism · observation · personal).
- `strength` (pull) `high|medium|low`; `prevalence` (base rate) `common|occasional|rare`.

Semantic rules the build enforces: `amplify` edges must start at a `synthetic_agent`;
`exit` edges must end at an `exit_state`; flow edges may not target an exit.

## File shapes

**`nodes/red_piller.md`** (identity)
```yaml
---
name: Red Piller
aka: Redpill · TRP
kind: belief_state
cluster: manosphere
volatility: static
tags: [masculinity, conspiracy]
tactics: [us_vs_them_framing, identity_fusion]   # intrinsic (static identity)
harm_to_self: 3
harm_to_others: 2
reversibility: 3
entry_point: false
terminal: false                # if true, add nothing — trap_depth is derived from reversibility
status: reviewed               # stub | draft | reviewed | contested
valid_from: 2026-06
last_confirmed: 2026-06
target:
  age: "16-30"
  gender: male_heavy
  psychology: [romantic rejection, resentment]
timeline: { entry: weeks, deepening: months, terminal: N/A }
hook: >-
  Someone finally explains why dating feels impossible.
cost: >-
  Reframes every relationship as adversarial power.
intervention:
  breaking: >-
    A relationship that contradicts the framework's predictions.
  alternative: >-
    Therapy or peer groups addressing rejection without an enemy.
  resources: [Men's mental-health services, Licensed therapists]
---
# Red Piller — long-form documentation + citations here (ignored by the build).
```

**`nodes/disillusionment.md`** (exit anchor — minimal)
```yaml
---
name: Disillusionment
kind: exit_state
cluster: exit
note: >-
  Failed predictions or hypocrisy crack the framework's certainty.
status: draft
---
```

**`edges/red_piller__mgtow.md`**
```yaml
---
from: red_piller
to: mgtow
type: progression
strength: high
prevalence: occasional
confidence: documented
tactics: [us_vs_them_framing, identity_fusion]   # transitional (the pull happens here)
valid_from: 2026-06
last_confirmed: 2026-06
sources:
  - ref: "Ging 2019, 'Alphas, Betas, and Incels'"
    kind: study
mechanism: >-
  Adversarial dating frame resolves into total withdrawal once strategy fails.
---
```

## Build

```bash
npm install          # js-yaml + gray-matter
npm run build        # DATA/ → graph.json + analysis.json
npm run check        # validate only; non-zero exit on any broken reference — use in CI
```

## `analysis.json` — what the graph computes about itself

`build.mjs` derives, over the directed *flow* edges (progression/recruitment/gateway/rebrand):
- **betweenness** — the structural hubs (which identities the most paths run through);
- **degree**, **reachability** (which entry points reach which terminals, in how many steps);
- **cluster_bridges** — edges that cross clusters (the dangerous connectors);
- **synthetic_amplifier** — what the AI node fans out to, and across which clusters;
- **volatility** split and **tactics_frequency**;
- **warnings** (real problems: orphans, unreachable terminals) and **review** (judgement
  calls: dual-entry nodes, risk that dips along a descent).

This is the layer that lets the structure *demonstrate* claims — e.g. which clusters are the
real cores — instead of asserting them.

## Growing it

Add a node by dropping `nodes/<slug>.md`; wire it with `edges/<a>__<b>.md`. Add any new
vocabulary (`tags/`, `tactics/`, `clusters/`) first so references resolve. `npm run build`,
reload.
