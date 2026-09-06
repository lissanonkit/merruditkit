# Méthode : d'un brief à un dossier de référence design prêt pour la construction

> Canevas réutilisable sur n'importe quel projet, pour arriver à un cahier des charges solide, un prototype interactif audité, et un dossier de référence design que l'outil de code (izikit/Antigravity ou autre) suit à la lettre au lieu d'improviser.

## Pourquoi un "design reference html" échoue, en général

Huit causes reviennent presque à chaque fois :
1. **Brief trop vague** au départ → le prototype qui en sort est générique, sans vraie logique métier.
2. **Maquette statique** (captures ou images figées) au lieu d'un **outil navigable** avec de vraies interactions et de vraies données d'exemple cohérentes.
3. **Pas d'étape d'audit dédiée** avant de considérer que c'est fini → les bugs partent directement dans la construction réelle.
4. **Pas de méthode explicite de passage de relais** vers l'outil de code → l'agent de code ignore le prototype et invente son propre style par défaut.
5. **Les prompts à coller sont noyés dans un guide** (explications + exemple + modèle mélangés) → au moment de copier-coller, la frontière entre "ce qu'il faut lire" et "ce qu'il faut copier" devient invisible dans un éditeur brut : on emporte un bout d'instruction en trop, ou on coupe la fin d'une phrase. Voir la règle d'or en Phase 5.
6. **Le backend arrive d'un coup à la fin** → chaque écran est reproduit à la perfection visuellement, mais aucune vraie logique ne l'accompagne ; l'outil de code se retrouve à devoir deviner toute la logique métier de tous les écrans à la fois, d'où une avalanche de questions bloquantes au pire moment. Voir le prompt de fondations backend en Phase 5.
7. **Des écrans "fantômes"** → un écran référencé seulement en creux dans le prototype (l'aperçu d'un contenu déjà soumis par un utilisateur, une mention d'un lien ou d'un document envoyé ailleurs) sans jamais avoir été construit comme un écran à part entière — l'outil de code ne peut pas le construire puisqu'il n'est documenté nulle part. Voir le repérage en Phase 4.
8. **Des composants transverses confondus avec des écrans** → un élément présent sur toutes les pages (bandeau de cookies, centre de notifications, invite d'installation en PWA) n'est ni un écran à part entière ni un détail propre à un seul écran. Non repéré comme tel, il finit soit oublié du dossier de référence, soit décrit en double (et de façon incohérente) dans chaque prompt d'écran. Voir le repérage en Phase 4 et le traitement dédié en Phase 5/7.

Les 7 phases ci-dessous existent spécifiquement pour boucher chacun de ces huit trous. Ne pas sauter de phase, et surtout ne jamais fusionner les phases 3 et 4 — l'audit doit rester une étape à part, explicitement demandée.

---

## Phase 0 — Cadrage

**Qui fait quoi :** toi, en langage libre — pas de formulaire à remplir, mais le brief doit couvrir ces points, même implicitement, avant de passer à la suite :
- Pour qui est le produit, et quel problème précis il résout.
- Ce qui existe déjà (le cas échéant) et pourquoi on le refait plutôt que de le corriger.
- Les contraintes non négociables : juridiction/pays, budget, outil de code déjà choisi, technologies imposées.
- Ce qui est explicitement exclu ou hors périmètre.
- Le format de livrable final attendu (site, back-office, les deux, etc.).

Si un de ces points manque, Claude le demande avant d'avancer plutôt que de deviner.

**Réflexe supplémentaire, avant de passer au cahier des charges :** parcourir `pages-fonctionnalites-universelles.md` (checklist niveau 1 — identité/session, profil, paramètres, organisation, navigation, pages publiques, états système, accessibilité, admin, divers, chaque item marqué [Universel] ou [Conditionnel]). Objectif : ne rien oublier de ce qui revient sur presque tout projet (paramètres, sécurité, tableau de bord, zone de danger, mode sombre...) avant de se concentrer sur ce qui est spécifique au métier. Le tri se fait à ce moment-là — ce qui est retenu part dans le brief, le reste est ignoré.

---

## Phase 1 — Cahier des charges

**Qui fait quoi :** Claude, à partir du brief.

**Prompt à utiliser :**
```
À partir de ce que je viens de décrire, rédige-moi un cahier des charges complet
(fonctionnel + annexe juridique/réglementaire locale si pertinent), en .docx.
```

Claude fait toujours une recherche web préalable pour tout élément réglementaire ou local avant de rédiger — jamais de référence juridique inventée. Ce document devient la référence produit, indépendante de l'outil de code qui sera choisi ensuite pour construire.

Pour chaque item retenu en Phase 0 depuis `pages-fonctionnalites-universelles.md`, Claude reprend son comportement par défaut dans `detail-fonctionnalites-universelles.md` (checklist niveau 2 — champs exacts, règles de validation, états à prévoir, cas limites) et l'intègre tel quel au cahier des charges, sauf si le brief ou une contrainte du projet dit explicitement autre chose — auquel cas c'est toujours cette exigence spécifique qui prime, jamais le défaut générique.

---

## Phase 2 — État du projet

**Qui fait quoi :** Claude, automatiquement — à condition que la conversation soit rattachée à une **Project** claude.ai.

Réflexe à prendre de ton côté : repartir systématiquement du même Project pour un projet donné, jamais d'une conversation isolée — c'est ce qui permet à Claude de retrouver tout l'historique même dans une session toute neuve.

Claude maintient de lui-même un document `claude/etat-du-projet.md` mis à jour à chaque jalon significatif : contexte, décisions actées, points ouverts, historique résumé, statut courant, prochaine étape critique. Ce document est toujours réécrit en entier à chaque mise à jour (pas de correctif partiel possible sur les docs de Project).

---

## Phase 3 — Prototype interactif de référence

**Qui fait quoi :** Claude, avec des allers-retours.

**Prompt à utiliser :**
```
Construis un prototype HTML interactif complet (un seul fichier autonome) qui simule
un outil de design : navigation entre tous les écrans du produit (site public + back-office/
admin le cas échéant), bascule Bureau/Mobile, données d'exemple réalistes reflétant la vraie
logique métier (jamais de lorem ipsum, jamais de valeurs identiques d'un item à l'autre), et
toutes les interactions réellement fonctionnelles en JS (formulaires multi-étapes, filtres
avec compteurs en direct, modales avec logique conditionnelle par état) — pas de maquette
statique.
```

Détails techniques utiles :
- Bascule Bureau/Mobile via une **container query** sur un conteneur `frame`, plutôt que de vraies media queries qui casseraient le chrome de l'outil de prototypage lui-même.
- Le conteneur simulant l'écran mobile doit être **borné en hauteur avec défilement interne** (comme un vrai téléphone), sinon les éléments en position fixe (barres de navigation, modales) dérivent vers le bas de toute la page au lieu de rester ancrés à l'écran visible.
- Republier via l'outil Artifact à chaque itération significative, en gardant le même lien.

### Phase 3bis — Boucle de correction

**Qui fait quoi :** toi, avec des captures d'écran.

Ce qui marche le mieux : une capture + des corrections **numérotées et précises**, chacune citant le libellé exact du texte/bouton concerné plutôt qu'une description vague ("le bouton X doit dire Y" plutôt que "corrige le bouton"). Regrouper plusieurs retours dans un même message plutôt que d'envoyer un message par micro-correction — Claude peut tout traiter d'un coup et confirmer par une nouvelle capture. Chaque correction est revérifiée (capture ou script de vérification) avant d'être considérée comme faite, puis republiée.

Si un état interactif précis manque d'exemple concret dans les données de démo (ex. un bouton qui ne s'affiche que dans un cas particulier), c'est aussi le moment de le signaler — la correction consiste alors à enrichir les données d'exemple pour couvrir cet état, pas à changer la logique.

---

## Phase 4 — Audit exhaustif (obligatoire, avant tout empaquetage)

**Qui fait quoi :** Claude, sur demande explicite — c'est l'étape la plus souvent oubliée ailleurs.

**Prompt à utiliser :**
```
Avant toute livraison, audite tout le prototype : relis tout le code (CSS + HTML + JS en
entier), teste chaque écran et chaque scénario interactif, en desktop ET en mobile. Zéro
erreur console tolérée. Corrige tout bug trouvé et revérifie avant de me dire que c'est bon.
```

Sans cette étape, des bugs réels (rendu cassé quand un écran n'est pas encore visible, valeur de champ non resynchronisée, mise en page mobile cassée) partent tels quels dans la construction réelle.

Pour les scripts de test (Playwright) dans ce type de prototype : bloquer tout trafic réseau non-`file://` (pour éviter qu'un lien externe comme "Se connecter avec Google" ne fasse planter le script), et scoper les sélecteurs à l'écran actif (`.screen.active ...`) quand plusieurs écrans coexistent cachés dans le DOM. Cette étape peut être déléguée à un agent dédié avec un brief très détaillé (architecture du prototype + scénarios précis à couvrir) pour ne pas saturer le contexte principal.

**Vérification supplémentaire, avant de considérer l'audit terminé : chasse aux écrans fantômes.** Relis chaque écran à la recherche de toute action attribuée à quelqu'un d'extérieur (un utilisateur, un tiers) qui suppose l'existence d'un support — un formulaire externe, un document, une page — sans que ce support n'ait lui-même été construit comme un écran du prototype. Le repérer ici, avant l'empaquetage, coûte une relecture ; le repérer seulement pendant la construction réelle coûte un aller-retour complet (maquette de rattrapage + captures + prompt dédié).

**Vérification symétrique : repérage des composants transverses.** À l'inverse d'un écran manquant, il s'agit ici de repérer ce qui n'est PAS un écran mais un élément présent sur (ou au-dessus de) toutes les pages : bandeau de cookies, centre de notifications, invite d'installation en PWA, chat de support flottant, etc. — un composant à documenter et prompter une seule fois, pas à répéter (ou oublier) dans chacun des prompts d'écran.

---

## Phase 5 — Empaquetage du dossier de référence design

**Qui fait quoi :** Claude, une fois le prototype stable et audité.

**Prompt à utiliser :**
```
Prépare le dossier de référence design complet pour [OUTIL DE CODE CHOISI] : document de
spécification écran par écran (valeurs exactes recopiées du code, jamais approximées),
captures systématiques desktop+mobile de chaque écran et état important, un guide
expliquant comment faire suivre ce design à la lettre par cet outil — en te renseignant
d'abord sur son comportement par défaut (compétences/skills embarquées) pour savoir
précisément quoi neutraliser plutôt que d'inventer un problème à contourner — et surtout
un prompt de lancement DÉJÀ ENTIÈREMENT RÉDIGÉ pour chacun des écrans listés dans la
spécification, prêt à copier-coller sans aucune adaptation. Chaque prompt d'écran doit
combiner, dans le même bloc, la partie design habituelle et un paragraphe "Comportement
backend attendu" propre à cet écran, précédés d'un unique prompt de fondations backend
(modèle de données complet de l'application) à coller une seule fois avant le premier écran.
```

Contenu du dossier livré :
- **`DESIGN-SPEC.md`** — une section par écran : Purpose / Screenshots / Layout & visual design (valeurs exactes) / Content (copy réelle) / Functional behavior / Différences mobile.
- **`screenshots/`** — captures desktop + mobile de chaque écran et de leurs états interactifs significatifs, toutes référencées depuis `DESIGN-SPEC.md` (vérifier l'absence de liens cassés ou orphelins avant livraison).
- **`[OUTIL]-PROMPTS.md`** — le guide méthode (voir Phase 6) : explique le principe, mais ne contient PAS lui-même les blocs à copier (voir règle d'or ci-dessous).
- **`prompt-1-claude-md.md`** — le prompt permanent, seul dans son fichier, prêt à coller une fois pour toutes.
- **`prompts-par-ecran/`** — `00-fondations-backend.md` en premier (modèle de données complet, une seule fois), puis un fichier par écran de `DESIGN-SPEC.md` (ex. `01-accueil.md`, `02-tableau-de-bord.md`…), chacun contenant le prompt de lancement déjà entièrement rédigé pour cet écran précis (nom de l'écran, section de la spec, numéros exacts des captures à regarder, PLUS son paragraphe "Comportement backend attendu") — zéro `[PLACEHOLDER]` à remplacer, zéro jugement à faire sur les bornes à copier. Un composant transverse repéré en Phase 4 (voir ci-dessus) y a droit à son propre fichier numéroté à la suite, écrit sur le même modèle, mais précisant explicitement qu'il ne s'agit pas d'un écran et sur quelles pages il doit apparaître.
- **`README.md`** — index du dossier.
- Le tout empaqueté en `.zip` et livré en fichier téléchargeable.

> **Règle d'or :** tout bloc destiné à être copié-collé tel quel doit vivre dans **son propre fichier, sans rien d'autre dedans** — pas de titre, pas de phrase d'explication avant ou après, pas d'exemple à côté qui pourrait être confondu avec le modèle. Dès qu'un bloc à copier est entouré de texte dans le même fichier (même avec des ``` autour), la frontière devient ambiguë en vue "texte brut" et des erreurs de copie silencieuses apparaissent (fragment manquant, ligne de bordure emportée par erreur). Un fichier = un seul bloc, prêt à l'usage, sélection = Ctrl+A.

---

## Phase 6 — Mise en place dans l'outil de code

**Qui fait quoi :** toi, une fois le dossier reçu.

Le dossier de la Phase 5 contient trois types de prompts, dans des fichiers séparés :

**1. Prompt permanent** (`prompt-1-claude-md.md`) — à coller dans le fichier de contexte persistant de l'outil (`CLAUDE.md` ou équivalent) **avant toute ligne de code**, jamais en réaction à un problème déjà constaté, et une seule fois. Il doit :
- Présenter le produit en un paragraphe.
- Pointer vers les fichiers de référence comme source de vérité **unique** (palette, typographie, layout, copy, comportement).
- Interdire explicitement à toute compétence de design par défaut de l'outil de proposer ses propres choix.
- Neutraliser explicitement toute compétence non pertinente identifiée en Phase 5.

**2. Prompt de fondations backend** (`prompts-par-ecran/00-fondations-backend.md`) — à coller une seule fois, en tout premier, avant le premier écran. Il définit le modèle de données complet de l'application (toutes les entités, tous écrans confondus) pour que chaque écran construit ensuite s'appuie dessus au lieu de réinventer sa propre variante à chaque fois.

**3. Prompts de lancement par écran** (`prompts-par-ecran/01-...` à `NN-...`) — un fichier déjà prêt par écran, à coller **en ouverture de la tâche correspondante** (pas à chaque message, une fois par écran). Chaque fichier combine la partie design (lecture du document + des captures concernées, confirmation de compréhension avant le code, implémentation stricte sans invention de variation de style) et un paragraphe "Comportement backend attendu" propre à cet écran, qui réutilise toujours le modèle défini en `00-fondations-backend.md` — sans qu'il y ait quoi que ce soit à adapter toi-même.

**Point important à ne pas rater :** l'outil de code ne va **pas** te demander ce prompt de lui-même — il n'y a pas d'étape ou de "phase" intégrée qui s'arrête et attend une description de l'écran. C'est **toi** qui déclenches chaque tâche d'écran en ouvrant un nouveau message — et c'est à ce moment précis, à chaque fois, que tu colles le fichier correspondant de `prompts-par-ecran/`.

---

## Phase 7 — Construction écran par écran

**Qui fait quoi :** toi, dans l'outil de code, avec le prompt de lancement de la Phase 6 collé au début de chaque nouvel écran ou reprise de session.

Commence toujours par coller `00-fondations-backend.md`, une seule fois, avant le premier écran.

Pour un projet à beaucoup d'écrans qui se ressemblent (ex. 50 fiches produit identiques dans leur structure), ne redemande pas le prompt de lancement 50 fois : construis et valide un seul gabarit avec le prompt complet, puis pour les suivants demande simplement "même gabarit que [écran validé], applique-le à [X]" — le design a déjà été tranché une fois, inutile de repartir de la spécification à chaque répétition.

Claude reste disponible pour ajuster `DESIGN-SPEC.md`, les captures ou les prompts par écran si un écart de design est découvert pendant la construction réelle — republier le zip si les changements s'accumulent plutôt qu'à chaque micro-ajustement.

**Si un écran fantôme apparaît pendant la construction** (l'outil de code signale qu'il lui manque un écran non documenté) : (1) Claude construit une maquette de cet écran en réutilisant exactement les mêmes variables de couleur/police déjà en place dans le prototype (jamais de nouvelles valeurs inventées), (2) la capture en desktop et mobile avec les numéros de capture suivants dans la continuité de la séquence existante, (3) écrit un nouveau fichier dans `prompts-par-ecran/` sur le même modèle que les autres (design + comportement backend dans le même bloc), référencé dans l'index. Un aller-retour, pas un blocage.

**Si un besoin de composant transverse apparaît en cours de route** (ex. bandeau de cookies, invite d'installation en PWA) plutôt qu'en Phase 4 : même traitement qu'un écran fantôme (maquette + capture + fichier dédié dans `prompts-par-ecran/`), mais le fichier obtenu se colle **une seule fois**, comme `00-fondations-backend.md`, et non en ouverture d'une tâche d'écran précise — puisqu'il s'applique à toutes les pages à la fois plutôt qu'à une seule.

### Phase 7bis — Audit backend final

**Qui fait quoi :** Claude, une fois tous les écrans (y compris tout écran fantôme découvert en cours de route) construits.

**Prompt à utiliser :**
```
Maintenant que tous les écrans sont construits, audite le backend dans son ensemble :
vérifie que les données circulent correctement d'un écran à l'autre (pas seulement que
chaque écran fonctionne isolément), que les permissions sont vérifiées sur CHAQUE action
d'écriture et pas seulement certaines, que les identifiants/tokens sensibles ne sont
jamais exposés en clair, et que le modèle de données défini dans 00-fondations-backend.md
n'a pas été dupliqué ou contredit par un écran construit plus tard. Corrige tout écart
trouvé et revérifie avant de me dire que c'est bon.
```

C'est le même principe que la Phase 4, mais appliqué au fonctionnement réel plutôt qu'à la fidélité visuelle — les deux audits sont complémentaires, ni l'un ni l'autre ne remplace l'autre.

---

## Résumé express

| Phase | Qui | Sortie |
|---|---|---|
| 0. Cadrage | Toi | Brief complet (+ tri dans `pages-fonctionnalites-universelles.md`) |
| 1. Cahier des charges | Claude | `.docx` (items retenus détaillés via `detail-fonctionnalites-universelles.md`) |
| 2. État du projet | Claude (auto) | `etat-du-projet.md` dans le Project |
| 3. Prototype interactif | Claude ↔ Toi | Artifact HTML navigable |
| 4. Audit exhaustif | Claude (sur demande explicite) | Prototype à zéro bug console |
| 5. Empaquetage | Claude | `.zip` : spec + captures + guide + `prompt-1-claude-md.md` + `prompts-par-ecran/` (`00-fondations-backend.md` + un fichier design+backend prêt-à-coller par écran) |
| 6. Mise en place | Toi | Prompt permanent collé une fois dans `CLAUDE.md` |
| 7. Construction | Toi, écran par écran | `00-fondations-backend.md` une fois, puis à chaque écran le fichier correspondant de `prompts-par-ecran/`, sans adaptation |
| 7bis. Audit backend final | Claude (sur demande explicite) | Backend vérifié bout en bout, une fois tous les écrans construits |
