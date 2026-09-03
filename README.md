# Kit de démarrage — base projet réutilisable

Ce dépôt contient les documents de base à charger dans **n'importe quel** nouveau projet, avant de commencer le cahier des charges avec Claude — peu importe le projet, l'étudiant, ou le compte Claude utilisé. Il sert de copie externe stable : accessible à tous, indépendamment d'un compte ou d'un ordinateur Claude en particulier.

## Contenu

- `methode-projet-design-reference.md` — la méthode complète en 7 phases : cadrage → cahier des charges → état du projet → prototype interactif audité → empaquetage → mise en place dans l'outil de code → construction écran par écran.
- `pages-fonctionnalites-universelles.md` — la checklist des pages et fonctionnalités qui reviennent sur presque tout projet web (identité/session, paramètres, sécurité, tableau de bord, etc.), à trier selon le projet.
- `detail-fonctionnalites-universelles.md` — le détail fonctionnel précis (champs, règles, états, cas limites) de chaque item de cette checklist.
- `instructions-projet-kitliss-starter.md` — le texte à coller **une seule fois, dans les paramètres du Project** (pas dans le chat). Une fois en place, il suffit de taper "kitliss-starter" dans un message pour déclencher le chargement des 3 documents ci-dessus. **Méthode recommandée.**
- `prompt-etudiant-demarrage.md` — méthode alternative : le prompt complet à copier-coller directement dans le premier message du chat (utile si on ne veut pas toucher aux paramètres du Project, ou si le champ "instructions du projet" n'est pas disponible sur son plan).

## Pour les étudiants : comment démarrer un nouveau projet

**Méthode recommandée — "kitliss-starter"**

1. Crée un nouveau Project claude.ai dédié à ton propre projet (pas une conversation isolée).
2. Ouvre les paramètres de ce Project (icône de réglage / menu à côté du nom du Project — pas la zone des docs) et trouve le champ **"Instructions du projet"**.
3. Colle-y tout le contenu de `instructions-projet-kitliss-starter.md`. Ça ne se fait qu'une fois, à la création du Project.
4. Dans le chat, tape simplement : `kitliss-starter`
5. Une fois les 3 documents confirmés dans les docs de ton Project, tu peux commencer le cadrage de ton projet (Phase 0 de `methode-projet-design-reference.md`).

**Méthode alternative — sans toucher aux paramètres**

1. Ouvre une nouvelle conversation Claude, rattachée à un Project claude.ai dédié à ton projet.
2. Copie-colle tout le contenu de `prompt-etudiant-demarrage.md` dans ton tout premier message.
3. Une fois les 3 documents confirmés, commence le cadrage (Phase 0).

## Pour l'enseignant : maintenir ce kit à jour

Ces documents évoluent avec l'expérience (chaque projet réel fait remonter des ajustements). Remplace simplement les fichiers dans ce dépôt par leur nouvelle version — les étudiants qui redémarrent un nouveau projet après la mise à jour récupèrent automatiquement la dernière version, quelle que soit la méthode utilisée (les deux pointent vers les mêmes URLs GitHub).
