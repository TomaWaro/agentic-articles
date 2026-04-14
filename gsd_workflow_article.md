# Get Shit Done (GSD) : un workflow moderne pour développer avec l’IA

## Introduction

Le framework **Get Shit Done (GSD)** propose une approche radicalement différente du développement assisté par IA.  
Plutôt que de générer du code “au fil de l’eau”, GSD impose un **workflow structuré, traçable et orienté spécifications**.

L’objectif est simple : transformer les modèles d’IA en un **véritable système de production logiciel**, fiable et reproductible.

---

## Philosophie générale

GSD repose sur trois principes fondamentaux :

- **Spec-driven development** : tout part des besoins, pas du code  
- **Context control** : chaque tâche utilise un contexte maîtrisé  
- **Agents spécialisés** : chaque étape est exécutée par un agent dédié  

👉 Résultat : moins d’erreurs, moins d’improvisation, plus de qualité.

---

## Vue d’ensemble du workflow

Le workflow GSD est organisé en phases successives :

Initialisation → Discussion → Planification → Exécution → Vérification → Boucle

Chaque phase produit des artefacts (fichiers `.md`) qui structurent le projet.

---

## 1. Initialisation du projet

**Commande :** `/gsd:new-project`

Cette étape transforme une idée brute en projet structuré.

### Actions réalisées :
- Clarification du besoin via questions
- Recherche éventuelle (agents parallèles)
- Structuration du projet

### Fichiers générés :
- `REQUIREMENTS.md` → besoins fonctionnels
- `ROADMAP.md` → découpage en phases
- `PROJECT.md` → vision globale
- `STATE.md` → état courant du projet

👉 À la fin, le projet est clairement défini et prêt à être développé.

---

## 2. Phase de discussion (optionnelle mais recommandée)

**Commande :** `/gsd:discuss-phase`

Cette étape permet d’affiner la vision produit.

### Objectifs :
- Clarifier les choix UX/UI
- Définir les contraintes techniques
- Capturer l’intention produit

### Fichier généré :
- `CONTEXT.md`

👉 Plus ce fichier est précis, plus l’IA sera pertinente dans la suite.

---

## 3. Phase de planification

**Commande :** `/gsd:plan-phase`

C’est le cœur du système GSD.

### Étapes internes :

#### a. Research
- Analyse des solutions techniques
- Identification des bonnes pratiques
- Choix des outils et librairies

#### b. Planning
- Découpage en tâches **atomiques**
- Chaque tâche est indépendante et exécutable

#### c. Validation
- Vérification de la cohérence avec les requirements
- Inclusion obligatoire de tests
- Contrôle de faisabilité

### Fichiers générés :
- `RESEARCH.md`
- `PLAN.md`

👉 Le projet devient un ensemble de tâches petites, claires et maîtrisées.

---

## 4. Phase d’exécution

**Commande :** `/gsd:execute-phase`

C’est ici que le code est produit.

### Principes clés :

- **Contexte frais pour chaque tâche**  
  → évite la dérive du modèle

- **Exécution par vagues (waves)**  
  → parallèle ou séquentiel selon dépendances

- **Atomicité Git**  
  → 1 tâche = 1 commit

### Résultat :
- Code propre
- Historique Git lisible
- Faible taux d’erreurs

---

## 5. Vérification continue

La validation est intégrée à toutes les étapes.

### Contrôles effectués :
- Validation des plans avant exécution
- Vérification du code après implémentation
- Tests obligatoires

### Fichier produit :
- `VALIDATION.md`

👉 Aucun code n’est accepté sans validation explicite.

---

## 6. Boucle par phases

Le workflow est itératif :

Phase terminée → Phase suivante → (Discussion) → Plan → Execute → Verify

👉 Le projet progresse de manière incrémentale jusqu’à complétion.

---

## Concepts clés du framework

### 1. Orchestrateur léger

GSD utilise un **thin orchestrator** :
- coordonne les étapes
- délègue à des agents spécialisés

👉 Permet de garder un contexte simple et efficace.

---

### 2. State basé sur fichiers

Tout le projet est stocké dans des fichiers Markdown :

- lisibles par l’humain
- exploitables par l’IA

👉 Transparence totale, aucune “mémoire cachée”.

---

### 3. Contrôle du contexte

Chaque tâche est exécutée avec :
- un contexte limité
- des informations ciblées

👉 Résout un problème majeur des LLM : la dégradation du contexte.

---

### 4. Traçabilité complète

REQUIREMENTS → PLAN → CODE → VALIDATION

👉 Chaque ligne de code est justifiée et vérifiable.

---

## Pourquoi GSD est différent

Contrairement au “vibe coding” :

| Approche classique | GSD |
|------|------|
| Code direct | Spécifications d’abord |
| Contexte accumulé | Contexte contrôlé |
| Peu de validation | Validation systématique |
| Résultats variables | Résultats reproductibles |

---

## Conclusion

GSD ne se contente pas d’utiliser l’IA pour coder.  
Il restructure entièrement la manière de développer avec elle.

👉 C’est un passage :
- d’un usage opportuniste de l’IA  
➡️ à une **méthode industrielle de production logicielle**

---

## Résumé en une phrase

**GSD transforme une IA en une chaîne de production logicielle structurée, fiable et traçable.**
