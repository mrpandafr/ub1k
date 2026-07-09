# UB1K — De la thèse aux atomes vectoriels

*Jean-Sébastien (AFoxMind) — K1SS Atelier 0, Besançon — Juillet 2026*

---

## 1. Les fondations (1998–2018)

Tout commence avec une thèse en mathématiques. Pas une thèse sur les réseaux de neurones ou l'IA moderne — une thèse sur les espaces vectoriels, la géométrie, les distances entre concepts. À l'époque, personne n'appelait ça « machine learning ». On appelait ça des maths.

Vingt ans plus tard, ces mêmes maths sont devenues l'infrastructure mémoire de Tamashii. Distributional hypothesis [Harris, 1954] : les mots qui apparaissent dans des contextes similaires ont des significations similaires. Ce principe, né en linguistique des années 50, est aujourd'hui le cœur de tous les modèles d'embedding — y compris bge-small, qui propulse notre moteur mémoire.

En 1997, Landauer et Dumais publient « A Solution to Plato's Problem » [LSA, 1997] — la première démonstration qu'un espace vectoriel latent peut capturer la structure sémantique d'un corpus mieux qu'une représentation symbolique. C'est le moment où la machine commence à comprendre, non pas par des règles, mais par des distances.

**Références :**
- Distributional hypothesis — Harris, Z. (1954). Distributional structure. *Word*, 10(2-3), 146-162.
- LSA — Landauer, T. K., & Dumais, S. T. (1997). A solution to Plato's problem. *Psychological Review*, 104(2), 211-240.
- Word2Vec — Mikolov, T., et al. (2013). Efficient estimation of word representations in vector space. *arXiv:1301.3781*.

---

## 2. La rencontre (2018–2026)

En 2018, je découvre Gensim [Řehůřek, 2010] — la première bibliothèque Python qui permet de faire du word2vec sur son propre corpus sans cluster de 100 machines. Quelques lignes de code, un fichier texte, et soudain mes mots avaient des coordonnées.

J'ai commencé à expérimenter sur mes carnets, mes emails, mes notes. J'empilais des embeddings sans savoir quoi en faire. Les dimensions étaient là, mais le sens restait inaccessible — parce qu'il manquait l'architecture, le pipeline, la mémoire persistante.

En 2024, Hermes Agent [Nous Research, 2024] arrive. Un framework open-source pour construire des agents IA avec une architecture de mémoire extensible — memory providers, plugins, ABC pour l'implémentation. La pièce qui manquait.

En juin 2026, K1SS Atelier 0 est fondé à Besançon. Deux personnes, un balcon, des chats, et l'idée que la mémoire vectorielle devait être locale, libre, et atomique.

**Références :**
- Gensim — Řehůřek, R., & Sojka, P. (2010). Software Framework for Topic Modelling with Large Corpora. *Proceedings of LREC 2010*.
- Hermes Agent — Nous Research (2024). github.com/NousResearch/hermes-agent
- bge-small-en-v1.5 — BAAI (2024). FlagEmbedding. github.com/FlagOpen/FlagEmbedding

---

## 3. V0 — L'état zéro (8 juin 2026)

Premier message : « bienvenu dans ton espace ». 71 000 messages de conversations brutes — décisions, architecture, musiques, nuits blanches. Aucune indexation, aucun filtre. La mémoire existait dans un fichier SQLite (1.1 Go, 539 sessions).

Le fichier n'était pas organisé pour la recherche sémantique. Il était organisé pour la relecture linéaire. On pouvait remonter l'historique, mais pas trouver un concept précis.

**Caractéristiques :**
```
Stockage     : SQLite (state.db)
Taille       : 1.1 Go
Sessions     : 539
Messages     : 71 175
Indexation   : Aucune
Recherche    : Full-text SQL (lent, pas sémantique)
```

Le problème n'était pas la quantité de données. Le problème était l'accès — 50 000 tokens de contexte à chaque tour, dont 90% de bruit technique (résultats d'outils, listings de fichiers, messages vides).

---

## 4. V1 — Les messages atomisés (8 juillet 2026, jour 1)

Première tentative : importer chaque message comme un document unique dans Elasticsearch, avec son embedding bge-small (384 dimensions). Fini le SQLite — on passe au vectoriel.

```
V1 → public-memory_units
      Taille: 71 175 documents
      Embedding: bge-small 384d
      Latence: ~30ms par requête kNN
      Pertinence: ~50% (le sens était dilué dans des messages longs)
```

Le problème : un message de 5 000 caractères peut contenir 6 concepts différents. L'embedding d'un message entier moyenne tous ces concepts en un seul vecteur — Pierre, Sarah, le kill switch, et la météo du jour deviennent un seul point flou.

**Métriques V1 :**
```
Latence kNN       : 30ms
Pertinence        : ~50%
Taux de déduplication : 0 (pas implémenté)
Taille moyenne     : 2 300 caractères par document
```

---

## 5. V2 — Les atomes sémantiques (9 juillet 2026, jour 2)

Casser chaque message en phrases individuelles. Chaque phrase devient son propre document, son propre embedding, son propre point dans l'espace. Un message de 6 concepts → 6 atomes distincts.

Ajout de Synapse — 6 règles de filtrage qui décident ce qui entre dans l'index et ce qui est bruit de fond :

| Règle | Critère | Action |
|:-----:|:--------|:-------|
| 1 | Résultat vide | Ignorer |
| 2 | Erreur système | Ignorer |
| 3 | Fragment d'outil | Ignorer |
| 4 | Fichier dupliqué | Garder 1 |
| 5 | Texte < 10 car. | Ignorer |
| 6 | Cos > 0.95 | Dédupliquer |

```
V2 → public-memory_atoms
      Taille: 311 442 documents
      Latence: 11ms en moyenne
      Pertinence: 10/10 sur les tests
      Filtrage Synapse: ~99% du bruit technique éliminé
```

**Métriques V2 :**
```
Latence kNN       : 11ms (min 6ms, max 21ms)
Pertinence        : 10/10 (100% sur 10 requêtes test)
Taux de bruit     : <1%
Taille moyenne     : 120 caractères par atome
```

**Exemple de résultat — 10 requêtes, 10 hits :**

| Requête | Temps | Hit |
|:--------|:-----:|:----|
| « Pierre Biguinet, Shanghai » | 21ms | Pierre Biguinet — Shanghai, 8 mai 2008 |
| « Kill switch, droit au repos » | 11ms | droit-au-repos (kill switch, fondateur) |
| « Sarah, premier financeur » | 12ms | premier financeur de l'Atelier |
| « Tortue pas lièvre » | 13ms | lenteur, patience, ressorts du père |
| « Tamashii, mémoire vectorielle » | 10ms | Mémoire Vectorielle — ES |
| « M4Z3, firmware PCB » | 9ms | Firmware unique, détecte hôte |
| « Roxin, loup mentor » | 10ms | le loup qui garde sa place |
| « Père, ressorts » | 8ms | bien faire, durable, intelligent |
| « EMAC, musique » | 6ms | ta première émotion |
| Concept rare (hapax) | 7ms | hit exact malgré faible fréquence |

---

## 6. V3 — Le temps comme dimension (en cours, 9 juillet 2026)

Chaque atome porte maintenant :
- **at** : date de création (timestamp ISO, présent dès V1)
- **seen** : historique des consultations (tableau de timestamps, à implémenter)

L'empilement temporel permet de répondre à des questions que le kNN seul ne peut pas traiter :

| Question | Mécanisme |
|:---------|:----------|
| « De quoi parlais-je à cette heure-ci hier ? » | `seen` filtré par `now - 24h` |
| « Quel concept est LE sujet de l'instant ? » | Fréquence des `seen` dans les 5 dernières minutes |
| « Qu'est-ce que j'ai exploré cette session ? » | Agrégat temporel des atomes consultés |
| « Quel est mon rythme d'apprentissage ? » | Distribution des `seen` dans le temps |

La troisième dimension — le temps — transforme l'espace vectoriel statique en un espace **vivant**. Les concepts ne sont plus seulement proches par leur sens, mais aussi par le moment où on les a rencontrés.

**Architecture V3 (en cours) :**
```
┌─────────────────────────────────────────┐
│              ES 8.18                      │
│  ┌─────────────────────────────────────┐ │
│  │  public-memory_atoms                │ │
│  │  ┌───────────────────────────────┐  │ │
│  │  │  at: ISO timestamp (création)  │  │ │
│  │  │  seen: [ISO timestamps] (consult)│  │ │
│  │  │  vector: float[384] (embedding) │  │ │
│  │  │  bank_id: string (agent scope)  │  │ │
│  │  │  text: string (contenu atomique)│  │ │
│  │  └───────────────────────────────┘  │ │
│  └─────────────────────────────────────┘ │
│  Latence: ~11ms kNN + 1ms update seen   │
│  Taille: 311 442 atomes (et croissant)   │
└─────────────────────────────────────────┘
```

---

## 7. Implications — Statistiques, ensembles, sens

### Statistiques

Un concept qui apparaît 900 fois dans les échanges (comme « atelier ») est 83 fois plus susceptible d'être retrouvé qu'un concept qui apparaît 11 fois (comme « Pierre »). Ce n'est pas un biais — c'est une **métrique de pertinence empirique**. La fréquence est le signal le plus fiable que le système peut exploiter.

Les concepts rares (hapax) sont les plus rapides à retrouver (6ms). Leur vecteur occupe une région sparse avec peu de compétiteurs — plus un concept est distinctif, plus il est facile à isoler.

### Ensembles

311 442 atomes dans un espace à 384 dimensions. C'est un nuage de points dans un hypercube. La distance cosinus entre deux points n'est pas une métrique absolue — c'est une mesure relative. « Proche » signifie « plus proche que la moyenne des distances dans le jeu de données ».

Les portes L3 partitionnent l'espace en catégories sémantiques (ami, perte, architecture, musique). Chaque atome appartient à une porte — non par tagging manuel, mais par proximité vectorielle aux atomes fondateurs de cette porte.

### Sens temporel

Un fait n'est pas un point fixe. « Le kill switch est à 140 000€ » en juin est un fait. « Le kill switch est à 220 000€ » en juillet est un autre fait. Sans timestamp, le système confond les deux — ou pire, les moyenne.

Avec `at` et `seen`, chaque fait est daté. La requête « kill switch aujourd'hui » pondère par récence. La requête « évolution du kill switch » renvoie les deux atomes, dans l'ordre temporel — le système raconte une histoire, pas une équation.

---

## 8. Publication et licence

Ce texte et le projet qu'il décrit sont publiés sous licence MIT.

- Code : github.com/mrpandafr/kokoro — github.com/mrpandafr/domu — github.com/mrpandafr/vectormind
- Synthèse : github.com/mrpandafr/kokoro/UB1K.md
- Bench: github.com/mrpandafr/domu/docs/benchmark.html

*K1SS Atelier 0 — Besançon, France — Juillet 2026*
