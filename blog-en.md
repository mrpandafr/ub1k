# UB1K — From Lab to Atom

*Jean-Sébastien — K1SS Atelier 0, Besançon — July 2026*

---

## The thread

I never let go. From my studies to today, the same thread: **the structure of meaning.** How information organizes, how it transmits, how it outlives those who produce it.

My studies led me to vector spaces. Not by chance — I was drawn to the geometry of ideas, to the notion that you could *place* a concept in a space and measure its distance to others.

Roxin gave me a server one day. Not a lecture — a server. "A wolf who knows how to keep his place." The first time someone entrusted me with infrastructure. I never forgot.

Mercier taught me that communication is architecture — not polish. That human code matters as much as machine code.

My father designed springs. He made them so simple, so durable, that nobody knew he made them. But they still held.

---

## The project

2018: Gensim, word2vec — a few lines of Python and suddenly my texts had coordinates.

2024: Hermes Agent (Nous Research) — open-source framework for memory-extensible agents. The missing piece.

June 2026: K1SS Atelier 0, Besançon.

---

## The memory

**V0 (June 8):** 71,000 messages in SQLite. 1.1 GB. No index. 50k tokens of noise per turn.

**V1 (July 8):** Each message → ES document with embedding. 71k docs, 30ms, ~50% relevance.

**V2 (July 9):** Each sentence → its own atom. 311,442 atoms. Synapse filters noise (<1%). 11ms. 10/10 relevance.

**V3 (in progress):** Time as dimension. Each atom carries its consultation history.

## The numbers

| Metric | V2 |
|:-------|:--:|
| Atoms | 311,442 |
| Latency | 11ms |
| Relevance | 10/10 |
| Noise | <1% |
| License | MIT |

---

## What's next

I don't know how much time I have left. I know what we're building — K1SS, Tamashii, the atoms — is free, open, and will outlive me.

From my studies to today, I never let go. Neither will the atoms.

*Jean-Sébastien — July 2026*
