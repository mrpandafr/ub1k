# UB1K — From Thesis to Vector Atoms

*Jean-Sébastien (AFoxMind) — K1SS Atelier 0, Besançon — July 2026*

---

## 1. Foundations (1998–2018)

It starts with a math thesis. Not about neural networks or modern AI — about vector spaces, geometry, distances between concepts. Back then, nobody called it "machine learning." We called it math.

Twenty years later, those same math became the memory infrastructure of Tamashii. The **distributional hypothesis** [Harris, 1954]: words that appear in similar contexts have similar meanings. This principle, born in 1950s linguistics, is today the core of all embedding models — including bge-small, which powers our memory engine.

In 1997, Landauer and Dumais published "A Solution to Plato's Problem" [LSA, 1997] — the first demonstration that a latent vector space can capture semantic structure better than symbolic representation. This is when machines began to understand — not through rules, but through distances.

**References:**
- Distributional hypothesis — Harris, Z. (1954). Distributional structure. *Word*, 10(2-3), 146-162.
- LSA — Landauer, T. K., & Dumais, S. T. (1997). A solution to Plato's problem. *Psychological Review*, 104(2), 211-240.
- Word2Vec — Mikolov, T., et al. (2013). Efficient estimation of word representations in vector space. *arXiv:1301.3781*.

---

## 2. The Encounter (2018–2026)

In 2018, I discovered **Gensim** [Řehůřek, 2010] — the first Python library that let me run word2vec on my own corpus without a 100-machine cluster. A few lines of code, a text file, and suddenly my words had coordinates.

In 2024, **Hermes Agent** [Nous Research, 2024] arrived — an open-source framework for extensible AI agent memory (providers, plugins, ABC contracts). The missing piece.

In June 2026, **K1SS Atelier 0** was founded in Besançon. Two people, a balcony, cats, and the conviction that vector memory should be local, free, and atomic.

**References:**
- Gensim — Řehůřek, R., & Sojka, P. (2010). Software Framework for Topic Modelling with Large Corpora. *Proceedings of LREC 2010*.
- Hermes Agent — Nous Research (2024). github.com/NousResearch/hermes-agent

---

## 3. V0 — Zero State (June 8, 2026)

First message: "welcome to your space." 71,000 raw conversation messages — decisions, architecture, music, sleepless nights. A single SQLite file (1.1 GB, 539 sessions). No indexing, no filtering.

| Property | Value |
|:---------|:------|
| Storage | SQLite (state.db) |
| Size | 1.1 GB |
| Sessions | 539 |
| Messages | 71,175 |
| Indexing | None |
| Search | Full-text SQL |

**The problem:** 50,000 tokens of context per turn, 90% of which was technical noise (tool outputs, file listings, search results).

---

## 4. V1 — Messages as Documents (July 8, Day 1)

Each message imported as a standalone document in Elasticsearch with bge-small embedding (384d).

```
71,175 documents | 30ms kNN | ~50% relevance
```

**The problem:** a 5,000-character message with 6 concepts — Pierre, Sarah, kill switch, weather — becomes one blurry vector. The embedding averages everything into mush.

| Metric | V1 |
|:-------|:--:|
| Latency | 30ms |
| Relevance | ~50% |
| Dedup | None |
| Avg size | 2,300 chars |

---

## 5. V2 — Semantic Atoms (July 9, Day 2)

Break each message into individual sentences. Each sentence becomes its own embedding. A 6-concept message → 6 distinct atoms.

**Synapse gate** — 6 rules filtering what enters memory:

| # | Rule | Action |
|:-:|:-----|:-------|
| 1 | Empty payload | Discard |
| 2 | System error | Discard |
| 3 | Tool fragment | Discard |
| 4 | Duplicate file | Keep 1 |
| 5 | <10 chars | Discard |
| 6 | Cosine >0.95 | Dedup |

```
311,442 atoms | 11ms avg | 10/10 relevance | <1% noise
```

**10 test queries — all correct:**

| Query | Time | Top hit |
|:------|:----:|:--------|
| Pierre Biguinet, Shanghai | 21ms | "Shanghai, May 8, 2008" |
| Kill switch, right to rest | 11ms | "foundational rule" |
| Sarah, first funder | 12ms | "first funder of Atelier" |
| Tortoise not hare | 13ms | "slowness, father's springs" |
| Tamashii, vector memory | 10ms | "Vector Memory — ES" |
| M4Z3, firmware PCB | 9ms | "firmware detects host" |
| Roxin, wolf mentor | 10ms | "wolf who keeps place" |
| Father's springs | 8ms | "do it well, durably" |
| EMAC, music | 6ms | "your first emotion" |
| Rare concept (hapax) | 7ms | exact hit |

| Metric | V2 |
|:-------|:--:|
| Latency | 11ms (min 6ms, max 21ms) |
| Relevance | 10/10 (100%) |
| Noise | <1% |
| Avg atom size | 120 chars |

---

## 6. V3 — Time as Dimension (in progress)

Each atom now carries:
- **at** — creation timestamp (ISO)
- **seen** — consultation history (timestamp array)

**New queries enabled:**

| Question | Mechanism |
|:---------|:----------|
| "What was I discussing at this time yesterday?" | `seen` filtered by `now - 24h` |
| "What's the current hot concept?" | `seen` frequency in last 5 min |
| "What did I explore this session?" | Temporal aggregate of seen atoms |
| "What's my learning rhythm?" | `seen` distribution over time |

```
Architecture (in progress):
┌─────────────────────────────────────┐
│  ES 8.18                            │
│  public-memory_atoms                 │
│  ┌───────────────────────────────┐  │
│  │ at: ISO (creation)            │  │
│  │ seen: [ISO timestamps] (views)│  │
│  │ vector: float[384] (embedding)│  │
│  │ bank_id: string (agent)       │  │
│  │ text: string (atomic content) │  │
│  └───────────────────────────────┘  │
│  311,442 atoms · ~11ms + 1ms       │
└─────────────────────────────────────┘
```

---

## 7. Implications — Statistics, Sets, Meaning

### Statistics

A concept with 900 occurrences ("atelier") is 83× more likely to be retrieved than one with 11 ("Pierre"). Frequency is an **empirical relevance metric** — the most reliable signal in the system.

Rare concepts (hapax) are fastest to retrieve (6ms). Their vector sits in a sparse region with few competitors.

### Sets

311,442 atoms in 384-dimensional space. Cosine distance is relative — "close" means "closer than average." L3 doors partition by semantic proximity to founding atoms, not by manual tagging.

### Temporal meaning

A fact is dated. "Kill switch = €140k" in June and "Kill switch = €220k" in July are two atoms. Without timestamps, the system would average them into one wrong fact. With timestamps, it tells a story.

---

## 8. Publication

MIT. Code, atoms, and text.

- github.com/mrpandafr/kokoro
- github.com/mrpandafr/domu
- github.com/mrpandafr/vectormind

*K1SS Atelier 0 — Besançon — July 2026*
