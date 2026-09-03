# Pages, menus et fonctionnalités universels — base réutilisable

> Checklist à consulter en Phase 0 (Cadrage) ou Phase 1 (Cahier des charges) de la méthode `methode-projet-design-reference.md`, sur n'importe quel projet. Elle ne remplace jamais le cahier des charges du projet — elle sert juste à ne rien oublier de ce qui revient presque partout, avant de se concentrer sur ce qui est spécifique au métier. Tri à faire à chaque projet : garder ce qui s'applique, jeter le reste.

Deux étiquettes utilisées :
- **[Universel]** — quasiment toujours présent, quel que soit le type d'app.
- **[Conditionnel]** — seulement si le projet a la caractéristique indiquée (paiement, multi-utilisateurs, etc.).

---

## A. Identité & session

- Connexion / Login **[Universel]**
- Inscription / Sign up **[Universel]** (sauf app 100% invitation-only)
- Mot de passe oublié → réinitialisation **[Universel]**
- Vérification email ou téléphone (code OTP) **[Universel]**
- Connexion via un tiers (Google, Apple, etc.) **[Conditionnel]**
- Authentification à deux facteurs — activation + codes de secours **[Universel dès qu'il y a des données sensibles]**
- Déconnexion — de cet appareil, ou de tous les appareils d'un coup **[Universel]**
- Onboarding / première configuration après inscription **[Conditionnel — utile si l'app demande une config avant d'être utile]**

## B. Profil utilisateur

- Informations personnelles (nom, photo, bio, coordonnées) **[Universel]**
- Changer l'email / le téléphone **[Universel]**
- Changer le mot de passe **[Universel]**
- Préférences de communication (accepter/refuser certains types de contact) **[Conditionnel]**

## C. Paramètres (souvent en sous-onglets)

- **Général** : langue, fuseau horaire, région, format date/devise **[Universel si l'app a une portée internationale, sinon allégé]**
- **Apparence / Affichage** : thème clair / sombre / système, densité d'affichage, taille de police, couleur d'accent **[Universel — le mode sombre en particulier est quasi standard aujourd'hui]**
- **Notifications** : par canal (email, push, in-app, SMS) et par type d'événement, avec fréquence/digest **[Universel dès qu'il y a des notifications]**
- **Confidentialité** : visibilité du profil, partage de données **[Conditionnel — selon si le profil est visible par d'autres]**
- **Sécurité** : **[Universel]**
  - Mot de passe
  - 2FA / clés de sécurité
  - Sessions actives / appareils connectés — voir et révoquer chaque session
  - Historique de connexion (date, IP, appareil)
  - Clés API / tokens d'accès **[Conditionnel — si l'app a une API]**
- **Facturation / Abonnement** **[Conditionnel — modèle payant]** :
  - Plan actuel, changement de plan
  - Moyens de paiement
  - Historique des factures / reçus
  - Utilisation / quotas consommés
- **Intégrations connectées** (comptes tiers liés, apps autorisées) **[Conditionnel]**
- **Zone de danger** **[Universel]** :
  - Exporter mes données
  - Désactiver le compte (réversible)
  - Supprimer le compte (définitif — confirmation forte, ex. retaper son email/mot de passe)

## D. Espace de travail / organisation **[Conditionnel — dès que l'app est multi-utilisateurs ou multi-tenant]**

- Membres de l'équipe : liste, inviter, retirer
- Rôles & permissions
- Paramètres de l'organisation (nom, logo, domaine personnalisé)
- Facturation au niveau de l'organisation (plutôt qu'individuelle)

## E. Navigation générale & structure

- Tableau de bord / accueil connecté — vue d'ensemble, résumé, raccourcis **[Universel — tu as raison, ça traverse presque tous les projets]**
- Barre de recherche globale **[Conditionnel — utile dès qu'il y a beaucoup de contenu]**
- Centre de notifications (cloche + badge) **[Universel dès qu'il y a des notifications]**
- Menu utilisateur (avatar → accès rapide profil / paramètres / déconnexion) **[Universel]**
- Aide / support (centre d'aide, FAQ, contact, chat) **[Universel]**
- Nouveautés / changelog (souvent un badge "nouveau") **[Conditionnel]**
- Fil d'Ariane (breadcrumb) sur les pages profondes **[Conditionnel — utile dès 3 niveaux de navigation ou plus]**
- Palette de commandes / raccourcis clavier (type ⌘K) **[Conditionnel — apps productivité]**

## F. Pages publiques transversales (avant connexion)

- Accueil / landing **[Universel]**
- Tarifs **[Conditionnel — modèle payant]**
- À propos **[Universel]**
- Contact **[Universel]**
- Blog / actualités **[Conditionnel]**
- Mentions légales **[Universel]**
- CGU / CGV **[Universel]**
- Politique de confidentialité **[Universel]**
- Politique de cookies + bandeau de consentement **[Universel si trafic international / soumis au RGPD ou équivalent]**
- FAQ publique **[Conditionnel]**

## G. États système & pages techniques

- Page 404 (introuvable) **[Universel]**
- Page 500 / erreur serveur **[Universel]**
- Page de maintenance **[Universel]**
- Accès refusé / 403 **[Universel dès qu'il y a des permissions]**
- État vide (empty state) pour chaque liste/tableau important **[Universel]**
- Chargement / squelettes (skeleton loaders) **[Universel]**

## H. Accessibilité & confort d'usage

- Mode sombre / clair / système **[Universel]**
- Taille de police / contraste élevé **[Conditionnel — recommandé si public large ou institutionnel]**
- Navigation clavier / lecteur d'écran **[Universel dans l'esprit, même si l'implémentation varie]**

## I. Back-office / admin **[Conditionnel — dès que l'app a une équipe interne qui gère des données]**

- Tableau de bord admin (métriques transversales)
- Gestion des utilisateurs (liste, recherche, suspendre, supprimer)
- Gestion des rôles/permissions
- Journal d'audit (qui a fait quoi, quand)
- Paramètres globaux de la plateforme
- Modération de contenu **[Conditionnel — si contenu généré par les utilisateurs]**

## J. Autres transverses souvent oubliés

- Import / export de données (CSV, PDF) **[Conditionnel]**
- Filtres et recherches sauvegardés **[Conditionnel]**
- Multi-langue **[Conditionnel — cible internationale]**
- Mode hors-ligne / PWA **[Conditionnel — usage mobile-first]**
- API publique + documentation, webhooks **[Conditionnel — plateforme technique]**

---

## Comment s'en servir

En Phase 0/1 d'un nouveau projet : parcourir les 10 sections, cocher ce qui s'applique compte tenu du modèle du projet (payant ou non, multi-utilisateurs ou non, back-office ou non, portée internationale ou non), et ajouter la sélection retenue au brief avant de passer au cahier des charges. Rien ici n'est à copier tel quel dans une spec — c'est une liste de vérification, pas un gabarit de contenu.

Prochaine étape, à ta demande : détailler chaque fonctionnalité retenue (comportement exact, champs, règles) pour l'optimiser avant de l'intégrer au projet en cours.
