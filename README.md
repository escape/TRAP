# The Identity Trap

Indexing algorithmically promoted identities that promise self-improvement, belonging, and purpose — but deliver chronic grievance, financial exploitation, and a pipeline toward extremism.

![trap-graph.jpg](trap-graph.jpg)

## Content warning

This project describes manipulative, extremist, and violent ideologies for **educational purposes only**. The content includes:

- Descriptions of radicalization mechanisms
- References to white nationalism, antisemitism, and misogyny
- Discussion of suicide, self-harm, and violence

Reading about these identities does not mean endorsing them. If you recognize yourself in any profile, that's the point — and the intervention section is there for a reason.

If you or someone you know is in crisis:

(Emergency contacts following here)

## Early preview

**v0.1 — first public release**

This is the first public draft of the project — a preliminary release for feedback, review, and source citation work. Expect active updates as the data and methodology are refined.

## Why

Algorithms don't just serve content — they construct identities. A teenager searching for gym advice gets served masculinity content. A lonely young man looking for community finds a world that explains his isolation as someone else's fault. A woman seeking simpler living gets channeled toward ethno-nationalism.

These aren't accidents. They're patterns. The same structural mechanism repeats across seemingly unrelated communities:

1. **Hook** — an emotional appeal that feels like insight
2. **Cost** — hidden damage that the identity obscures
3. **Pipeline** — a directed path toward deeper, more extreme identities

This project makes those patterns visible. It's a directed graph: nodes are identities, edges are the escalation pathways between them. 

Once you see the structure, you can recognize the trap — in yourself, in people you care about, or in the platforms that profit from it.

## Current status

This project is in an initial detection phase. The current graph is sufficiently developed to test pattern discovery and visibility, while the set of identities, clusters, and pipeline mappings is still expanding to capture the identities that are actively shaping online pathways.

| Metric | Count | Status |
|--------|-------|--------|
| [Identities (nodes)](DATA/nodes/) | 57 | Initial coverage — expanding |
| [Clusters](DATA/clusters/) | 9 | Provisional |
| [Pipeline connections (edges)](DATA/edges/) | 125 | Initial mapping — review ongoing |
| Terminal nodes | 6 | In place |
| [Deception tactics (vocabulary)](DATA/tactics/) | 14 | Stable |

**What's established:**

- A working graph structure with 52 identity nodes, each capturing hook, cost, tactics, timelines, and intervention
- 125 directed edges representing escalation pathways with strength and mechanism
- Schema covering nodes, edges, clusters, tag vocabulary, and tactics vocabulary
- `trap_depth` scale on terminal nodes

**What is still evolving:**

- Identity and cluster coverage as new relevant profiles are discovered
- Per-node source citations (`evidence_sources`)
- JSON export for visualization and content ops integration
- `methodology.md` and `sources.md`

See [CHANGELOG.md](CHANGELOG.md) for version history.

## Who this is for

### Specialists

- **Researchers** — studying algorithmic radicalization, identity fusion, or digital extremism
- **Developers** — building tools, visualizations, or interventions based on this data

### General Public

- Visit https://trap.thehumanspace.org for the upcoming visualizations and wiki for this project.

- **Parents** — understanding what their kids are encountering online
- **Educators** — teaching media literacy, critical thinking, or digital citizenship
- **Individuals** — recognizing patterns in their own media consumption or that of friends/family

## Repository structure

```text
the-identity-trap/
├── README.md
├── CHANGELOG.md
├── SCHEMA.md
├── LICENSE.md
├── DATA/
│   ├── clusters/          ← 7 cluster definitions (one per file)
│   ├── nodes/             ← 52 identity profiles (one per file)
│   ├── edges/             ← 125 pipeline connections (one per file)
│   └── tactics/           ← 14 deception technique definitions (one per file)
├── DOCS/
│   ├── methodology.md
│   └── sources.md
├── scripts/
│   └── split_data.py      ← utility: split monolithic data into per-entity files
└── CONTRIBUTING.md
```

Each entity is a self-contained markdown file named by its slug (e.g., `DATA/nodes/red_piller.md`, `DATA/edges/red_piller__mgtow.md`).

## How to read the data

Each **node** (identity) contains:

| Field | Purpose |
|-------|---------|
| Hook | The emotional appeal — what draws people in |
| Cost | The hidden damage — what it actually does |
| Tactics | Deception techniques used to recruit and retain |
| Pipeline to | Where it leads next (authoritative data in edges) |
| Risk level | 1–10 severity scale |
| Entry / Terminal | Whether this is a common starting point or a hard-to-escape destination |
| Trap depth | 1–5 escape difficulty for terminal nodes |
| Target demographics | Who is most vulnerable |
| Timeline | How fast the pipeline moves |
| Intervention | Breaking points, alternatives, resources |

Each **edge** (pipeline connection) contains:

| Field | Purpose |
|-------|---------|
| From → To | Source and target identity |
| Strength | How reliably the transition occurs (high/medium/low) |
| Mechanism | What drives the movement between identities |

Each **tactic** (deception technique) contains a name and description of the manipulation mechanism, used across multiple identities.

See [SCHEMA.md](SCHEMA.md) for full field definitions.

## Contributing

This project benefits from domain expertise, lived experience, and careful review. See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on:

- Proposing new identities or clusters
- Correcting inaccuracies
- Adding sources or interventions
- Reporting harmful misrepresentations

All contributions are reviewed for accuracy and responsibility.
