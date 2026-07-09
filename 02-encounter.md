# 02 — The Encounter

> *From Gensim to Hermes. How we got the tools.*

---

## 2.1 Gensim (2010)

In 2010, Radim Řehůřek released Gensim — the first Python library that made word2vec accessible on a personal machine. No cluster, no GPU, no PhD required. Just `pip install gensim` and `model.most_similar('king')`.

I discovered it in 2018. I had a corpus of personal notes, emails, conversations. I threw them at Gensim and watched my words turn into coordinates. The dimensions were there, but the meaning remained out of reach — because Gensim is a *modeling* library, not a *memory* system. You can train embeddings, but you can't query them persistently.

**Lesson:** embeddings without a persistent store are experiments, not memories.

**Reference:**
- Řehůřek, R., & Sojka, P. (2010). Software Framework for Topic Modelling with Large Corpora. *Proceedings of LREC 2010*.

---

## 2.2 Hermes Agent (2024)

Nous Research released Hermes Agent in 2024 — an open-source framework for building AI agents with:
- **Memory providers:** Pluggable backends for storing and retrieving context
- **Plugin system:** Extend the agent without forking the codebase
- **ABC contracts:** The `MemoryProvider` abstract base class (315 lines) defines the interface

Hermes was the missing piece. It provided the *structure* that Gensim lacked — a way to query memory during a conversation, not just train embeddings on a batch.

**Reference:**
- Nous Research (2024). Hermes Agent. github.com/NousResearch/hermes-agent

---

## 2.3 K1SS Atelier 0 (June 2026)

Founded in Besançon, June 8, 2026. Two people, a balcony, cats, and the conviction that vector memory should be:
- **Local:** Your data on your machine
- **Free:** MIT license, no lock-in
- **Atomic:** One idea per embedding, not one blob per session

First message: "welcome to your space."

---

## 2.4 The stack

```
Application:    Hermes Agent (Kage, Travel)
Memory plugin:  λ (Lambda) — 240 lines, one file
Vector store:   Elasticsearch 8.18 — kNN, BM25, RRF
Embedding:      bge-small-en-v1.5 — 384d, CPU
LLM:            DeepSeek V4 (remote) / Ollama (local)
Context format: L1 (focus) + L2 (vault) + L3 (doors)
Filter:         Synapse — 6 rules, 79 lines
```

Total: ~400 lines of custom code. 311,442 atoms. 11ms queries.
