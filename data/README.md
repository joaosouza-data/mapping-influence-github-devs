# Data

## Source

GitHub Social Network dataset (MUSAE), Rozemberczki, Allen & Sarkar (2019), distributed via the [Stanford Large Network Dataset Collection (SNAP)](https://snap.stanford.edu/data/github-social.html). Nodes are GitHub developers who starred at least 10 repositories; edges represent mutual follower relationships collected from the public GitHub API. Each node carries a binary label (`Dev` / `MLdev`) derived from job title.

Developer usernames referenced in this analysis (e.g. `antirez`, `rasbt`, `bradfitz`) are public GitHub identities — a username is the public identifier of a GitHub profile, and the follow relationships that form the network edges are public by construction (collected via GitHub's public API). No private or personally identifying information is included beyond what is already public on each developer's profile.

## Files

| File | Description |
|---|---|
| `top_ml_developers.csv` | Top 5 ML developers ranked by degree, with all four centrality measures and their community assignment |
| `top10_by_pagerank.csv` | Top 10 developers by PageRank, split into the `Dev` and `MLdev` label groups |
| `network_metrics.csv` | Global network efficiency metrics (size, path length, diameter, topology) |

## Data dictionary

| Column | Description |
|---|---|
| `rank` | Position within the ranked list |
| `username` | Public GitHub handle |
| `degree` | Number of direct mutual-follow connections |
| `eigenvector_centrality` | Influence weighted by the influence of one's connections |
| `pagerank` | Recursive importance score (eigenvector-based variant) |
| `betweenness_centrality` | Frequency with which a node lies on shortest paths between others (bridging/brokerage role) |
| `community_id` | Modularity class assigned by Gephi's community detection |
| `community_size` | Number of nodes in that community |
| `community_composition` | Whether the community mixes `Dev` and `MLdev` labels, or is homogeneous |

## Reproducibility note

All metrics were computed in Gephi (Degree, Eigenvector Centrality, PageRank, Betweenness Centrality, Modularity) on the full 37,700-node network. The full Gephi project file (`.gephi`, ~15MB) is not included in this repository to keep it lightweight — the CSVs above cover everything needed to reproduce the tables and figures in the main README. The project file is available on request.
