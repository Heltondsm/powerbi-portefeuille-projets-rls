# Suivi de 104 projets dans 52 pays — Power BI

Trois niveaux de direction, un seul rapport : chacun voit son périmètre et reçoit une alerte
dès qu'un projet dérape de plus de 15 % sur les coûts, les délais ou les livrables.

![Vue globale](captures/02-vue-globale.png)

---

## Le problème à résoudre

La demande, posée par la responsable du bureau de gestion de projets : rendre les données
des projets lisibles par les directeurs, et en dégager des axes d'amélioration.
Le portefeuille couvre 4 régions, avec deux familles de projets indépendantes : 6 phases pour
l'IT (A à F), 4 phases pour le Marketing (1 à 4).

Trois profils d'utilisateurs, trois périmètres :

| Rôle | Ce qu'il voit |
|---|---|
| Directeur Général | Tous les projets, toutes régions |
| Directeur Régional | Uniquement les projets de sa région |
| Directeur Pays | Uniquement les projets de son pays |

## Les trois choix qui structurent le rapport

**La sécurité est appliquée à la connexion, pas par un filtre.** Le rapport utilise la sécurité
au niveau des lignes, ou RLS pour *row-level security* : les données affichées dépendent de
l'identité de l'utilisateur, qui ne peut pas élargir son périmètre en retirant un filtre.
Trois rôles sont définis, un par niveau de direction.

**Un seuil d'alerte unique, trois indicateurs.** Un projet passe en alerte dès que l'écart entre
le prévu et le réel dépasse **15 %** sur les coûts, les durées ou les livrables. Un seul code
couleur sur tout le rapport : vert sous 10 %, orange entre 10 et 15 %, rouge au-delà.

**Le rapport se lit sans mode d'emploi, et il en fournit un quand même.** Un onglet entier
documente les indicateurs, le système d'alerte, le filtrage, les accès par rôle et la procédure
de mise à jour en 5 étapes, pour que le rapport survive à son auteur.

**Deux éléments étaient optionnels dans le cahier des charges, ils sont livrés :** le diagramme
de Gantt et les infobulles enrichies.

## Les 9 onglets

| # | Onglet | Contenu |
|---|---|---|
| 1 | [Accueil](captures/01-accueil.png) | Navigation par boutons, volumétrie du portefeuille |
| 2 | [Vue Globale](captures/02-vue-globale.png) | Carte mondiale par statut, projets en alerte, écarts coûts et délais |
| 3 | [Budget](captures/03-budget.png) | Prévu contre réel par pays, écart budgétaire par phase |
| 4 | [Délais](captures/04-delais.png) | Diagramme de Gantt par phase, retard par phase |
| 5 | [IT vs Marketing](captures/05-it-vs-marketing.png) | Alertes par pays et par région, comparaison des deux familles |
| 6 | [Axe d'amélioration](captures/06-axe-amelioration.png) | Constats, recommandations, impact attendu |
| 7 | [Modèle des données](captures/07-modele-donnees.png) | Le schéma en étoile documenté |
| 8 | [Guide d'utilisation](captures/08-guide-utilisation.png) | Indicateurs, alertes, filtres, rôles, procédure de mise à jour |
| 9 | [Mise à jour](captures/09-mise-a-jour.png) | Product Strategy Canvas et les 9 user stories d'origine |

Une page dédiée alimente les [infobulles de la carte](captures/10-infocarte.png) : pays,
score de retard et nombre de projets en alerte au survol.

## Ce que les données disent

- **32 projets en alerte sur 104**, soit 30,8 % du portefeuille
- **56,11 M$ de budget prévu** contre **60,2 M$ dépensés**
- **Phase D — Testing : +401,3 % d'écart budgétaire.** Dépassement massif et isolé : la phase
  suivante la plus dégradée est à +19 %
- **La région CEMEA concentre 19 des 32 alertes**, dont 12 projets Marketing
- Côté familles : **19 alertes Marketing (59 %) contre 13 IT (41 %)**
- Sur les 52 pays : 25 sous contrôle, 23 en alerte, 4 à surveiller

## Ce qu'on en fait

L'onglet Axe d'amélioration ne s'arrête pas au constat. Il propose trois actions chiffrées :
un audit d'urgence de la Phase D avec blocage des dépenses non validées au-delà de +50 %,
un point mensuel obligatoire en région CEMEA avec un seuil d'alerte interne abaissé à 10 %,
et un réalignement des enveloppes Marketing sur les livrables réellement produits.
Objectif affiché : **ramener le taux d'alertes de 30,8 % à moins de 15 %**.

![Axe d'amélioration](captures/06-axe-amelioration.png)

## Comment les données sont organisées

**7 tables sources** issues d'un fichier Excel, organisées en étoile autour de `Projects_plans`
(clé `Project_ID` + `Project_phase`).

- Liées directement à la table centrale : `Actual_Costs`, `Actual_Duration`, `Actual_Delivrable`
  via `Project_phase`, et `Projects_Locations` via `Project_ID`
- Liées via `Projects_Locations` : `Country_Profiles` via `Country`, `Project type` via `Project_ID`
- Une table `Mesures` regroupe les calculs DAX : pourcentage de projets en alerte, couleur
  d'alerte globale, couleur coûts, couleur durées

![Modèle des données](captures/07-modele-donnees.png)

## Outils et techniques

Power BI Desktop · DAX · Power Query · modèle en étoile · sécurité au niveau des lignes ·
visuel personnalisé (diagramme de Gantt) · page d'infobulle

## Contenu du dépôt

```
captures/                              une image par onglet
suivi-projets-sanitoral.pbix     le rapport, ouvrable dans Power BI Desktop
```

## D'où vient ce projet

Projet réalisé dans le cadre du parcours Data Analyst d'OpenClassrooms, validé en mai 2026.
Sanitoral est une entreprise fictive : les données sont un jeu pédagogique, aucune donnée
réelle n'est publiée ici.

---

**Helton Dos Santos Moreira** · [LinkedIn](https://linkedin.com/in/helton-dsm-data) · [GitHub](https://github.com/Heltondsm)
