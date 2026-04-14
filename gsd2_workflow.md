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

## Token optimisation

L’un des apports majeurs de GSD-2 par rapport aux approches classiques d’agents est sa gestion proactive du coût et du contexte. Là où la plupart des systèmes subissent le problème du “context rot” ou explosent en tokens, GSD-2 introduit une stratégie coordonnée qui permet de réduire drastiquement la consommation tout en maintenant la qualité.

Concrètement, le système de token optimisation repose sur trois piliers complémentaires : les token profiles, la compression de contexte et le routage dynamique basé sur la complexité des tâches.

Le concept central est celui de token profile. Plutôt que de régler manuellement chaque paramètre (modèle, phases, taille du contexte…), GSD propose un simple levier de configuration qui orchestre automatiquement l’ensemble. Ce profil va déterminer quels modèles sont utilisés, quelles étapes du workflow sont exécutées ou ignorées, et surtout combien de contexte est injecté dans chaque appel au modèle.

Trois profils principaux structurent cette logique.

Le mode budget pousse l’optimisation au maximum. Il réduit agressivement le contexte, supprime certaines phases comme la recherche intermédiaire, et privilégie des modèles plus légers. C’est le mode idéal pour itérer rapidement sur un projet déjà compris, ou pour explorer des idées à faible coût.

Le mode balanced, activé par défaut, représente un compromis intelligent. Il conserve les étapes importantes du workflow tout en éliminant celles dont le retour sur investissement est faible. Le contexte reste suffisamment riche pour produire des résultats fiables, sans tomber dans l’excès.

Enfin, le mode quality adopte l’approche inverse : aucune compression, aucune simplification. Tout le contexte est injecté, toutes les phases sont exécutées. Ce mode est particulièrement adapté aux tâches complexes, aux refactorings profonds ou aux projets critiques où chaque détail compte.

Cette logique est renforcée par un second mécanisme : la compression de contexte. Selon le profil choisi, GSD va décider de ne transmettre que l’essentiel (plan, résumés récents) ou au contraire d’inclure l’intégralité des artefacts (décisions, exigences, historique complet).
L’idée est simple : envoyer moins d’information… mais mieux sélectionnée.

Enfin, GSD ajoute une couche d’intelligence avec le complexity-based routing. Chaque tâche est automatiquement analysée (nombre d’étapes, fichiers impliqués, nature du travail) puis routée vers le bon niveau de modèle. Une correction triviale n’utilise pas les mêmes ressources qu’une refonte d’architecture.

Résultat : une réduction typique de 40 à 60 % des tokens consommés, sans perte notable de qualité dans la majorité des cas.

Ce n’est pas simplement une optimisation technique, c’est un changement de paradigme : le coût devient une variable pilotée par le système, et non plus une contrainte subie.

------------------------------------------------------------------------

## Différences fondamentales avec la V1

Pour comprendre GSD-2, il faut d’abord accepter que ce n’est pas une simple évolution de la V1. C’est une refonte complète de la manière dont un agent structure son travail, son contexte et sa mémoire.

La V1 reposait principalement sur un ensemble de prompts statiques, installés localement et exécutés de manière relativement linéaire. Chaque étape dépendait fortement du contexte accumulé dans la session, ce qui entraînait rapidement des dérives : perte de cohérence, répétitions, ou décisions oubliées.

GSD-2 prend le contre-pied total de cette approche.

La première différence majeure est le passage d’un système de prompts à un système orchestré. Au lieu d’une simple séquence d’instructions, GSD-2 fonctionne comme un pipeline structuré, avec des phases clairement définies (planning, exécution, vérification, etc.) et un moteur de dispatch qui décide dynamiquement quoi exécuter.

Ensuite, la gestion du contexte n’est plus implicite mais explicitement modélisée. Là où la V1 accumulait du contexte de manière passive, GSD-2 le reconstruit en permanence : résumés, artefacts, décisions et plans sont organisés, compressés et réinjectés de façon contrôlée. Cela permet de maintenir une vision cohérente du projet, même sur des sessions longues.

Autre rupture importante : l’introduction du routage dynamique des modèles. En V1, un seul modèle était généralement utilisé pour tout. En V2, chaque tâche peut être confiée à un modèle différent en fonction de sa complexité. Cela permet d’allouer intelligemment les ressources, plutôt que de surdimensionner ou sous-exploiter le système.

GSD-2 introduit également une logique de phases adaptatives. Certaines étapes du workflow peuvent être ignorées si elles n’apportent pas de valeur dans un contexte donné. Ce comportement, piloté notamment par les token profiles, permet d’éviter le sur-traitement qui était fréquent en V1.

Enfin, la V2 intègre nativement des concepts absents ou implicites auparavant : gestion des coûts, orchestration parallèle, isolation des tâches, et capacité à travailler sur des projets longs sans dégradation progressive.

En résumé, là où la V1 était une boîte à prompts bien organisée, GSD-2 est un véritable système d’exécution autonome.
Ce n’est plus simplement un outil pour générer du code — c’est une architecture pour piloter des agents sur la durée, avec cohérence, efficacité et contrôle.

## Conclusion

GSD-2 transforme profondément la manière de développer :

-   le développeur se concentre sur le **quoi**
-   l'agent gère le **comment**
-   le système s'auto-corrige en continu

C'est une approche orientée automatisation, fiabilité et scalabilité,
particulièrement adaptée aux projets pilotés par IA.
