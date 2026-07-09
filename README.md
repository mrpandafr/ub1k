# UB1K — Ubik. One Kilo. A thousand atoms of meaning.

> *Vector learning for AI memory. From a math thesis to 311,442 semantic atoms.*
> *K1SS Atelier 0 — Besançon — July 2026*

---

## Index

| # | Section | What it covers | Pages |
|:-:|:--------|:---------------|:------|
| 01 | [Foundations](01-foundations.md) | Distributional hypothesis, LSA, Word2Vec, Harris → Mikolov | ~3 |
| 02 | [Encounter](02-encounter.md) | Gensim, Hermes Agent, K1SS founding, the stack | ~2 |
| 03 | [V0 — Zero State](03-v0.md) | SQLite, 71k messages, 1.1GB, no index | ~2 |
| 04 | [V1 — Messages](04-v1.md) | First ES import, 30ms, 50% relevance, dilution problem | ~2 |
| 05 | [V2 — Atoms](05-v2.md) | Sentence splitting, Synapse gate, 311k atoms, 11ms, 10/10 | ~4 |
| 06 | [V3 — Time](06-v3.md) | Timestamp arrays, `at`/`seen`, granularity second/minute/hour | ~3 |
| 07 | [Implications](07-implications.md) | Statistics, sets, temporal meaning, the delta | ~3 |
| 08 | [Blog (FR)](blog-fr.md) | Full French narrative from thesis to V3 | ~1 |
| 09 | [Blog (EN)](blog-en.md) | Full English narrative | ~1 |
| 10 | [Benchmark](benchmark.html) | 10 queries, measured latencies, hit analysis | ~1 |
| — | [Synthesis](UB1K.html) | One-page visual overview | ~1 |

**Total: ~20 pages across the territory.**

---

## Quick start

```
01-foundations  →  why vectors work for meaning
02-encounter    →  how we got the tools
03-v0           →  where we started (SQLite hell)
04-v1           →  first attempt (dilution)
05-v2           →  breakthrough (atoms)
06-v3           →  current work (time)
07-implications →  what it all means
```

## Key numbers

| Metric | V0 | V1 | V2 | V3 (est.) |
|:-------|:--:|:--:|:--:|:---------:|
| Documents | 71k (SQLite) | 71k (ES) | **311k** | 311k+ |
| Latency | N/A | 30ms | **11ms** | ~12ms |
| Relevance | N/A | ~50% | **10/10** | 10/10 |
| Noise | ~90% | ~50% | **<1%** | <1% |
| Temporal | No | No | No | **Yes** |

## License

MIT — K1SS Atelier 0, Besançon, July 2026.

[github.com/mrpandafr/ub1k](https://github.com/mrpandafr/ub1k)
