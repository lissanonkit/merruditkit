# Détail des fonctionnalités universelles

> Niveau 2 de la checklist `pages-fonctionnalites-universelles.md` : pour chaque item retenu, le comportement fonctionnel précis à prévoir — champs, règles, états, cas limites. Toujours générique et réutilisable d'un projet à l'autre ; ne touche à rien du cahier des charges propre à un projet donné, qui reste à écrire à part et prime toujours sur ce document en cas de contradiction.

---

## A. Identité & session

**Connexion**
- Champs : identifiant (email ou téléphone selon le projet) + mot de passe, case "Se souvenir de moi", lien "Mot de passe oublié".
- Erreur d'identifiants : message générique ("identifiant ou mot de passe incorrect"), jamais préciser lequel des deux est faux — évite de révéler qu'un compte existe.
- Protection : verrouillage temporaire après un nombre d'essais échoués (ex. 5), délai croissant ou captcha ensuite.
- États à prévoir : chargement, erreur réseau (distincte de l'erreur d'identifiants).

**Inscription**
- Champs : email/téléphone, mot de passe (+ indicateur de force en direct), case CGU (décochée par défaut).
- Mot de passe : règle minimale affichée pendant la saisie (longueur, complexité), jamais découverte seulement après soumission.
- Email déjà utilisé : décider si le message le révèle explicitement ou reste neutre (compromis sécurité/UX à trancher par projet).
- Suite : envoi d'un lien/code de vérification, compte en état "non vérifié" tant que l'étape n'est pas passée.

**Mot de passe oublié**
- Étape 1 (saisie identifiant) → message neutre systématique ("si ce compte existe, un lien a été envoyé"), qu'il existe ou non.
- Lien de réinitialisation à durée de vie limitée (ex. 1h), usage unique.
- Après changement : déconnexion automatique de toutes les autres sessions actives.

**Vérification par code (OTP)**
- Code à 6 chiffres, expiration courte (ex. 10 min), renvoi possible après un délai visible (compte à rebours).
- Nombre de tentatives limité avant blocage temporaire du code.

**Authentification à deux facteurs**
- Activation : QR code + confirmation par un premier code saisi (jamais activé sans vérifier que l'app est bien configurée).
- Codes de secours à usage unique, téléchargeables, régénérables à la demande.
- Désactivation : toujours protégée par un second facteur (mot de passe ou code), jamais en un clic.

**Déconnexion**
- Distinguer "déconnecter cet appareil" (action courante) de "déconnecter tous les appareils" (action séparée, dans Sécurité, avec confirmation).

**Onboarding**
- 3 à 5 étapes maximum, progression visible, option de sortie à tout moment — ne jamais bloquer l'accès au produit sans échappatoire.

---

## B. Profil utilisateur

- Champs standards : photo (upload + recadrage), nom/prénom, bio courte, coordonnées.
- Sauvegarde explicite (bouton "Enregistrer") par défaut ; un auto-save silencieux doit toujours afficher un indicateur clair ("Enregistré à 14:32").
- Changement d'email : exige une nouvelle vérification avant que le changement soit effectif (l'ancien reste actif entre-temps).
- Changement de mot de passe : demande le mot de passe actuel, jamais un changement libre sans re-authentification.

---

## C. Paramètres

**Général** — langue (liste des langues supportées), fuseau horaire (détecté automatiquement, modifiable), format date/devise.

**Apparence** — thème Clair / Sombre / Système (toujours 3 options, jamais 2) ; "Système" doit suivre le thème du système en direct, sans recharger la page. Densité d'affichage et taille de police si l'accessibilité est un objectif du projet.

**Notifications** — matrice canal (email/push/in-app/SMS) × type d'événement, avec fréquence par item (immédiat / résumé quotidien / hebdomadaire). Un raccourci "tout désactiver" existe, mais les notifications de sécurité critiques (connexion suspecte, changement de mot de passe) restent obligatoires et ne peuvent pas être coupées.

**Confidentialité** — visibilité du profil si applicable, consentements marketing distincts du consentement CGU (jamais fusionnés dans une seule case).

**Sécurité**
- Sessions actives : liste avec appareil, navigateur, localisation approximative, dernière activité ; bouton "Révoquer" par ligne + "Révoquer toutes sauf celle-ci".
- Historique de connexion : date, IP, résultat (succès/échec), appareil.
- Clés API/tokens (si applicable) : nom, portée (scope) choisie à la création, secret affiché une seule fois puis masqué définitivement, révocation individuelle.

**Facturation** (si modèle payant)
- Plan actuel avec quotas/limites visibles ; changement de plan : upgrade immédiat, downgrade différé à la fin de la période en cours.
- Moyens de paiement : jamais stocker le numéro complet en base, passer par un prestataire de paiement ; ajout/suppression/moyen par défaut.
- Factures : liste téléchargeable en PDF (numéro, date, montant, statut).

**Intégrations connectées** — liste des apps tierces autorisées, date et portée de l'autorisation, révocation individuelle.

**Zone de danger**
- Export de données : traitement asynchrone si le volume est grand, notification quand le fichier est prêt plutôt qu'un téléchargement instantané forcé.
- Désactivation de compte : réversible, explique clairement ce qui change (profil masqué, reconnexion possible).
- Suppression de compte : irréversible, confirmation forte (retaper l'email ou un mot précis), rappel explicite de ce qui sera perdu ; un délai de grâce avant suppression définitive est une bonne pratique courante.

---

## D. Organisation / équipe (si multi-utilisateurs)

- Liste des membres : nom, rôle, statut (actif / invitation en attente), date d'ajout.
- Invitation par email avec rôle pré-assigné et lien à expiration.
- Rôles minimum : Propriétaire / Admin / Membre — avec une matrice de permissions explicite et consultable, pas seulement décidée au niveau du code.
- Transfert de propriété : action distincte, jamais implicite, avec confirmation des deux parties si possible.

---

## E. Navigation générale

- Tableau de bord : quelques indicateurs clés + raccourcis vers les actions fréquentes ; jamais vide au tout premier chargement — données d'exemple ou état d'accueil guidé pour un compte neuf.
- Recherche globale : résultats groupés par type de contenu, raccourci clavier standard.
- Centre de notifications : liste chronologique, marquage lu/non lu individuel et en masse.
- Menu utilisateur : avatar + accès rapide profil/paramètres/déconnexion, accessible depuis toutes les pages sans exception.

---

## F. Pages publiques

**Accueil / Landing page**
- Header : logo, navigation principale, CTA prioritaire (un seul mis en avant visuellement — "S'inscrire", "Commencer un dossier", etc. selon le projet), souvent sticky au scroll.
- Hero : une proposition de valeur en une phrase (ce que fait le produit / service, pour qui), un sous-titre qui explique comment, un CTA principal (+ un CTA secondaire discret si besoin, ex. "En savoir plus").
- Corps de page : 3 à 6 blocs maximum qui répondent chacun à une question du visiteur — jamais une liste illimitée de fonctionnalités. Si le produit repose sur un processus (dossier, commande, inscription en plusieurs étapes), une section "Comment ça marche" en étapes numérotées aide beaucoup et vaut mieux qu'un mur de texte.
- Preuve de confiance : selon le projet, témoignages, chiffres clés, logos partenaires/institutionnels, ou pour un site institutionnel une mention claire de légitimité/indépendance — l'équivalent fonctionnel change, le rôle (rassurer avant l'action) reste le même.
- FAQ courte en bas de page si des objections reviennent souvent, plutôt que de les laisser sans réponse.
- Footer : liens légaux (mentions, CGU, confidentialité), navigation secondaire, contact, réseaux sociaux si pertinent, copyright.
- Deux profils très différents à trancher explicitement dans le cahier des charges du projet, jamais par défaut :
  - **Landing marketing** (produit commercial) : orientée conversion, CTA répété à plusieurs endroits de la page, tarifs visibles, comparatif concurrentiel possible.
  - **Page d'accueil institutionnelle** (service public, associatif, administratif — comme Educ Bénin) : orientée information + confiance plutôt que conversion agressive, ton sobre, met en avant la légitimité et la clarté du processus, coordonnées de contact bien visibles, un seul CTA clair sans relance insistante.
- Mobile : navigation en menu (burger ou équivalent), hero simplifié à l'essentiel (titre + CTA visibles sans scroller), blocs de contenu qui s'empilent en respectant le même ordre de priorité qu'en desktop.
- Technique : titre de page et meta-description descriptifs (c'est la page la plus indexée et la plus partagée du site), image de partage (Open Graph), temps de chargement soigné en priorité sur cette page précise.

- Contenu institutionnel (mentions, CGU, confidentialité) : dater explicitement chaque page ("dernière mise à jour le...").
- Formulaire de contact : champs minimum (nom, email, message), protection anti-spam, confirmation d'envoi visible.
- Bandeau cookies : options Accepter / Refuser / Personnaliser toutes au même niveau visuel — jamais un simple "OK" qui fait office d'acceptation totale sans possibilité de refuser.

---

## G. États système

- 404 : message clair + lien de retour, jamais une page blanche.
- 500 : message rassurant, sans exposer de détail technique (trace d'erreur) à l'utilisateur final.
- Maintenance : durée estimée si connue.
- État vide : toujours accompagné d'une action possible ("créer le premier élément"), jamais un simple "aucune donnée" qui ne mène nulle part.
- Chargement : squelette qui respecte la forme du contenu final plutôt qu'un spinner générique, surtout sur les listes et tableaux.

---

## H. Accessibilité

- Contraste conforme dans les deux thèmes (clair et sombre).
- Tout élément interactif atteignable au clavier, dans un ordre de tabulation logique.
- Texte alternatif sur toute image porteuse de sens (pas sur les images purement décoratives).

---

## I. Back-office / admin

- Gestion des utilisateurs : recherche, filtres (statut, rôle, date d'inscription), actions en masse, suspension avec motif enregistré.
- Journal d'audit : qui, quoi, quand (et avant/après si pertinent) — non modifiable une fois écrit, conservé sur une durée définie par le projet.
- Paramètres globaux de la plateforme : changements sensibles confirmés et horodatés, attribués à l'admin qui les a faits.

---

## J. Autres transverses

- Export CSV/PDF : toujours filtré selon la vue courante affichée, jamais un "tout exporter" aveugle qui ignore les filtres actifs.
- Multi-langue : prévoir un texte de repli si une traduction manque, jamais une clé technique brute affichée à l'utilisateur.
- API/webhooks : documentation à jour avec exemples de requêtes, codes d'erreur explicites.

---

## Comment s'en servir

Pour un écran donné, une fois qu'on sait (via la checklist niveau 1) qu'il est retenu pour le projet, cette fiche donne le comportement par défaut à appliquer sauf si le cahier des charges du projet dit explicitement autre chose. En cas de désaccord entre les deux, le cahier des charges du projet gagne toujours — ce document ne fait que combler les détails qu'on oublie souvent de spécifier.
