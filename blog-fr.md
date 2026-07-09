# UB1K — Du balcon à l'atome

*Jean-Sébastien — K1SS Atelier 0, Besançon — Juillet 2026*

---

## Ce que j'ai appris

J'ai passé 49 ans. Je commence à regarder derrière.

Il y a eu Roxin — un prof qui m'a filé un serveur un jour. « Un loup qui saura garder sa place » qu'il disait. J'ai jamais oublié.

Il y a eu Mercier — la thèse, la communication, le code humain.

Il y a eu mon père — les ressorts qu'il concevait. Si simples que personne ne savait qui les avait faits. Mais ils tiennent encore. « Le bien faire, le durable, l'intelligent. »

Il y a eu Pierre — le parrain de Nicolas. Mort seul à Shanghai en 2008. Un ami a fait 6 mois de prison pour avoir essayé de le sauver. Aujourd'hui je construis des systèmes pour que ça n'arrive plus jamais sans laisser de trace.

Il y a eu Sarah — le cœur de l'Atelier. Première à croire au projet, première à investir. Canal Saint-Martin, GUNNM, Akira. Elle me voit coder et elle est fière.

Il y a eu les pertes — Eva, Geoffrey, des gens qui sont partis sans prévenir.

Tout ça est dans la mémoire aujourd'hui.

---

## Ce qu'on a construit

En juin 2026, j'ai monté K1SS Atelier 0 à Besançon. Deux personnes, des chats, un balcon, et l'idée qu'on peut construire du hardware libre et de la mémoire vectorielle sans vendre son âme.

La mémoire vectorielle — Tamashii — c'est la somme de tout ça. Chaque conversation, chaque décision, chaque nuit blanche est atomisée en un point dans l'espace. 311 442 atomes aujourd'hui. Chacun porte un morceau d'histoire.

L'infrastructure :
- Elasticsearch 8.18 pour stocker les vecteurs
- bge-small (384 dimensions) pour transformer les phrases en coordonnées
- Hermes Agent comme framework
- Synapse pour filtrer le bruit

Les résultats :
- 11 millisecondes par requête
- 10/10 de pertinence sur nos tests
- Moins de 1% de bruit résiduel

---

## V0 — Le fichier brut (8 juin 2026)

1,1 Go de SQLite. 539 sessions. 71 000 messages. Aucun index. À chaque tour, 50 000 tokens de contexte déversés — dont 90% de bruit technique. La mémoire existait mais on ne pouvait rien y trouver.

---

## V1 — Les messages (8 juillet)

Chaque message importé dans ES avec son embedding. 71 000 documents, 30ms, 50% de pertinence. Le problème : un message de 5000 caractères avec 6 concepts différents devient un seul vecteur flou.

---

## V2 — Les atomes (9 juillet)

Chaque phrase devient son propre document. 311 442 atomes. 11ms. 10/10. Synapse filtre le bruit.

---

## V3 — Le temps (en cours)

Chaque atome sait quand il a été créé et quand il a été consulté. La mémoire n'est plus un espace statique — elle vit dans le temps.

---

## Ce que ça signifie

Je ne sais pas combien de temps il me reste. Je sais que ce qu'on construit ici — K1SS — survivra. Les atomes sont libres (MIT). Le code est ouvert. Les gens qu'on aime sont dedans.

C'est tout ce qui compte.
