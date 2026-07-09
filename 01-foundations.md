# 01 — Foundations

> *From Harris (1954) to Mikolov (2013). How vector spaces learned meaning.*

---

## 1.1 The distributional hypothesis (1954)

Zellig Harris, in 1954, published what would become the cornerstone of semantic vector spaces: **words that appear in similar contexts have similar meanings**.

This wasn't a computational discovery — it was a **linguistic observation**. Harris noticed that the environments in which words appear (their co-occurrence patterns) encode their meaning. "King" appears in different contexts than "queen," but the distance between their contexts is smaller than between "king" and "banana."

> "Words that occur in similar contexts tend to have similar meanings." — Harris, 1954

Forty years later, this observation would become the mathematical foundation of latent semantic analysis.

**Reference:**
- Harris, Z. (1954). Distributional structure. *Word*, 10(2-3), 146-162.

---

## 1.2 Latent Semantic Analysis (1997)

In 1997, Landauer and Dumais published "A Solution to Plato's Problem" — demonstrating that a latent vector space, built from a large corpus via singular value decomposition (SVD), can capture semantic relationships without explicit supervision.

LSA didn't use neural networks. It used **linear algebra**: decompose a term-document matrix, keep the top K dimensions, and suddenly "king - man + woman ≈ queen" emerges from the math. No training. No labels. Just geometry.

> "How do people know as much as they do with as little information as they get?" — Plato's problem, answered by LSA.

**Reference:**
- Landauer, T. K., & Dumais, S. T. (1997). A solution to Plato's problem. *Psychological Review*, 104(2), 211-240.

---

## 1.3 Word2Vec (2013)

In 2013, Mikolov at Google published Word2Vec — replacing the SVD with a shallow neural network that learns embeddings by predicting words from context (CBOW) or context from words (skip-gram).

Word2Vec wasn't theoretically novel — it was the distributional hypothesis, implemented efficiently at scale. But it **popularized** the idea that words could be vectors. Suddenly every NLP project had embeddings.

**Reference:**
- Mikolov, T., et al. (2013). Efficient estimation of word representations in vector space. *arXiv:1301.3781*.

---

## 1.4 From words to sentences

Word embeddings capture lexical meaning. Sentence embeddings (like bge-small, Sentence-BERT) capture phrasal and semantic meaning. The same principle — proximity in vector space = similarity in meaning — scales from words to paragraphs.

**bge-small-en-v1.5** (the model we use):
- 384 dimensions (compact, fast)
- Cosine similarity
- Trained on a diverse corpus of text pairs
- Quantized for local CPU inference (~30ms per batch)

---

## 1.5 The key insight

**Meaning is frequency.** A word that appears 900 times matters more than one that appears 3 times. A word that co-occurs with another has a shorter vector distance. The space encodes the **lived experience of the corpus** — not someone's opinion about what matters.

This is the foundation of UB1K. Everything else is implementation.
