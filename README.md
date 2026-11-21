# TOPTEXT — Topological Text Analysis via Embedded Flow Graphs

**TOPTEXT** is a model and software for topological text analysis. A text is represented from the outset as a **two-dimensional object**: sentences form the horizontal structure, lexical recurrences and semantic fields form the vertical structure. The resulting *flow graph* embeds into an oriented surface, and its topology is used to detect the themes of a text — transparently, without training data and without any choice of window size or other tuning parameter.

**Authors**

- **Clemens Berger** — Laboratoire J.A. Dieudonné, Université Côte d'Azur, Nice · ORCID: [0000-0000-0000-0000](https://orcid.org/0000-0000-0000-0000)
- **Timon Georg Boehm** — Stuttgart Research Centre for Text Studies · ORCID: [0000-0000-0000-0000](https://orcid.org/0000-0000-0000-0000)

**Preprint:** C. Berger, T. G. Boehm, *TOPTEXT. Topological Text Analysis via Embedded Flow Graphs* (2026). DOI: [10.5281/zenodo.XXXXXXX](https://doi.org/10.5281/zenodo.XXXXXXX)

**Software record:** DOI: [10.5281/zenodo.YYYYYYY](https://doi.org/10.5281/zenodo.YYYYYYY)

---

## Motivation

Most methods of topic modeling rest on the distributional hypothesis: a word's meaning is determined by its frequency distribution within a context window. This works well for everyday language, but literary, philosophical and scientific texts derive much of their meaning from their form — from intratextual references, consistent terminology, recurrence and rhetorical structure. In addition, many current methods take decisions inside a black box, so their results are hard to interpret and only partly reproducible.

TOPTEXT tries to stay independent of statistical hypotheses for as long as possible. Instead of representing words as vectors, it determines the context of a word entirely through the horizontal and vertical structure of the graph around it. Meaning is not tied to local proximity. It arises from a word's participation in a global recurrence structure of the text.

## The model in brief

| Structure | What it is | Interpretation |
|---|---|---|
| **Sentence cycles** | Each sentence (or verse) is a closed edge path through its words. | Syntax: horizontal structure |
| **Relational cycles** | Cycles linking repetitions of the same word, or words of the same semantic field, across sentences. | Semantics: vertical structure |
| **Flow graph** | The union of all sentence and relational cycles. The edges at each node are cyclically ordered, which makes it a *ribbon graph*. | The text as a two-dimensional network |
| **Boundary cycles** | Closed paths alternating between sentence and relational edges. Each one bounds a cell of the embedding surface, and every term of the text lies on a boundary cycle. | Thematic units (hypothesis 1) |
| **Homology cycles** | The 2*g* cycles generating the first homology group of the embedding surface of genus *g*. | Rhematic units (hypothesis 2) |

The boundary cycles replace the context windows of distributional semantics. They are a classical mathematical notion and depend on no choice of parameter. Themes are obtained by grouping boundary cycles in the weighted **dual graph**, where edge weights measure how many flow-graph edges two boundary cycles share. Each theme is then described by keywords, by *T-centrality* and *C-centrality* of words, and by the sentences that express it most clearly.

Semantic fields can be specified by hand or generated automatically from word embeddings. Hand-specified fields keep the analysis fully controllable. Automatically generated fields can be inspected and corrected.

## What the software computes

For a given text, the Python implementation computes:

- the flow graph, its dual graph, the boundary cycles and the homology cycles
- the genus of the embedding surface
- correlation matrices of the word distribution with respect to the boundary cycles
- themes, with keywords, T- and C-central words, and representative sentences
- plots of all cycles

Preprocessing reduces terms to their lemmas and removes punctuation, articles, prepositions, pronouns and auxiliary verbs. Temporal, correlative and causal conjunctions are kept. Semantic fields are generated with fastText embeddings and DBSCAN clustering, which yields the smallest fields that make the flow graph connected.

Dependencies: `networkx`, `matplotlib`, `sympy`, `gensim`, `scikit-learn`.

## Example

Applied to a passage from Richard Feynman's *QED* (1985), TOPTEXT divides the text into eight themes, among them *light*, *white light*, *red / blue*, *quantum electrodynamics* and *particle*. These match the way human readers would summarise the passage. The result comes from the text alone, without semantic fields or external world knowledge. A second example, a passage from Shakespeare's *King Lear* analysed with a few hand-specified semantic fields, is discussed in the preprint.

## Fields of application

TOPTEXT is designed for texts in which form matters for meaning:

- literary texts, especially poetry
- philosophical texts
- scientific texts

## Access to the code

The source code is kept in a **private repository** and is currently not public. Researchers interested in using or evaluating TOPTEXT are welcome to contact the authors. Versioned snapshots of the code are archived on Zenodo with restricted access (see the software DOI above). Access can be requested there.

## History

A first prototype of the model was presented in:

> T. Boehm (2023). Zur Erschliessung semantischer Strukturen mit algebraisch-topologischen Konzepten. Vorstellung eines neuen Textmodells anhand von *Also sprach Zarathustra* IV. *Nietzscheforschung* 30(1), 289–299.

## How to cite

If you refer to TOPTEXT, please cite the preprint:

```bibtex
@misc{berger_boehm_toptext_2026,
  author    = {Berger, Clemens and Boehm, Timon Georg},
  title     = {{TOPTEXT}. Topological Text Analysis via Embedded Flow Graphs},
  year      = {2026},
  publisher = {Zenodo},
  doi       = {10.5281/zenodo.XXXXXXX},
  url       = {https://doi.org/10.5281/zenodo.XXXXXXX}
}
```

## Copyright

© 2026 Clemens Berger and Timon Georg Boehm. All rights reserved.

The TOPTEXT model, its documentation and its source code are the work of the authors. No licence to use, copy, modify or distribute the source code is granted unless the authors agree in writing.

## Contact

- Clemens Berger — clemens.berger@univ-cotedazur.fr
- Timon Georg Boehm — philosophie@timonboehm.ch
