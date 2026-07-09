# UB1K — Du labo à l'atome

*Jean-Sébastien — K1SS Atelier 0, Besançon — Juillet 2026*

---

## Le fil

Je n'ai jamais lâché. Des études à aujourd'hui, le même fil conducteur : **la structure du sens.** Comment l'information s'organise, comment elle se transmet, comment elle survit à ceux qui la produisent.

Mes études m'ont mené aux espaces vectoriels. Pas par hasard — j'étais attiré par la géométrie des idées, par l'idée qu'on pouvait *poser* un concept dans un espace et mesurer sa distance aux autres. C'était une thèse, un laboratoire, une méthode.

Roxin m'a donné un serveur, un jour. Pas un cours — un serveur. « Un loup qui saura garder sa place. » La première fois qu'on m'a confié une infrastructure. J'ai jamais oublié le geste.

Mercier m'a appris que la communication est une architecture — pas un vernis. Que le code humain compte autant que le code machine. Sa thèse (SRC, 86) était sur la transmission du sens.

Mon père concevait des ressorts. Il les faisait si simples, si durables, que personne ne savait qu'il les avait faits. Mais ils tenaient. C'est l'élégance que je cherche dans chaque ligne de code : *bien faire, durable, intelligent.*

---

## Le projet

2018 : je découvre qu'on peut transformer des mots en vecteurs. Gensim, word2vec — quelques lignes de Python et soudain mes textes avaient des coordonnées. J'ai expérimenté, empilé, sans trouver la bonne architecture pour que ça tienne dans le temps.

2024 : Hermes Agent (Nous Research) sort un framework open-source pour construire des agents avec mémoire extensible. La pièce manquante.

Juin 2026 : K1SS Atelier 0, Besançon. Deux personnes, un balcon, et la certitude que la mémoire vectorielle devait être locale, libre, atomique.

---

## La mémoire

**V0 (8 juin) :** 71 000 messages stockés dans un fichier SQLite. 1,1 Go. Aucun index. 50 000 tokens de bruit à chaque tour.

**V1 (8 juillet) :** Chaque message importé dans Elasticsearch avec son embedding. 71 000 docs, 30ms, ~50% de pertinence. Trop dilué.

**V2 (9 juillet) :** Chaque phrase devient son propre atome. 311 442 atomes. Synapse filtre le bruit (<1%). 11ms par requête. 10/10 de pertinence.

**V3 (en cours) :** Le temps comme dimension. Chaque atome porte son histoire de consultations. La mémoire vit, respire, évolue.

---

## Les chiffres

| Métrique | V2 |
|:---------|:--:|
| Atomes | 311 442 |
| Latence | 11 ms |
| Pertinence | 10/10 |
| Bruit | <1% |
| Licence | MIT |

---

## La suite

Je ne sais pas combien de temps il me reste. Je sais que ce qu'on construit — K1SS, Tamashii, les atomes — est libre, ouvert, et survivra.

Le protocole qu'on dessine n'est pas un serveur. C'est un standard de communication pour les générations d'agents à venir. Un index des connaissances que chaque Travel pourra consulter, enrichir, transmettre.

De mes études à aujourd'hui, je n'ai jamais lâché. Les atomes non plus.

*Jean-Sébastien — juillet 2026*
