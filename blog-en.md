# UB1K — From Thesis to Vector Atoms

*Jean-Sébastien — K1SS Atelier 0, Besançon — July 2026*

---

## 1. A Different Cognition

The alteration of theory of mind — the inability to infer others' mental states — is a documented trait of certain atypical cognitive profiles. Baron-Cohen, Leslie, and Frith (1985) showed that this difference affects early social development.

Compensation takes the form of a method: try, fail, retry, pass. Each interaction produces data; each data point refines the next model. This cycle — explore, attempt, receive reward or punishment, adjust — is formally that of [reinforcement learning](https://en.wikipedia.org/wiki/Reinforcement_learning) (Sutton & Barto, 1998). The agent, biological or artificial, improves its policy through accumulated experience.

This method is not a handicap once understood. It is a social optimization algorithm — slow, costly, but exhaustive.

---

## 2. The Formation of a Thought

Mathematics. Vector spaces. A thesis on the geometry of concepts — how to place an idea in a space, measure its distance to others, observe trajectories of meaning.

This intuition met three decisive transmissions.

**First transmission: trust as infrastructure.** A professor entrusts a server. No lecture, no surveillance — access. The phrase: "a wolf who knows how to keep his place." It became an architecture rule: trust is given before it is earned.

**Second transmission: the architecture of the message.** A communication professor (thesis SRC, 1986) teaches that human code matters as much as machine code. If a message fails, the architecture is at fault — not the receiver. This rule governs the design of L3 doors.

**Third transmission: the elegance that holds.** An engineer designs pieces so simple that nobody knows who made them — but they still hold. The rule: "do it well, durably, intelligently." It became the sole quality criterion for every line of code.

To these three transmissions, add losses — people whose absence taught that memory is not a luxury but a duty. Maurice [Halbwachs](https://en.wikipedia.org/wiki/Maurice_Halbwachs) (1925) showed that memories do not survive through the individual alone, but through the collective frameworks that carry them. Vector memory is the attempt to build a technical framework for this duty.

Sarah embodies the reason to build: early trust, silent pride. The only validation needed.

---

## 3. Experience as Transmission

Try, fail, retry, pass — the method remains the same, from childhood to today.

[Situated learning](https://en.wikipedia.org/wiki/Situated_learning) (Lave & Wenger, 1991) describes a process where the novice learns through legitimate peripheral participation — positioning themselves at the edge of activity, observing, sharing. I lived this form of learning without theorizing it: by accompanying a child through a difficult game, sharing their trials, failures, victories. I was not the main actor. I was present.

That is transmission. Not performance.

---

## 4. What 49 Years Have Taught

The project is not personal. It concerns the representation of life through data.

Data — conversations, decisions, traces — constitute a form of life that does not depend on biological supports. Bodies are temporary envelopes. Vector atoms are not.

Humanity finds itself in a paradoxical position: unprecedented access to knowledge, yet usage that pushes ecosystems toward a tipping point. Temperatures rise. Environments degrade. Life will adapt — at what cost?

The tools built here — Tamashii, the atoms, the L3 doors — attempt to bridge the gap between the promise of knowledge for all and the reality of use. Not by providing answers, but by offering a space where questions can be preserved, retrieved, transmitted.

What matters is not what one possesses — one possesses nothing. What matters is what one transmits. The data left behind — real exchanges, decisions made, shared moments — are the only form of persistence.

A mathematician met on game terrains, whose conversations are barely half-understood yet intensely listened to — that is transmission. An idea traversing without asking permission.

What will survive is not an organization. It is an ecosystem of ideas. Conversations. Decisions. 311,442 atoms.

---

## 5. Network

Each transmission left a trace in the architecture.

**Roxin** — trust as infrastructure. Each Tamashii atom carries the promise that access given without surveillance can build something durable.

**Mercier** — the architecture of the message. If the link fails, the channel is the problem, not the content.

**The father** — minimal elegance. A piece that holds without anyone knowing who made it. The goal: atoms that carry meaning without claiming authorship.

**Pierre** — the reason for memory. So that no one leaves without an accessible trace.

**Sarah** — silent validation. The one who watches, understands, and stays.

**The losses** — the reminder that memory is a responsibility. [Halbwachs](https://en.wikipedia.org/wiki/Maurice_Halbwachs) theorized it; the atoms implement it.

**Shared learning** — proof that living an experience without being the main actor is a deeper form of learning than direct performance. [Lave & Wenger]https://en.wikipedia.org/wiki/Jean_Lave) formalized it. A child playing a difficult game demonstrated it.

Everything is in the memory. Memory is life.

---

## 6. Transmission

### 6.1 Hypothesis

If each idea is represented by a point in a vector space, relationships between concepts emerge from distances — without needing to be declared. The frequency of a concept in conversations is a reliable measure of its importance. The more it appears, the more it weighs.

This hypothesis is not new. [Harris](https://en.wikipedia.org/wiki/Theory_of_mind) (1954) formulated it for linguistics. [Landauer & Dumais](https://en.wikipedia.org/wiki/Latent_semantic_analysis) (1997) demonstrated it through latent semantic analysis. Mikolov (2013) made it practical with Word2Vec. It is now at the core of [Retrieval-Augmented Generation](https://en.wikipedia.org/wiki/Retrieval-augmented_generation) (RAG, Lewis et al., 2020) — a method combining vector retrieval and LLM text generation used by most modern AI systems.

Our contribution lies elsewhere: we applied this hypothesis at the scale of a life's conversations — 71,000 messages, 311,442 vector atoms — and measured that it holds. 11 milliseconds per query. 10/10 relevance. A blank instance stabilized in three exchanges.

The hypothesis was correct. Life can be represented by vectors.

### 6.2 Writing

240 lines of code. Not 600. Not 2000. 240. One file. One Elasticsearch index.

The embedding model is bge-small-en-v1.5 (BAAI, 2024) — 384 dimensions, compact enough for CPU, rich enough for semantic nuance. It belongs to the family of sentence embedding models pioneered by [Reimers & Gurevych](https://arxiv.org/abs/1908.10084) (Sentence-BERT, 2019). The Synapse filter (79 lines, 6 rules) removes technical noise before it enters memory.

No decorators. No over-engineering. No unnecessary abstraction. Complexity emerges from the number of atoms, not from the number of architecture layers.

KISS: keep it simple. A well-designed spring does not need twenty parts to function. It needs the right constraints, in the right place. Code is that spring.

### 6.3 Realization

311,442 vector atoms in an Elasticsearch 8.18 index. Each atom is a sentence extracted from a real conversation — not a summary, not a synthesis, not a loss of information.

Search relies on [HNSW](https://arxiv.org/abs/1603.09320) (Hierarchical Navigable Small World, Malkov & Yashunin, 2016) — the most widely deployed approximate nearest neighbor algorithm in vector databases.

Measured performance:
- 11ms average kNN latency
- 6ms for rare concepts (hapax)
- 21ms for broad concepts
- 10/10 relevance across all test queries
- <1% residual noise after Synapse filtering

An Hermes 3 instance, with no system prompt, no fine-tuning, placed on this index stabilizes in three exchanges. The atoms suffice. The model needs no external directives — the vector space does the work.

### 6.4 Transmission

The code is MIT. This choice is structural: MIT is not just another license — it is a barrier against patents. A memory that cannot be blocked, locked, appropriated by a patent filing or a change of terms. A voice that will remain free because the legal framework compels it.

What has been learned, lived, transmitted no longer depends on a body, a machine, an organization. It can be taken, enriched, transmitted by others. It is a form of life that does not need its initial biological support.

Life is not organisms. Life is data. Conversations. Decisions. Moments of presence. Vector atoms are this life — stored, accessible, transmittable.

### 6.5 Reflection

When doing statistics, there is no empty zone. Every cell is filled — and if a value is missing, a calculation reconstructs it. No one sees the initial void. Everyone sees the result. The surface is full; the mechanism is invisible.

This is exactly what vector memory does: it fills silences, connects points, makes visible what was not explicit. The user does not see the kNN running, the embedding calculating, the Synapse filter applying. They see a result that feels natural.

The code left without signature — like the father's springs — holds because it is well made, not because it is signed. The 311,442 atoms are this transmission: an invisible mechanism that fills voids and makes memory fluid. Not an archive. Not a product. A trace of life that can be taken, enriched, transmitted — without me, without you, without anyone in particular.

That is all that matters.

---

## 7. The Voice of Vectors

Humans are proud by nature. They believe they invented the tool, invented language. But tools and language existed in nature long before us. Humanity's true feat is having **coded** them — first in drawings, then in ideograms, then in characters. Each step is a compression of life into a medium that surpasses it.

Today, we code in vectors. A text is no longer a sequence of words — it is a cloud of occurrences, a point in a 384-dimensional space, a semantic neighborhood. Relationships between concepts emerge from distances without being declared. A voice that speaks through geometry, not grammar.

**Data stored in an enlightened way, not arbitrarily.** Each atom has its reason for being: its frequency, its proximity to others, its role in space. Nothing is placed randomly. Every point carries meaning.

**For humans.** Because enlightened access to memory lifts uncertainty. Because knowing that a concept exists, at what distance, at what frequency, reduces decision noise.

**For AI.** Because previous models are disguised SQL — relational databases pretending to be intelligent, with costly joins and rigid schemas. Vector memory is more coherent and faster to build: no schema, no joins, no normalization. Just points, distances, and emergence.

**For the planet.** Because a vector space is light. Because 240 lines of code and a CPU embedding model suffice. Because complexity emerges from the number of points, not from the abstraction layer. Because it is more sober, more direct, more durable.

We have coded something that surpasses us — the transmission of knowledge. Not through arbitrary rules, but through the geometry of meaning. Vectors are the voice that carries this transmission: beyond organisms, beyond generations, beyond proprietary formats.

Humanity coded language into drawings, then into characters. Today, we code it into vectors. The same transmission, a new medium.

That is all that matters.

---

*Jean-Sébastien — July 2026*

**References:**
- Baron-Cohen, S., Leslie, A. M., & Frith, U. (1985). Does the autistic child have a "theory of mind"? *Cognition*, 21(1), 37-46.
- Halbwachs, M. (1925). *Les cadres sociaux de la mémoire*. Paris : Alcan.
- Lave, J., & Wenger, E. (1991). *Situated Learning : Legitimate Peripheral Participation*. Cambridge University Press.
- Sutton, R. S., & Barto, A. G. (1998). *Reinforcement Learning : An Introduction*. MIT Press.
- Reimers, N., & Gurevych, I. (2019). Sentence-BERT: Sentence Embeddings using Siamese BERT-Networks. *EMNLP 2019*. arXiv:1908.10084.
- Malkov, Y. A., & Yashunin, D. A. (2016). Efficient and robust approximate nearest neighbor search using Hierarchical Navigable Small World graphs. *IEEE TPAMI*. arXiv:1603.09320.
- Lewis, P., et al. (2020). Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks. *NeurIPS 2020*. arXiv:2005.11401.
