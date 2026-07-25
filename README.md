# Mapping Influence: Social Network Analysis of GitHub Developers

Who are the most influential developers in a large open-source community, and what makes them influential? This project analyzes a 37,700-node network of GitHub developers to answer that question — not through follower counts, but through structural position: who connects to whom, and who those connections are.

## Executive summary

Using multiple centrality measures on a public GitHub developer network, influence turns out to be **highly concentrated and structurally amplified**: a small group of developers consistently ranks at the top across Degree, Eigenvector Centrality, and PageRank. They aren't isolated stars — they sit inside large, mixed communities alongside both ML and non-ML developers, which extends their reach well beyond any single technical niche. That combination — high connectivity *and* proximity to other well-connected people — is what marketing and developer-relations teams should target when identifying opinion leaders for outreach, tool adoption, or word-of-mouth diffusion.

## Business context

Developer platforms like GitHub are where tools, frameworks, and practices actually spread. For any company trying to reach developers — through open-source marketing, developer relations, or community-led growth — knowing *who* shapes that spread matters more than knowing how many people are in the room. This analysis identifies which developers occupy the structurally advantageous positions that make them effective multipliers, and shows that targeting a small, well-chosen set of them can outperform broad, untargeted outreach.

## Methodology

- **Dataset:** [GitHub Social Network (MUSAE)](https://snap.stanford.edu/data/github-social.html) — 37,700 nodes, 289,003 undirected edges, collected via the public GitHub API. Each node is labeled `Dev` or `MLdev` based on job title.
- **Tool:** Gephi, using the Data Laboratory for metric computation and Modularity for community detection.
- **Metrics:**
  - **Degree** — direct connections (visibility, immediate reach)
  - **Eigenvector Centrality** — connections to other well-connected nodes (integration within influential regions)
  - **PageRank** — recursive, eigenvector-based importance
  - **Betweenness Centrality** — how often a node bridges shortest paths between others
  - **Modularity** — community structure, to test whether influential MLdev sit in isolated ML clusters or integrated, mixed communities

Multiple metrics were used deliberately: influence is not a single number, and cross-validating across four measures avoids over-indexing on any one definition of "influential."

## Key findings

**Network is a small world.** Average path length of 3.26 and diameter of 11 across 37,700 nodes — any two developers are, on average, only a few connections apart.

| Metric | Value |
|---|---|
| Nodes | 37,700 |
| Edges | 289,003 |
| Average Path Length | 3.26 |
| Diameter | 11 |
| Topology | Small-world |

**A small group dominates influence across every metric.** These five consistently rank at the top by Degree, Eigenvector Centrality, and PageRank:

| Rank | Name | Degree | Eigenvector Centrality | PageRank | Betweenness Centrality |
|---|---|---|---|---|---|
| 1 | antirez | 967 | 0.0972 | 0.00309 | 0.00745 |
| 2 | rasbt | 729 | 1.0000 | 0.00991 | 0.00784 |
| 3 | bradfitz | 617 | 0.0667 | 0.00218 | 0.00345 |
| 4 | amueller | 478 | 0.6785 | 0.00622 | 0.00365 |
| 5 | sebastianruder | 398 | 0.5628 | 0.00519 | 0.00333 |

High Degree alone would only mean "well-connected." What matters more here is that Eigenvector Centrality and PageRank are *also* high — these developers aren't just connected, their connections are themselves influential. That's a compounding effect, not a simple popularity count.

**Influence isn't exclusive to ML-labeled developers.** Looking at the top 10 by PageRank split by label, developers such as `addyosmani` (a well-known name in JS/web performance) rank comparably to the top MLdev — a reminder that "who you know" as a driver of influence doesn't respect category labels:

| Rank | Top Dev | Top MLdev |
|---|---|---|
| 1 | singhsugga | antirez |
| 2 | nfultz | rasbt |
| 3 | addyosmani | bradfitz |
| 4 | Bunlong | amueller |
| 5 | rfthusn | sebastianruder |
| 6 | gabrielpconceicao | adeshpande3 |
| 7 | nelsonic | rhiever |
| 8 | dalinhuang99 | nd1511 |
| 9 | getify | hunkim |
| 10 | ronenhamias | onstash |

**Influential developers are embedded in large, mixed communities — not ML-only bubbles.** Community detection assigns the top 5 to just two communities, both mixed:

| Name | Community ID | Community Size | Composition |
|---|---|---|---|
| antirez | C389 | 8,095 | Mixed |
| rasbt | C311 | 6,570 | Mixed |
| bradfitz | C389 | 8,095 | Mixed |
| amueller | C311 | 6,570 | Mixed |
| sebastianruder | C311 | 6,570 | Mixed |

This matters strategically: because these developers sit inside large, heterogeneous communities rather than niche ML clusters, their reach — and any message that spreads through them — extends across the broader developer ecosystem, not just to other ML practitioners.

**Bridging matters, but isn't universal.** Not every top-ranked developer scores highest on Betweenness Centrality, but several show non-negligible values — meaning some of them also act as bridges between otherwise weakly-connected parts of the network, not just as hubs within a dense local cluster.

## Implications

- **Outreach efficiency.** A small, well-identified set of central developers can be a more effective target for tool adoption, technical advocacy, or community-led growth than broad, untargeted campaigns.
- **Cross-domain reach.** Because top MLdev are embedded in mixed communities, endorsement or adoption by them can propagate beyond the ML niche into the wider developer ecosystem — a relevant consideration for any product trying to reach developers broadly, not just an ML audience.
- **Influence is relational, not just volumetric.** Eigenvector Centrality and PageRank show that *who* you're connected to matters as much as *how many* connections you have — a useful reframe for any influencer-identification strategy that currently relies on follower counts alone.

## Limitations

- Centrality captures **structural position**, not content quality or the actual substance of a developer's contributions — a high-degree node isn't necessarily a technically better developer, just a better-connected one.
- The `Dev` / `MLdev` label is derived from job title, which is a coarse proxy and can misclassify developers who work across both spaces.
- The network is a static snapshot (collected June 2019) — influence and connections shift over time, and this analysis doesn't model that dynamics.
- No behavioral or content-based data (contribution quality, commit activity, engagement) is incorporated — only structural/graph-based signals.

## Tech stack

`Gephi` · `Python` (data processing) · Centrality algorithms: Degree, Eigenvector, PageRank, Betweenness · Modularity-based community detection

## Repository structure

```
├── README.md              this file
├── data/                  CSV exports + data dictionary (see data/README.md)
└── figures/                visualizations
```
