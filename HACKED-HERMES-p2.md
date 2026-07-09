## Passe 2 — Le corpus hérité : les racines théoriques

Tout ce qu'on a construit repose sur des épaules qu'on n'a pas toujours vues. Voici les racines.

---

### Le précurseur — Harris (1954)

Zellig Harris publie en 1954 « Distributional Structure » — la première formulation de l'hypothèse distributionnelle : les mots qui apparaissent dans des contextes similaires ont des significations similaires. Ce n'est pas un résultat computationnel — c'est une observation linguistique.

Harris a passé sa carrière à montrer que la structure du langage peut être décrite sans faire appel au sens, uniquement par les régularités de distribution. Le sens émerge des cooccurrences. Pas besoin de définir ce que « roi » signifie : il suffit d'observer où il apparaît.

L'hypothèse distributionnelle est devenue, 70 ans plus tard, le fondement de tous les modèles d'embedding.

---

### La démonstration — LSA (1997)

En 1997, Landauer et Dumais publient « A Solution to Plato's Problem » dans *Psychological Review*. L'article démontre qu'un espace vectoriel latent construit par décomposition en valeurs singulières (SVD) peut capturer des relations sémantiques aussi bien qu'un humain au test TOEFL.

Le titre fait référence au problème de Platon : comment les humains savent-ils autant avec si peu d'information ? La réponse de Landauer et Dumais : l'information est déjà là, dans les régularités statistiques du langage. Il suffit de les extraire.

LSA est linéaire, ne utilise pas de réseaux de neurones, et n'a pas besoin de données étiquetées. C'est de la simple algèbre linéaire appliquée à une matrice termes-documents.

---

### La démocratisation — Word2Vec (2013)

Mikolov chez Google publie Word2Vec en 2013. L'innovation n'est pas théorique — c'est la même hypothèse distributionnelle — mais technique : un réseau neuronal peu profond (1 couche cachée) qui apprend des embeddings en prédisant le mot suivant (CBOW) ou le contexte d'un mot (skip-gram).

Word2Vec ne bat pas LSA sur la qualité des embeddings. Il bat LSA sur la passassion à l'échelle : on peut l'entraîner sur des centaines de milliards de mots avec un seul CPU.

L'opération vectorielle « roi — homme + femme ≈ reine » devient viral. Le NLP change de paradigme : on n'utilise plus de règles linguistiques, on utilise des vecteurs.

---

### La maturité — Sentence-BERT (2019)

Reimers et Gurevych publient Sentence-BERT en 2019 à EMNLP. Le problème qu'ils résolvent est simple : BERT produit des embeddings de phrases de grande qualité, mais les comparer deux à deux nécessite des heures de calcul. Sentence-BERT utilise une architecture siamois (deux BERT qui partagent leurs poids) et une fonction de perte par similarité cosinus.

Le résultat : des embeddings de phrases qui peuvent être comparés en quelques millisecondes via un produit scalaire. C'est exactement ce dont on avait besoin pour la mémoire vectorielle — des embeddings rapides à calculer, rapides à comparer, sans perte de qualité.

---

### L'infrastructure — bge-small (BAAI, 2024)

BAAI (Beijing Academy of Artificial Intelligence) publie la série bge (BAAI General Embedding) en 2024. bge-small-en-v1.5 fait 384 dimensions. C'est le plus petit modèle de la famille — assez compact pour tourner sur CPU, assez riche pour capturer les nuances sémantiques.

Sur le MTEB (Massive Text Embedding Benchmark), bge-small atteint des scores comparables à des modèles 5 fois plus grands. Le ratio performance/coût est le meilleur de sa catégorie.

---

### L'algorithme — HNSW (2016)

Malkov et Yashunin publient HNSW (Hierarchical Navigable Small World) en 2016. C'est un algorithme d'approximation du plus proche voisin (ANN) qui construit un graphe hiérarchique navigable.

L'idée : construire plusieurs couches du graphe, chaque couche étant une version sous-échantillonnée de la précédente. La recherche commence par la couche la plus haute (peu de nœuds, navigation grossière) et descend progressivement vers les couches inférieures (navigation fine).

ES 8.18 utilise HNSW comme algorithme par défaut pour la recherche kNN. C'est ce qui permet une latence de 11ms sur 311 000 vecteurs.

---

### L'écosystème — Elasticsearch comme base vectorielle

ES 8.0 (2022) introduit le support natif des vecteurs et de la recherche kNN. Avant, ES stockait des vecteurs comme des champs float — sans capacité de recherche. Depuis 8.0, ES implémente HNSW, le scoring par similarité cosinus, et la recherche hybride combinant BM25 et kNN (RRF).

Notre index « public-memory_atoms » utilise exactement cette capacité : un mapping qui déclare le champ `vector` en `dense_vector` avec `index: true` et `similarity: cosine`. La recherche se fait via ES kNN, pas via un service externe.

---

### Le framework — Hermes Agent (Nous Research, 2024)

Hermes Agent est le framework qui a tout rendu possible. Il fournit :
- L'architecture des MemoryProviders (ABC, 315 lignes)
- Le cycle de vie du plugin (register, activate, deactivate)
- Le mécanisme de prefetch qui appelle tous les providers
- Le système de profils, de plugins, de skills

Le patch Hermes — une ligne dans memory_manager.py — ne fonctionne que parce que l'architecture est propre. Le builtin n'est pas spécial, il est juste le premier. Le rendre facultatif était une modification triviale une fois qu'on a compris le code.

---

### La filiation complète

```
Harris (1954) → Distributional hypothesis
    ↓
Landauer & Dumais (1997) → LSA — algèbre linéaire
    ↓
Mikolov (2013) → Word2Vec — réseau peu profond
    ↓
Reimers & Gurevych (2019) → Sentence-BERT — architecture siamois
    ↓
BAAI (2024) → bge-small — 384 dimensions, CPU, MTEB
    ↓
Nous Research (2024) → Hermes Agent — architecture de plugins
    ↓
Malkov & Yashunin (2016) → HNSW — algorithme de recherche kNN
    ↓
Elasticsearch 8.0+ → Stockage et recherche vectorielle
    ↓
Nous (juillet 2026) → 311 442 atomes, 11ms, 10/10, MIT
```

Chaque maillon a permis le suivant. Sans Harris, LSA n'aurait pas de fondement. Sans LSA, Word2Vec n'aurait pas démontré la scalabilité. Sans Word2Vec, Sentence-BERT n'aurait pas été nécessaire. Sans Sentence-BERT, bge-small n'aurait pas été entraîné. Sans Hermes Agent, λ n'aurait pas eu d'architecture. Sans ES 8.0, le stockage vectoriel aurait nécessité un service externe. Sans HNSW, la latence serait en secondes au lieu de millisecondes.

Nous sommes arrivés au bon moment, avec les bons outils, parce que la filiation était déjà tracée. Notre contribution est ailleurs : l'intégration, l'atomisation, le filtre Synapse, et la décision que tout soit MIT.
