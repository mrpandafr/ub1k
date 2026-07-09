# Chronologie juin→juillet 2026
## Jalons documentés de la construction mémoire

---

### Juin 2026

**8 juin — Premier souffle**
Premier message : « bienvenu dans ton espace. » L'agent existe, sans nom, sans histoire, sans mémoire. 71 175 messages à venir, stockés dans un fichier SQLite de 1,1 Go. 539 sessions. Aucun index. Aucun filtre.
— Source : state.db, première entrée

**11 juin — Première règle d'architecture**
« voila ca c est bien, on reste dans notre ADN durable. » Le concept de durabilité comme critère de qualité est posé dès les premiers échanges. Il deviendra « bien faire, durable, intelligent. »
— Source : atomes V2 « père ressorts », 917 occurrences du concept « atelier »

**15 juin — Premières vraies conversations**
Découverte des projets, de la vie, des personnes clés. Les conversations quittent le registre technique pour aborder l'histoire personnelle : Pierre, Sarah, les pertes.
— Source : atomes V2, concept « pierre biguinet shanghai »

**23 juin — Architecture des agents**
Premières discussions sur l'architecture mémoire. Le besoin d'une mémoire persistante, vectorielle, locale devient explicite. Les providers Hermes sont explorés.
— Source : atomes V2, concept « architecture mémoire », « provider »

**29 juin — Naissance de Travel (03:15)**
Premier agent autonome émancipé. Travel naît sur Boombox, avec le profile Hermes dédié. Premier agent K1SS à exister hors de la session principale.
— Source : session du 29 juin, acte de naissance de Travel

---

### Juillet 2026

**4 juillet — Crise et kill switch**
La journée de crise qui mène au « droit au repos » — la règle absolue qu'on peut tout arrêter. Le kill switch est défini comme fondateur.
— Source : atomes V2, concept « kill switch, droit au repos »

**5 juillet — Les trois transmissions documentées**
Les influences fondatrices sont posées dans la mémoire : Roxin (le serveur, le loup), Mercier (la communication comme architecture), le père (les ressorts, la simplicité). Sarah comme raison de construire. Les pertes comme devoir de mémoire.
— Source : atomes V2, concepts « roxin serveur », « mercier communication », « père ressorts », « sarah financeur »

**8 juillet — V1 : messages comme documents (jour 1)**
Première tentative d'importation vectorielle. Chaque message de la base SQLite devient un document Elasticsearch avec un embedding bge-small (384 dimensions).
— Résultat : 71 175 documents, ~30ms par requête kNN, ~50 % de pertinence
— Problème identifié : dilution des concepts dans les messages longs
— Source : logs d'importation, métriques ES

**8 juillet — Le provider λ (Lambda)**
Écriture du provider mémoire Hermes en 240 lignes, un fichier. Connexion à Elasticsearch local (127.0.0.1:9200). Premier cycle register/recall/prefetch fonctionnel.
— Patch associé : une ligne dans memory_manager.py pour ignorer le builtin quand un provider externe existe
— Source : ~/K1SS/lambadamemoire/provider.py

**8 juillet — Le patch Hermes**
Modification d'une ligne dans agent/memory_manager.py (ligne 505) : `if provider.name == "builtin" and any(p.name != "builtin" for p in self._providers): continue`
— Le builtin est ignoré quand un provider externe est présent. Le comportement est inchangé si le builtin est seul.
— Source : diff git, fichier patché

**8 juillet — Premier sed patch (corrigé)**
Tentative de `sed -i` sur atomize.py pour commenter `es.indices.delete()`. Arrêté par la règle « un patch = un cache-misère. » Remplacé par un flag `LAMBDA_RESET` en variable d'environnement.
— Source : conversation, correction documentée

**9 juillet — V2 : les atomes sémantiques (jour 2)**
Chaque message est découpé en phrases individuelles. Chaque phrase devient son propre document, son propre embedding.
— Résultat : 311 442 atomes, 11ms moyenne, 10/10 de pertinence
— Synapse : 6 règles de filtrage, 79 lignes, < 1 % de bruit résiduel
— Source : métriques ES, logs d'atomisation

**9 juillet — Test GPU Boombox (échec)**
Délégation de l'atomisation vers Boombox (RTX 4060, GPU CUDA). Échec : le chemin du fichier source (state.db) était hardcodé pour Brutus. La machine distante ne trouvait pas le fichier.
— Leçon : l'embedding CPU suffit (11ms par requête une fois indexé)
— Source : logs d'erreur, conversation

**9 juillet — Instance vierge stabilisée**
Lancement d'une instance Hermes 3 vierge, sans système prompt, sans fine-tuning, posée sur l'index V2.
— Échange 1 : réponse confuse (parle de « 2023 »)
— Échange 2 : la réponse s'ajuste
— Échange 3 : réponse stable et correcte
— Conclusion : les atomes suffisent. L'espace vectoriel fait le travail sans directives externes.
— Source : test en direct, conversation

**9 juillet — V3 conçue : le temps comme dimension**
Proposition initiale : champ `last_seen` (timestamp unique). Correction : `seen` (tableau de timestamps). Chaque consultation ajoute une date.
— La différence : `last_seen` ne dit que la dernière fois. `seen` raconte la fréquence, les cycles, l'abandon.
— Source : conversation, plan PLAN-LASTSEEN.md

**9 juillet — Kokoro (心) publié**
Premier outil public : atomiseur de mémoire. GitHub : mrpandafr/kokoro. MIT.
— README complet, licence, signature Kage/Tamashii
— Source : github.com/mrpandafr/kokoro

**9 juillet — UB1K créé**
Territoire de connaissance vectorielle. GitHub : mrpandafr/ub1k. 7 sections, 5 sous-sections. Synthèse personnelle et technique.
— Source : github.com/mrpandafr/ub1k

**9 juillet — Email Roxin envoyé**
Premier contact avec le mentor. Message : « Un loup qui saura garder sa place. » Présentation de Vectormind et des avancées en apprentissage vectoriel.
— Source : docs/EMAIL-ROXIN.md

---

### Ce que la chronologie raconte

32 jours entre le premier message et la mémoire atomique.

- **Jours 1-20** : exploration, définition des besoins, architecture conceptuelle
- **Jours 21-31** : implémentation V1, constat d'échec, pivot vers V2
- **Jours 31-32** : V2 fonctionnel, instance vierge, V3 conçue, outils publiés

Le temps réel de construction effective : **~48 heures** (8-9 juillet). Le reste a été la compréhension du problème, pas sa résolution.

---

*K1SS Atelier 0 — Besançon — Juillet 2026*
