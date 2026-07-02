# Test technique – Add-on Shopper

## Contexte

[Shopper](https://github.com/shopperlabs/shopper) est un panneau d'administration e-commerce headless pour Laravel, construit avec la TALL stack (Tailwind CSS, Alpine.js, Laravel, Livewire) et Filament. Il s'étend via un système d'add-ons.

Votre mission : développer un add-on complet pour Shopper, distribué comme package Composer indépendant, en vous appuyant sur la documentation officielle et le code source du projet.

## Objectif

Réaliser un add-on fonctionnel qui :

- S'installe via Composer dans un projet Laravel où Shopper (`shopper/framework`) est installé.
- S'enregistre via le système d'add-ons de Shopper et peut être activé ou désactivé par configuration.
- Déclare ses propres migrations, routes et pages d'administration.
- Ajoute sa propre entrée dans la navigation de l'admin.
- Expose au moins un composant que le développeur final peut surcharger dans son application.
- Respecte les conventions de code du projet Shopper.

## Choix de l'add-on

Choisissez un ou plusieurs add-ons parmi les suivants. Chaque add-on a un niveau de difficulté ; votre score global est la somme des niveaux des add-ons implémentés.

| # | Add-on | Ce qui doit exister à la fin | Niveau |
|---|--------|------------------------------|--------|
| 1 | **Blog** | Articles et catégories : CRUD complet dans l'admin, statut brouillon/publié, date de publication, association d'une image de couverture. | 4/10 |
| 2 | **FAQ** | Questions/réponses organisées par groupes : CRUD dans l'admin, réordonnancement des questions, activation/désactivation individuelle. | 3/10 |
| 3 | **Newsletter** | Gestion des abonnés : inscription et désinscription via API, liste des abonnés dans l'admin avec recherche et filtres, export CSV. | 3/10 |
| 4 | **Flux produits** | Export du catalogue au format Google Shopping (XML) : mapping des produits, prix et stocks du core, régénération planifiée du flux, page admin de configuration et de prévisualisation. | 5/10 |
| 5 | **Alertes de retour en stock** | Souscriptions d'alertes sur des produits : notification automatique des clients inscrits quand le stock redevient disponible, vue admin des souscriptions en attente. | 6/10 |

**Total maximum : 21 points.**

## Exigences techniques

| Domaine | Attendu |
|---------|---------|
| PHP | 8.3 minimum, `declare(strict_types=1)` dans chaque fichier |
| Laravel | 13.x |
| Admin | Livewire + Filament (schemas/tables), cohérent avec les pages existantes de Shopper |
| Base de données | Migrations versionnées, rollback fonctionnel |
| PHPStan | Niveau 6 minimum avec Larastan, zéro erreur |
| Laravel Pint | Configuration alignée sur celle de Shopper, zéro violation |
| Rector | Configuré, dry-run sans changement au moment de la soumission |
| Tests | Pest, syntaxe `it()` : chaque route, action métier et la surcharge de composant doivent être couvertes |

## Guide d'utilisation

1. Créez un nouveau projet Laravel 13 en local.
2. Installez Shopper (`shopper/framework`) en suivant la [documentation officielle](https://docs.shopperlabs.com).
3. Créez un dépôt Git dédié pour votre add-on : il vit dans son propre dépôt et s'installe par-dessus une installation standard de Shopper. Aucun fork de Shopper n'est accepté.
4. Développez l'add-on choisi en respectant les exigences techniques ci-dessus. La documentation et le code source de Shopper sont vos seules références : aucune assistance ne sera fournie sur le fonctionnement interne du framework.
5. Documentez et vérifiez votre travail au fur et à mesure (tests, PHPStan, Pint, Rector).

## Guide de commit

Votre historique Git fait partie de l'évaluation. Il doit raconter la progression du travail, pas arriver en un seul commit final.

- Format [Conventional Commits](https://www.conventionalcommits.org/) : `type(scope): description`.
- Types autorisés : `feat`, `fix`, `test`, `docs`, `chore`, `refactor`.
- Sujet à l'impératif, en anglais, 50 caractères maximum, sans point final.
- Un commit = un changement cohérent. Pas de commit fourre-tout du type `wip` ou `updates`.

Exemples :

```
feat(faq): add question group model and migration
feat(faq): register addon and sidebar entry
test(faq): cover question reordering
docs: add installation and override instructions
```

## Livrables

- Dépôt Git (public, ou privé avec invitation), taggé `v1.0.0`.
- `README.md` : prérequis, installation, configuration, utilisation, comment surcharger le composant exposé, comment lancer les tests et les outils d'analyse.
- `REPORT.md` : sorties de PHPStan, Pint, Rector et des tests.

## Soumission

1. Vérifiez que le tag `v1.0.0` pointe sur votre version finale.
2. Si votre dépôt est privé, invitez [@mckenziearts](https://github.com/mckenziearts) en lecture.
3. Envoyez le lien du dépôt pour vérification.

## Notation (sur 10, par add-on)

| Critère | Points |
|---------|--------|
| Intégration au système d'add-ons (enregistrement, activation/désactivation, navigation) | 2 |
| Architecture et complétude fonctionnelle de l'add-on | 3 |
| Qualité du code (conventions Shopper, PHPStan, Pint, Rector) | 2 |
| Tests | 2 |
| Documentation | 1 |
