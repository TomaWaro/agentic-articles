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

L’un des apports les plus structurants de GSD-2 est sa manière de traiter les tokens comme une ressource stratégique. Là où beaucoup d’agents se contentent d’empiler du contexte jusqu’à atteindre les limites du modèle, GSD-2 introduit une approche beaucoup plus disciplinée : chaque token envoyé doit être justifié.

Cette logique repose sur un mécanisme central : les **token profiles**.  
Plutôt que de configurer manuellement chaque paramètre du système, on choisit un profil, et GSD-2 adapte automatiquement son comportement — modèles utilisés, quantité de contexte injectée, phases exécutées, etc.

Voici les trois profils principaux :

| Profil      | Objectif principal        | Contexte envoyé                        | Phases exécutées                     | Cas d’usage typiques                         |
|-------------|--------------------------|----------------------------------------|--------------------------------------|----------------------------------------------|
| **budget**  | Minimiser le coût        | Très réduit (résumés uniquement)       | Phases essentielles uniquement       | Itérations rapides, tests, exploration       |
| **balanced**| Équilibre coût / qualité | Modéré (résumés + éléments clés)       | La plupart des phases                | Usage quotidien, développement standard      |
| **quality** | Maximiser la qualité     | Complet (historique étendu)            | Toutes les phases                    | Tâches complexes, refactoring profond        |

Ce tableau résume une idée importante : GSD-2 ne cherche pas à être “optimal” dans l’absolu, mais à être **adaptatif** selon le contexte d’utilisation.

### Une compression de contexte contrôlée

Derrière ces profils se cache un mécanisme essentiel : la **sélection et compression du contexte**.

Plutôt que de transmettre tout l’historique brut au modèle, GSD-2 reconstruit un contexte pertinent à chaque étape. Cela inclut typiquement :

- un résumé des décisions précédentes  
- le plan courant  
- les éléments directement liés à la tâche en cours  

En mode *budget*, cette reconstruction est très agressive : seuls les éléments critiques sont conservés.  
En mode *quality*, au contraire, le système conserve une vision beaucoup plus large du projet.

Cette approche permet d’éviter un problème classique des agents : plus le contexte grandit, plus il devient… inutile.

### Routage intelligent des tâches

L’optimisation ne s’arrête pas au contexte. GSD-2 ajuste également **quel modèle utiliser** en fonction de la tâche.

Une modification triviale (renommer une variable, corriger une typo) ne nécessite pas le même niveau de raisonnement qu’une refonte d’architecture. Le système détecte cette complexité et adapte automatiquement :

- le modèle appelé  
- la profondeur du raisonnement  
- et le volume de contexte nécessaire  

On évite ainsi deux écueils fréquents :

- surconsommer des tokens pour des tâches simples  
- sous-dimensionner les tâches complexes  


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
