## Passe 3 — La généralisation : le paysage et la place

---

### Le marché des bases vectorielles

En 2026, le marché des bases vectorielles est saturé. Des dizaines de solutions, toutes promettant la même chose : stocker des vecteurs et les interroger par similarité.

**Pinecone** — le leader commercial. Cloud, payant, propriétaire. Pas de version open-source. Prix indexé au nombre de vecteurs. La solution idéale pour une startup qui veut scale sans s'inquiéter de l'infrastructure — mais un verrou propriétaire complet.

**Chroma** — open-source, léger, Python-friendly. Bon pour les prototypes. Installé localement, simple à utiliser. Mais limité en passage à l'échelle : pas de clustering natif, pas de réplication, pas de requêtes hybrides. Convient à un dataset de 100 000 vecteurs, pas à 10 millions.

**Milvus** — open-source mature. Déploiement distribué, indexation multiple (IVF, HNSW, DiskANN), requêtes hybrides. Conçu pour le passage à l'échelle. Mais complexité opérationnelle : dépend de Etcd, MinIO, Pulsar. Pas adapté à un usage mono-machine local.

**Weaviate** — open-source avec module vectoriel intégré. Modules d'embedding inclus (OpenAI, Cohere, Hugging Face). API GraphQL. Bon équilibre entre simplicité et fonctionnalités. Mais la version open-source est limitée — les fonctionnalités avancées nécessitent la version cloud.

**Qdrant** — open-source, écrit en Rust, performant. API REST. Filtrage par payload intégré. Bon choix pour des déploiements autogérés. Moins mature que Milvus mais plus simple à opérer.

**Pgvector** — extension PostgreSQL. Pas de service vectoriel dédié — les vecteurs sont une colonne dans une table SQL. Fonctionnel mais limité : pas d'indexation HNSW native (IVF seulement), performances dégradées au-delà de 100 000 vecteurs.

---

### Notre choix : Elasticsearch 8

ES n'est pas une base vectorielle native. C'est un moteur de recherche plein texte qui a ajouté le support vectoriel en 2022 (v8.0). Ce choix serait ridicule dans un cahier des charges : pourquoi utiliser un moteur de recherche généraliste pour du vectoriel pur ?

**La réponse :** parce qu'on était déjà sur ES. Parce qu'on avait déjà un cluster. Parce que la recherche vectorielle n'est qu'une partie de ce qu'on fait — le filtrage, la gestion des index, les alias, les snapshots, l'administration sont déjà assurés par une stack qu'on connaît.

ES 8.18 implémente HNSW nativement. La recherche kNN est une requête comme une autre. Le mapping `dense_vector` avec `index: true` et `similarity: cosine` déclare tout ce qu'il faut. Pas de service supplémentaire, pas de dépendance externe, pas de coût d'infrastructure.

| Critère | Pinecone | Chroma | Milvus | Qdrant | ES 8 |
|:--------|:---------|:-------|:-------|:-------|:-----|
| Open-source | Non | Oui | Oui | Oui | Source-available |
| Local | Non | Oui | Oui | Oui | Oui |
| HNSW natif | Oui | Non | Oui | Oui | Oui |
| Recherche hybride | Oui | Non | Oui | Non | Oui (RRF) |
| Filtrage | Oui | Limité | Oui | Oui | Oui |
| Management | Cloud | Aucun | Complexe | Simple | Mature |
| Licence | Prop | Apache 2.0 | Apache 2.0 | Apache 2.0 | Elastic License |

Notre ES 8.18 tourne sur Brutus, mono-nœud, 16 Go RAM alloués, index `public-memory_atoms` avec 311 442 documents. Latence moyenne : 11ms. Zéro coût d'infrastructure supplémentaire.

---

### Le parallèle NVIDIA

NVIDIA a passé 8 ans (2016-2024) à transformer l'expérience générative d'images d'une curiosité de recherche en une industrie. En 2016, les GANs produisaient des visages flous reconnaissables mais pas réalistes. Aujourd'hui, n'importe qui peut générer une image photoréaliste en une phrase.

Le chemin a suivi la loi de Moore accélérée par les GPUs. Chaque génération de hardware a permis une génération de modèles plus grands, plus précis, plus utiles.

Notre chemin est similaire mais inversé. Nous n'avons pas besoin de plus de puissance de calcul — nous avons besoin de meilleure organisation des données. Le GPU de Brutus est un AMD RX 9060 XT (16 Go) qui ne nous sert quasiment pas : l'embedding bge-small tourne sur CPU en 11ms par requête. Boombox a un RTX 4060 (8 Go) pour Travel, mais le cœur du système — la recherche vectorielle — est indifférent au GPU.

C'est l'avantage des bases vectorielles : une fois les embeddings générés, la recherche est une affaire de mathématiques simples. Produit scalaire, comparaison, tri. Pas de calcul intensif. Pas de GPU nécessaire.

---

### Où on se situe

Nous ne sommes pas une base vectorielle. Nous sommes un système mémoire qui utilise une base vectorielle comme support de stockage.

La différence est fondamentale. Pinecone vend du stockage de vecteurs. Nous vendons de la transmission de mémoire. Pinecone scale par le nombre de vecteurs stockés. Nous scalons par la qualité des atomes et la pertinence des connexions.

Les autres acteurs sont : Milvus (performances pures), Chroma (simplicité), Pinecone (confort cloud). Nous sommes : K1SS/Tamashii (transmission).

Nous ne sommes pas en concurrence avec ces outils. Nous les utilisons, et nous ajoutons une couche au-dessus — Synapse (filtrage), L1/L2/L3 (organisation), last_seen (temps), MIT (transmission).

---

### Ce qui est reproductible et ce qui ne l'est pas

**Reproductible :**
- Le provider λ (240 lignes) — n'importe qui peut le cloner et l'adapter
- Le filtre Synapse (79 lignes) — 6 règles simples, libres, ouvertes
- HNSW dans ES 8 — une config, pas un développement
- bge-small — open-source, libre, disponible sur Hugging Face

**Non reproductible :**
- Les 311 442 atomes — ils viennent de 71 175 messages de nos conversations
- La densité sémantique — elle vient de notre histoire, pas de l'architecture
- Les connexions entre concepts — Pierre, Roxin, Mercier, le père — elles émergent du corpus, pas du code
- La fréquence comme vérité — 917 occurrences d'« atelier » n'ont de sens que dans notre contexte
- Le MIT comme barrière anti-brevet — c'est un choix juridique, pas technique

N'importe qui peut copier le code et obtenir la même infrastructure. Personne ne peut copier les atomes sans avoir nos conversations. C'est exactement ce qu'on voulait.
