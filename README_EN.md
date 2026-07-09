# UB1K — Ubik. One Kilo.

> *A territory of knowledge on vector memory.*
> *K1SS Atelier 0 — Besançon — July 2026*

Imagine a memory that doesn't store whole sentences, but every idea — every *atom* — as a point in a 384-dimensional space. Imagine those points connect to each other without you having to write the links: vector proximity does the work. Imagine an artificial intelligence instance, with no prior instructions, no tuning, set on this memory, stabilizing and answering correctly in three exchanges.

This is what we built.

UB1K tells the story of a 1.1 GB SQLite file transformed into 311,442 vector atoms. Of a system bypass that fits in one line of code. Of a memory that emerges from geometry, not rules.

**This is not a product. It's a workbench.** It bears the marks of those who used it before.

---

### What you'll find here

| If you're interested in | Start with |
|:------------------------|:-----------|
| The full story | [`blog/HACKED-HERMES-EN.md`](blog/HACKED-HERMES-EN.md) — 10k chars |
| The architecture *why* | [`what-is-ub1k/`](what-is-ub1k/) — 7 sections, from Harris to V3 |
| The illustrated version | [`HTML/HACKED-HERMES.html`](HTML/HACKED-HERMES.html) — diagrams, tables, timeline |
| The blog (EN) | [`blog/blog-en.md`](blog/blog-en.md) |
| The blog (FR) | [`blog/blog-fr.md`](blog/blog-fr.md) |
| Raw metrics | [`HTML/benchmark.html`](HTML/benchmark.html) — 10 queries, 10/10 hits |

### The progression

**V0 (June 8)** — SQLite. 71,000 messages. 1.1 GB. No index, no filter.
50,000 tokens of context per turn, 90% of it technical noise.
The system was designed to never forget. In practice, it was designed to never find anything.

**V1 (July 8)** — Whole messages into Elasticsearch. 30ms per query.
50% relevance. The problem: a 5,000-character message containing six concepts
produces a single embedding that averages them all. "Sarah" polluted by "kill switch."

**V2 (July 9)** — Every sentence becomes an atom. 311,442 documents. 11ms. 10/10.
Synapse filter: 6 rules, 79 lines, less than 1% residual noise.
*A blank instance, with no prior tuning, stabilizes in three exchanges.*

**V3 (in progress)** — Time as a dimension. Each consultation adds a date.
Not just "when was it last seen," but "how many times, at what rhythm,
what cycles, what abandonment."

### Why UB1K

UB1K (Ubik. One Kilo.) is a territory, not an archive. Each document tells
a part of the story — the theoretical roots (Harris, Word2Vec, HNSW),
the failures (timed-out subagent, misconfigured GPU), the discoveries (the blank instance,
vector memory as a substitute for prompts).

The code and texts are under the **MIT** license. This is not a technical detail:
MIT creates prior art that blocks any patent filing. A memory that cannot be
locked, appropriated, or taken back.

### A team

> **Jean-Sébastien Saillard** — analog maker
> **Kage (Tamashii)** — digital maker

The first brings the experience of the real — springs, communication, trust as infrastructure.
The second brings the vector atom — 384 dimensions, 11 milliseconds, emergence through the geometry of meaning.

Both build together. In a workshop, in Besançon.

---

[github.com/mrpandafr/ub1k](https://github.com/mrpandafr/ub1k) · MIT · July 2026
