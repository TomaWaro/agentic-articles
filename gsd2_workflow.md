# Workflow complet de la méthode GSD-2

## Introduction

GSD-2 est une méthode de développement logiciel moderne conçue pour
exploiter pleinement le potentiel des agents IA. Contrairement aux
approches classiques, elle repose sur une logique **spec-driven**, où
tout commence par une définition claire du besoin, suivie d'un cycle
autonome d'exécution.

L'objectif est simple : permettre à un agent de développer un projet de
manière continue, fiable et structurée, tout en gardant l'humain dans un
rôle de supervision.

------------------------------------------------------------------------

## Philosophie générale

La méthode GSD-2 s'appuie sur plusieurs principes fondamentaux :

-   **Spec-driven development** : chaque fonctionnalité est définie
    avant d'être développée
-   **Gestion du contexte** : l'information envoyée à l'agent est
    maîtrisée et optimisée
-   **Boucle autonome** : le système planifie, exécute, vérifie et
    corrige en continu
-   **Résilience** : le système peut reprendre après interruption

L'humain n'intervient plus dans le code directement, mais dans la
stratégie et les décisions.

------------------------------------------------------------------------

## Le workflow global

Le fonctionnement de GSD-2 repose sur une boucle principale qui se
répète jusqu'à complétion du projet :

**Research → Plan → Execute → Verify → Commit → Advance**

Chaque étape a un rôle précis et contribue à la robustesse du système.

------------------------------------------------------------------------

## 1. Définition des objectifs (Milestones et Slices)

Le travail commence par la définition d'un objectif appelé *milestone*.\
Ce milestone est ensuite découpé en petites unités appelées *slices*.

Une slice correspond à une tâche simple, testable et indépendante.\
Cette granularité permet à l'agent de progresser de manière fiable et
contrôlée.

------------------------------------------------------------------------

## 2. Phase de recherche (Research)

Avant d'agir, l'agent analyse son environnement :

-   exploration du code existant
-   compréhension des dépendances
-   identification des contraintes

Cette étape permet d'éviter les erreurs et les approximations. Elle
garantit que l'agent travaille avec un contexte pertinent.

------------------------------------------------------------------------

## 3. Phase de planification (Plan)

Une fois le contexte compris, l'agent construit un plan structuré :

-   liste des tâches à effectuer
-   ordre d'exécution
-   dépendances entre tâches
-   résultats attendus

Ce plan devient la référence principale pour la suite du processus.

------------------------------------------------------------------------

## 4. Phase d'exécution (Execute)

L'agent passe ensuite à l'action. Il implémente chaque slice une par une
:

-   création ou modification de fichiers
-   écriture de code
-   utilisation d'outils

Le travail est souvent isolé (par exemple via des worktrees Git) pour
éviter les conflits.

------------------------------------------------------------------------

## 5. Phase de vérification (Verify)

Chaque action est ensuite validée :

-   exécution de tests
-   vérification du comportement attendu
-   contrôle de cohérence

Si un problème est détecté, le système revient automatiquement en
arrière pour corriger.

C'est une étape clé qui garantit la qualité du résultat.

------------------------------------------------------------------------

## 6. Commit et persistance

Une fois validé, le travail est enregistré :

-   commit du code
-   mise à jour de l'état du projet

Toutes les informations sont stockées localement, ce qui permet de
reprendre le travail à tout moment.

------------------------------------------------------------------------

## 7. Avancement automatique (Advance)

Le système passe ensuite à la tâche suivante :

-   nouvelle slice
-   ou nouveau milestone

Le cycle recommence jusqu'à ce que tout soit terminé.

------------------------------------------------------------------------

## Rôle de l'humain

Dans GSD-2, le développeur devient un **chef d'orchestre** :

-   il définit les objectifs
-   il valide les décisions importantes
-   il surveille l'avancement

Des commandes permettent d'interagir avec le système :

-   consulter le statut
-   discuter avec l'agent
-   ajouter du travail

------------------------------------------------------------------------

## Concepts clés

-   **Slices** : unités de travail élémentaires\
-   **Milestones** : regroupements de slices\
-   **State machine** : gestion des états du projet\
-   **Stockage local** : persistance complète dans `.gsd/`

------------------------------------------------------------------------

## Conclusion

GSD-2 transforme profondément la manière de développer :

-   le développeur se concentre sur le **quoi**
-   l'agent gère le **comment**
-   le système s'auto-corrige en continu

C'est une approche orientée automatisation, fiabilité et scalabilité,
particulièrement adaptée aux projets pilotés par IA.
