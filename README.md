# UB1K — Ubik. One Kilo. A thousand atoms of meaning.

> *Vector learning for AI memory. From a math thesis to 311,442 semantic atoms.*

## What is UB1K?

UB1K is a **knowledge territory** — not a single page, but a collection of documents about vector learning for AI memory. It traces the path from the distributional hypothesis (Harris, 1954) to our empirical results (July 2026): 311,442 atoms, 11ms kNN, 10/10 relevance.

## Structure

```
UB1K/
├── README.md                ← this page
├── 01-foundations.md        ← Thesis, Harris, LSA, Word2Vec
├── 02-encounter.md          ← Gensim, Hermes Agent, K1SS
├── 03-v0.md                 ← Zero state — SQLite, 71k messages
├── 04-v1.md                 ← Messages as documents — 30ms, 50%
├── 05-v2.md                 ← Semantic atoms — 311k, 11ms, 10/10
├── 06-v3.md                 ← Time as dimension — at, seen
├── 07-implications.md       ← Statistics, sets, temporal meaning
├── blog-fr.md               ← Blog post (French)
├── blog-en.md               ← Blog post (English)
├── benchmark.html           ← Performance benchmark
└── LICENSE                  ← MIT
```

## Navigation

- **01 Foundations** → The theory behind vector learning
- **02 Encounter** → How we met the tools
- **03 V0** → Where we started
- **04 V1** → First attempt
- **05 V2** → The breakthrough
- **06 V3** → Current work
- **07 Implications** → What it means

## Key numbers

| Metric | Value |
|:-------|:------|
| Source messages | 71,175 |
| Output atoms | **311,442** |
| kNN latency | **11ms** (avg) |
| Relevance | **10/10** |
| Filtering | Synapse gate (<1% noise) |
| Embedding | bge-small 384d |
| License | MIT |

## License

MIT — K1SS Atelier 0, Besançon — July 2026
