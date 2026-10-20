# Network Biology collection: literature selection

Supports GitHub Issue [Hongyang-Du/PaperLeet#3](https://github.com/Hongyang-Du/PaperLeet/issues/3) (*Add Network Biology section: problems, papers, and learning path*). The supplied 100-record dataset is preserved unchanged in [network_biology_literature.json](network_biology_literature.json); this note records how it was validated and which records drive the first six exercises. `papers.yaml` remains the only paper catalog: nothing here is a parallel literature registry.

## Dataset validation (2026-10-20)

Checked offline with a script against the supplied file:

- 5 categories with 20 records each, 100 records in total.
- Every record has exactly `id`, `title` and `url`; no empty fields.
- `id` values are unique integers 1-100; no duplicate titles; no duplicate URLs.
- Every `url` matches `https://doi.org/10.<registrant>/<suffix>`.

The file carries no authors, venue or year. Those were checked only for the five selected papers (below). The other 95 records are **unverified beyond their format**, and DOI resolution was not tested (no network access from the build environment), so no DOI here should be treated as resolved.

## Selected papers

| Paper (`papers.yaml` id) | Dataset record | Verified bibliographic data | Exercise (number) |
| --- | --- | --- | --- |
| Albert, *Scale-free networks in cell biology* (`scale-free-networks`, 61) | id 3, Classic Foundations & Network Topology | J Cell Sci 118(21):4947-4957, Nov 2005; author Réka Albert (arXiv q-bio/0510054 and publisher record) | `network_biology/degree_distribution` (93) |
| Barabási & Oltvai, *Network biology: understanding the cell's functional organization* (`network-biology`, 62) | id 1, Classic Foundations & Network Topology | Nat Rev Genet 5(2):101-113, Feb 2004; DOI shown on an independent record | `hubs_centrality` (94), `connected_components` (95) |
| Menche et al., *Uncovering disease-disease relationships through the incomplete interactome* (`incomplete-interactome`, 63) | id 42, Network Medicine, Disease Interactomes, & Epidemiology | Science 347(6224):1257601, 20 Feb 2015; DOI shown on PubMed | `shortest_paths` (96) |
| Milo et al., *Network motifs: simple building blocks of complex networks* (`network-motifs`, 64) | id 21, Network Motifs, Modules, & Community Detection | Science 298(5594):824-827, 25 Oct 2002; six authors | `feed_forward_loops` (97) |
| Ravasz et al., *Hierarchical organization of modularity in metabolic networks* (`hierarchical-modularity`, 65) | id 22, Network Motifs, Modules, & Community Detection | Science 297(5586):1551-1555, 30 Aug 2002; DOI listed on arXiv cond-mat/0209244 | `community_modules` (98) |

Titles, venues, volumes, pages and authors above were confirmed from publisher, institutional-repository, PubMed or arXiv records on 2026-10-20. DOI strings are the ones supplied in the dataset; for Barabási-Oltvai, Ravasz and Menche the same DOI appeared on an independent record, whereas for Albert (`10.1242/jcs.02714`) and Milo (`10.1126/science.1078368`) the DOI was **not** seen on an independent record in this session. Note that a book chapter by Almaas and Barabási has the same title as Albert's article; the dataset DOI prefix (Company of Biologists) is consistent with the Journal of Cell Science article.

## How each paper is used, and what is not claimed

The exercises are teaching adaptations on synthetic graphs. A paper is cited as the background for a concept, not as the source of the exercise's equations or data.

- **Albert (2005)**: degree and the degree distribution as graph descriptors of cellular networks. No power-law fit and no claim that any network is scale-free.
- **Barabási & Oltvai (2004)**: general network-measure background (the review has a box on network measures). Centrality and connected components are teaching adaptations; the exercises do not claim that the review defines them in this form, and centrality is never equated with essentiality.
- **Menche et al. (2015)**: the idea that network location and distance in an interactome relate disease-associated proteins. Only plain unweighted shortest paths are implemented, not the paper's module-separation statistic.
- **Milo et al. (2002)**: network motifs as patterns occurring more often than in randomized networks. The exercise detects the feed-forward loop; the supplied experiment compares counts with degree-preserving randomizations and makes no significance or function claim.
- **Ravasz et al. (2002)**: modular organization of metabolic networks. The exercise uses generic greedy modularity maximization; the paper's own procedure and its hierarchy are not implemented, and detected modules are not presented as validated pathways.

## Why these six exercises

They follow the roadmap in the issue (degree distribution, hubs and centrality, components, shortest paths, motifs, communities), each isolating one computational idea with deterministic synthetic data, no network access and no new dependencies. The other 95 records (for example network medicine at scale, single-cell and chromatin networks, graph representation learning and causal inference) need real datasets, heavier algorithms or statistics that do not fit a small, reviewable first contribution. They are kept in the dataset for later exercises and have **not** been added to `papers.yaml`.

## Learning-path order

`network-biology` lists `scale-free-networks`, `network-biology`, `incomplete-interactome`, `network-motifs`, `hierarchical-modularity`, which yields the problem order 93, 94, 95, 96, 97, 98. The catalog has no formal prerequisite field; the order of the collection and the prerequisite sentence in each README express the path. The collection is appended after the existing collections because the library has no introductory computational-biology collection to follow.

## Open items for the maintainers

- Paper `category` is `community` (a category already defined in `paperleet/paper_catalog.py`); a dedicated category would need a change to that managed file.
- `browser.backend` is set to `numpy-wasm` as in the one existing pure-NumPy package; whether the online runner executes these pure-Python packages was not verified.
