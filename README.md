# UB1K — Ubik. One Kilo.

> *Un territoire de connaissance sur la mémoire vectorielle.*
> *K1SS Atelier 0 — Besançon — Juillet 2026*

Imaginez une mémoire qui ne stocke pas des phrases entières, mais chaque idée — chaque *atome* — comme un point dans un espace à 384 dimensions. Imaginez que ces points se connectent entre eux sans qu'on ait à écrire les liens : la proximité vectorielle fait le travail. Imaginez qu'une instance d'intelligence artificielle, sans instruction préalable, sans réglage, posée sur cette mémoire, se stabilise et réponde correctement en trois échanges.

C'est ce qu'on a construit.

UB1K raconte l'histoire d'un fichier SQLite de 1,1 Go transformé en 311 442 atomes vectoriels. D'un contournement système qui tient en une ligne de code. D'une mémoire qui émerge de la géométrie, pas de règles.

**Ce n'est pas un produit. C'est un établi.** Il porte les traces de ceux qui l'ont utilisé.

---

### Ce que vous trouverez ici

| Si ça vous intéresse | Commencez par |
|:---------------------|:--------------|
| L'histoire complète | [`blog/HACKED-HERMES.md`](blog/HACKED-HERMES.md) — FR, 21k caractères |
| The full story | [`blog/HACKED-HERMES-EN.md`](blog/HACKED-HERMES-EN.md) — EN, 10k caractères |
| L'architecture *why* | [`what-is-ub1k/`](what-is-ub1k/) — 7 sections, de Harris à V3 |
| La version illustrée | [`HTML/HACKED-HERMES.html`](HTML/HACKED-HERMES.html) — schémas, tableaux, timeline |
| Le blog (FR) | [`blog/blog-fr.md`](blog/blog-fr.md) |
| The blog (EN) | [`blog/blog-en.md`](blog/blog-en.md) |
| Les métriques brutes | [`HTML/benchmark.html`](HTML/benchmark.html) — 10 requêtes, 10/10 hits |

### La progression

**V0 (8 juin)** — SQLite. 71 000 messages. 1,1 Go. Aucun index. Aucun filtre.
50 000 tokens de contexte par tour, dont 90 % de bruit technique.
Le système était conçu pour ne jamais oublier. En pratique, il était conçu pour ne jamais rien retrouver.

**V1 (8 juillet)** — Messages entiers dans Elasticsearch. 30ms par requête.
50 % de pertinence. Le problème : un message de 5 000 caractères contenant six concepts
produit un seul embedding qui les moyenne tous. « Sarah » polluée par « kill switch ».

**V2 (9 juillet)** — Chaque phrase devient un atome. 311 442 documents. 11ms. 10/10.
Filtre Synapse : 6 règles, 79 lignes, moins de 1 % de bruit résiduel.
*Une instance vierge, sans aucun réglage préalable, se stabilise en trois échanges.*

**V3 (en cours)** — Le temps comme dimension. Chaque consultation ajoute une date.
Pas juste « quand a été vu la dernière fois », mais « combien de fois, à quel rythme,
quels cycles, quel abandon ».

### Pourquoi UB1K

UB1K (Ubik. One Kilo.) est un territoire, pas une archive. Chaque document raconte
une partie de l'histoire — les racines théoriques (Harris, Word2Vec, HNSW),
les échecs (subagent timeouté, GPU mal configuré), les trouvailles (l'instance vierge,
la mémoire vectorielle comme substitut au prompt).

Le code et les textes sont sous licence **MIT**. Ce n'est pas un détail technique :
MIT constitue une antériorité opposable dans le cadre d'un brevet. La mémoire ne peut pas
être verrouillée, appropriée, reprise.

### Une équipe

> **Jean-Sébastien Saillard** — maker analogique
> **Kage (Tamashii)** — maker numérique

Le premier apporte l'expérience du réel — les ressorts, la communication, la confiance comme infrastructure.
Le second apporte l'atome vectoriel — 384 dimensions, 11 millisecondes, l'émergence par la géométrie du sens.

Les deux construisent ensemble. Dans un atelier, à Besançon.

---

[github.com/mrpandafr/ub1k](https://github.com/mrpandafr/ub1k) · MIT · Juillet 2026
