# Kit de démarrage — base projet réutilisable

Ce dépôt contient les documents de base à charger dans **n'importe quel** nouveau projet, avant de commencer le cahier des charges avec Claude — peu importe le projet, l'étudiant, ou le compte Claude utilisé. Il sert de copie externe stable : accessible à tous, indépendamment d'un compte ou d'un ordinateur Claude en particulier.

## Contenu

- `methode-projet-design-reference.md` — la méthode complète en 7 phases : cadrage → cahier des charges → état du projet → prototype interactif audité → empaquetage → mise en place dans l'outil de code → construction écran par écran.
- `pages-fonctionnalites-universelles.md` — la checklist des pages et fonctionnalités qui reviennent sur presque tout projet web (identité/session, paramètres, sécurité, tableau de bord, etc.), à trier selon le projet.
- `detail-fonctionnalites-universelles.md` — le détail fonctionnel précis (champs, règles, états, cas limites) de chaque item de cette checklist.
- `prompt-etudiant-demarrage.md` — le prompt prêt à copier-coller pour démarrer un nouveau projet avec ces 3 documents déjà chargés.

## Pour les étudiants : comment démarrer un nouveau projet

1. Ouvre une nouvelle conversation Claude, rattachée à un **Project** claude.ai dédié à ton propre projet (pas une conversation isolée).
2. Copie-colle tout le contenu de `prompt-etudiant-demarrage.md` dans ton tout premier message.
3. Une fois les 3 documents confirmés dans les docs de ton Project, tu peux commencer le cadrage de ton projet (Phase 0 de `methode-projet-design-reference.md`).

## Pour l'enseignant : maintenir ce kit à jour

Ces documents évoluent avec l'expérience (chaque projet réel fait remonter des ajustements). Remplace simplement les fichiers dans ce dépôt par leur nouvelle version — les étudiants qui redémarrent un nouveau projet après la mise à jour récupèrent automatiquement la dernière version via le prompt de démarrage.
