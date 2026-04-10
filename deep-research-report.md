# Spec‑Driven Development en 2026 : comparaison des principaux outils SDD et recommandation d’adoption

## Executive summary

Le **Spec‑Driven Development (SDD)** regroupe des pratiques et outils qui rendent la **spécification** (fichiers versionnés) centrale pour cadrer, planifier et faire exécuter le travail par des agents de code. Une convergence ressort des comparatifs récents : *les outils SDD sont très bons pour créer une feature “from scratch”, mais beaucoup moins naturels pour des modifications itératives sur un existant* — le fameux **“Modification Problem”**. citeturn18view0turn19view2  

**Recommandation claire (avril 2026)** :  
- **Choix principal** : **GitHub Spec Kit** pour cadrer et standardiser le flux “spec → plan → tasks”, avec un écosystème très dynamique et une forte adoption open‑source. citeturn17view2turn10search0  
- **Complément quasi systématique** (brownfield / évolutions fréquentes) : **OpenSpec**, conçu *modification‑first* via des “deltas”, pour réduire l’overhead lors des changements incrémentaux. citeturn18view0turn19view2turn13view1  

**Alternatives selon contexte** :  
- **BMad Method** si vous avez besoin de **gouvernance, auditabilité et rôles** (cadre fort, mais plus lourd). citeturn1view1turn13view0turn10search6  
- **GSD** si votre problème principal est la **fiabilité d’exécution** (lutte contre le “context rot”) et un workflow “anti‑bureaucratie”. citeturn8search2turn8search10turn3search1  
- **Task Master** si votre goulot d’étranglement est la **gestion de backlog/dépendances** et l’orchestration multi‑modèles — en acceptant une licence plus restrictive (Commons Clause). citeturn6view3turn10search3turn10search7  
- **Spec Kitty** si vous faites du **travail parallèle** et voulez de l’isolation forte via **git worktrees** intégrés. citeturn18view0turn15view2  
- **Kiro** et **Tessl** plutôt en **veille/expérimentation** (approches plus “plateforme”, risques de lock‑in et/ou d’accès). citeturn18view0turn1view1turn8search5turn9search1  

## Méthode, périmètre et sources autorisées

Cette recherche est **strictement limitée** aux domaines explicitement autorisés : **hoko.team**, **github.com** et **spillwave.com**. Les informations de maturité (versions/dates) sont relevées sur les **pages de releases / changelogs** GitHub à la date du **10 avril 2026**. citeturn1view1turn17view2turn15view2turn8search2turn13view1turn6view3  

Deux sources structurantes servent de colonne vertébrale :  
- **spec-compare** (GitHub) : un travail de comparaison approfondi (6 outils principaux + extensions), avec un accent utile sur l’itération, les worktrees et les anti‑patterns. citeturn18view0turn19view2  
- L’article **Hoko** “6 frameworks AIDD 2026” : un comparatif orienté adoption (setup time, learning curve, positionnement “top‑down vs bottom‑up”). citeturn1view1  

En complément, des contenus **Spillwave** apportent un point de vue “terrain” sur GSD et sur la divergence des outils SDD (malheureusement, certains articles sont hébergés via une expérience Medium et ne sont pas toujours ouvrables dans tous les environnements, mais leurs résumés indexés restent exploitables ici). citeturn3search0turn3search1  

## Lecture simple de l’écosystème SDD

L’écosystème se comprend mieux comme une **chaîne** que comme un outil unique :  
- **Spec authoring / workflow** : structurer la spec et produire plan + tâches (Spec Kit, OpenSpec, BMad, Spec Kitty, Kiro, Tessl tile). citeturn18view0turn1view1  
- **Orchestration** : gérer dépendances, priorités, multi‑modèles (Task Master). citeturn6view3turn7search1  
- **Exécution & fiabilité** : rendre l’agent fiable sur des sessions longues (GSD) et réduire la dérive de contexte (“context rot”). citeturn8search10turn3search1  
- **Intégration CI/PR** : la majorité des frameworks reposent sur le fait que les artefacts (specs/plans/tasks) sont **dans le repo**, donc revus en PR et automatisables (lint, vérifs, gates). Spec Kit, par exemple, investit fortement dans les intégrations et l’outillage “community extensions”. citeturn17view2turn9search3  

```mermaid
flowchart TD
  A[Spec authoring / workflow<br/>spec → plan → tasks] --> B[Orchestration<br/>(dépendances, priorités)]
  A --> C[Implémentation par agent/IDE]
  C --> D[Test runners & vérification<br/>(tests, checklists)]
  D --> E[CI / PR gates<br/>(qualité, auditabilité)]

  subgraph Frameworks SDD
    SK[GitHub Spec Kit]
    OS[OpenSpec]
    BM[BMad Method]
    SKi[Spec Kitty]
    KI[Kiro]
    TS[Tessl Tile]
  end

  subgraph Orchestration
    TM[Task Master]
  end

  subgraph Execution reliability
    GSD[GSD]
  end

  A --- SK
  A --- OS
  A --- BM
  A --- SKi
  A --- KI
  A --- TS

  B --- TM
  C --- GSD
```

## Tableau comparatif synthétique

Le tableau ci‑dessous met volontairement l’accent sur une lecture **décisionnelle** et non “tutoriel”, pour des **tech leads / PM**. Les données de versions/dates/licences sont détaillées juste après le tableau (avec sources). citeturn1view1turn18view0  

| Outil | But | Maturité | Intégrations clés | Points forts | Limites | Recommandation d’usage |
|---|---|---|---|---|---|---|
| **GitHub Spec Kit** | Standardiser un workflow SDD “spec → plan → tasks”, orienté adoption large | Très actif (releases fréquentes) | Agents multiples, extensions, Git/PR | Écosystème, industrialisation, traction | Moins optimisé pour “petites retouches” | **Choix principal** (standard d’équipe, greenfield, cadrage) |
| **OpenSpec** | SDD “change‑centric” (deltas) pour itérer sur un existant | Stable 1.x | Outils multiples, multi‑langue | Minimal overhead, brownfield‑first | Moins “gouvernance enterprise” | **Complément idéal** à Spec Kit pour itérations/brownfield |
| **BMad Method** | Framework multi‑agents, gouvernance et “process” complet | v6 très actif | Nombreux outils/agents | Auditabilité, rôles, profondeur | Setup + learning curve élevés | Enterprise / projets à fort enjeu & besoin de cadre |
| **GSD** | Fiabiliser l’exécution (context engineering), SDD “anti‑bureaucratie” | Releases fréquentes 1.x | Claude Code + autres agents | Robustesse sur sessions longues, discipline de contexte | Moins centré “spec authoring” standard | Solo/PM‑tech très orientés delivery fiable |
| **Task Master** | Orchestration de tâches (dépendances, workflows), multi‑modèles | Releases 0.x actives | MCP/IDE, multi‑providers | Backlog structuré, dépendances, PRD‑driven | Licence Commons Clause (SaaS interdit) | Équipes qui veulent industrialiser la planif/exécution |
| **Spec Kitty** | Workflow complet + **git worktrees** intégrés (travail parallèle) | v3 très actif | Worktrees, artefacts repo‑native | Parallélisme, isolation, suivi | Overhead possible pour petits changements | Équipes parallélisant des features/branches |
| **Kiro** | IDE agentique intégré “Requirements → Design → Tasks” | Preview, évolue vite | IDE + CLI, hooks | UX intégrée, parcours guidé | Propriétaire, moins flexible | À choisir si vous assumez l’écosystème/contrat Kiro |
| **Tessl (tile SDD)** | Approche “spec‑as‑source” / méthodologie pour agents | Activité modérée (tile) | Tile/agents Tessl | Vision “spec very central” | Dépendance plateforme, maturité à prouver | R&D / veille, pas standard “par défaut” |

**Données de maturité (vérifiées au 10 avril 2026)** :  
- **Spec Kit** : dernières entrées de changelog incluant **0.6.0 (2026‑04‑09)**, après 0.5.1 (2026‑04‑08) ; licence **MIT**. citeturn17view2turn10search0  
- **OpenSpec** : release **v1.0.2 (2026‑01‑27)** sur une branche 1.x “stable”, licence **MIT**. citeturn13view1turn10search5  
- **BMad** : releases **v6.0.4 (2026‑03‑01)** et **v6.0.3 (2026‑02‑23)**, avec cadre multi‑agents ; licence avec **mention de marques** (trademark notice). citeturn13view0turn10search6turn4search6  
- **GSD** : release **v1.34.2 (2026‑04‑06)**, licence **MIT**. citeturn8search2turn11search1  
- **Task Master** : release **task-master-ai@0.43.0 (2026‑02‑04)** ; licence **MIT + Commons Clause** (restrictions sur revente/hosting). citeturn6view3turn10search3turn10search7  
- **Spec Kitty** : release **v3.1.1 (2026‑04‑09)** ; licence **MIT**. citeturn15view2turn11search8  
- **Kiro** : pas de “releases” GitHub publiées (page Releases vide) et positionnement preview/propriétaire dans les comparatifs. citeturn8search5turn18view0turn1view1  
- **Tessl tile** : repo “spec-driven-development-tile” (composant open source) décrivant une méthodologie SDD ; licence indiquée **MIT** dans l’organisation Tessl sur GitHub. citeturn12search12turn12search9  

## Analyse qualitative des outils

### Ce qui différencie vraiment les outils en 2026

Deux axes dominent les comparatifs récents.  
Le premier est **l’overhead vs la couverture** : du “léger & rapide” (OpenSpec) au “complet mais lent sur petites modifs” (BMad/Kiro). spec-compare formalise même un **spectre de workflows de modification** et recommande explicitement de *ne pas forcer chaque micro‑changement* dans un pipeline SDD complet. citeturn19view2turn19view1  

Le second axe est la **nature du travail réel** (brownfield). spec-compare insiste sur le fait que la difficulté centrale n’est pas “écrire une spec”, mais **faire évoluer les specs sans les faire dériver** et sans casser la vélocité, d’où l’intérêt des outils “living specs” (OpenSpec, et dans une logique plus radicale, Tessl). citeturn19view2turn18view0  

### Positionnement outil par outil

**GitHub Spec Kit** est aujourd’hui le candidat le plus “standardisable” : il pousse des **spécifications exécutables** et un mécanisme de **validation continue** (ambigüités, contradictions, gaps), et investit massivement dans une architecture d’intégrations/agents et un catalogue d’extensions. citeturn9search13turn17view2turn9search3  
Le risque principal n’est pas technique, mais organisationnel : si vous l’imposez pour toute retouche, vous recréez une bureaucratie de specs. spec-compare note que Spec Kit est moins naturel pour les petites modifications et peut nécessiter des contournements (ex. phase “clarify”). citeturn18view0turn19view2  

**OpenSpec** se positionne explicitement comme une “couche spec légère” quand les exigences vivent sinon “dans le chat”, et sa release 1.x marque le passage “experimental → stable” avec un système d’actions basé sur l’état des artefacts. citeturn10search9turn13view1  
Sa valeur est maximale en **brownfield** et en **changement incrémental** ; spec-compare le met en “Best” pour des modifications simples grâce à un format delta et un overhead minimal, et recommande un couple **Spec Kit (greenfield) + OpenSpec (modifications)**. citeturn19view2turn19view1  

**BMad Method** est l’option “process & gouvernance” : multi‑agents, workflows structurés, et un discours clair sur l’adaptation de la profondeur de planification à la complexité (“Scale‑Domain‑Adaptive”). citeturn4search6turn1view1  
Hoko associe BMad à des contextes enterprise/audit, mais souligne une **learning curve élevée** et un setup plus long que les approches minimalistes. citeturn1view1turn13view0  
Côté risques, la licence mentionne explicitement des **contraintes de marque** (trademark) : ce n’est pas bloquant, mais c’est un point à anticiper pour un standard interne (naming, communication, redistribution). citeturn10search6  

**GSD** est moins un “framework de specs” qu’une **couche de fiabilité** : il se présente comme une combinaison de meta‑prompting, context engineering et SDD, “anti context rot”, et annonce une compatibilité large (Claude Code, OpenCode, Gemini CLI, Codex, Copilot, Cursor, etc.). citeturn8search10turn8search2  
Le point de vue Spillwave met en avant l’idée clé : éviter que la connaissance projet reste enfermée dans des conversations en la stockant en **fichiers**. citeturn3search1  
On le recommande quand vos incidents viennent moins d’un manque de specs que d’un agent qui “oublie”, dérive et produit du code incohérent après plusieurs itérations. citeturn8search10turn11search9  

**Task Master** vise l’orchestration : structuration de tâches, dépendances, et usage **multi‑providers** (avec clés API), en distinguant “main/research/fallback model”. citeturn7search1  
C’est très intéressant pour des équipes orientées **PRD → exécution**, mais le point d’attention est la **licence MIT + Commons Clause** : vous pouvez l’utiliser, le modifier, construire des produits avec, mais vous ne pouvez pas le revendre/hoster comme service concurrent. citeturn10search7turn10search3  

**Spec Kitty** s’adresse aux équipes qui veulent industrialiser le SDD *et* paralléliser proprement : la promesse est un flux repeatable “spec → plan → tasks → implement → review → merge”, et une réponse à trois douleurs très concrètes : dérive sur longues sessions, difficulté à coordonner le travail parallèle, incohérence des critères d’acceptation. citeturn8search0turn11search8  
spec-compare souligne surtout son différenciateur majeur : **seul outil avec support git worktree intégré** dans son comparatif de base. citeturn18view0turn19view0  

**Kiro** est un IDE agentique intégrant un workflow “Requirements → Design → Tasks” et des “agent hooks”. citeturn8search1  
Les comparatifs s’accordent sur son risque : c’est une approche **plus directive et moins “skippable”**, potentiellement sur‑dimensionnée pour des micro‑changements, avec un positionnement **propriétaire/preview** (donc décision plus “produit/achats” que “tooling”). citeturn19view0turn18view0turn1view1  

**Tessl (tile SDD)** illustre la tendance “spec‑as‑source” : une méthodologie qui enseigne aux agents à **collecter les exigences, écrire des specs, obtenir approbation avant code**, et à maintenir une chaîne traçable exigences → implementation (liens vers tests). citeturn12search9turn12search17  
Dans spec-compare, Tessl est associé à une vision “spec‑as‑source” mais aussi à un risque d’accès/maturité (beta/plateforme). citeturn18view0turn19view2  

## Recommandation finale

### Choix principal

**Standardisez sur GitHub Spec Kit** comme socle SDD d’équipe : c’est aujourd’hui l’outil le plus simple à “institutionnaliser” (artefacts repo‑native, intégrations/agents, écosystème d’extensions), avec une cadence de releases très élevée jusqu’à **0.6.0 (2026‑04‑09)**. citeturn17view2turn9search3turn10search0  

### Alternatives et combinaisons pragmatiques

- **Spec Kit + OpenSpec** est la combinaison la plus rationnelle **en production** : Spec Kit pour cadrer et livrer des features structurées, OpenSpec pour absorber le brownfield et les changements fréquents, exactement comme recommandé par spec-compare (hybrid approach) et explicitement suggéré par Hoko. citeturn19view2turn1view1  
- Si vous avez un besoin de **work parallèle propre** (équipes qui développent plusieurs features en même temps) : privilégiez **Spec Kitty** pour son worktree management intégré. citeturn18view0turn15view2  
- Si vous souffrez surtout de **dérive de contexte** (agents incohérents après plusieurs cycles) : **GSD** devient une option prioritaire, éventuellement en complément d’un cadre de specs plus simple. citeturn8search10turn3search1  
- Si vous avez des enjeux **enterprise/audit/compliance** (process, rôles, “checks & balances”) : **BMad** est cohérent, mais il faut assumer son coût d’adoption (setup + learning curve). citeturn1view1turn13view0turn4search6  
- Si votre enjeu central est la **gestion de tâches/dépendances** et l’orchestration multi‑modèles : **Task Master**, en gardant en tête la licence MIT + Commons Clause. citeturn7search1turn10search7  
- Pour **Kiro** et **Tessl** : à traiter comme des paris produit (UX/plateforme) à évaluer en pilote, pas comme un standard neutre. citeturn18view0turn1view1turn12search9  

## Pages consultées

### hoko.team
- Article “Spec‑Driven Development : 6 Frameworks AIDD…” (comparatif, profils recommandés, setup/learning curve). citeturn1view1  

### github.com
- Repo **cameronsjo/spec-compare** (findings, maturité SDD, recommandations). citeturn18view0  
- Analyse itération “Iterative Development” (anti‑patterns, hybrid approach). citeturn19view2turn19view1  
- **GitHub spec-kit** changelog (versions/dates) + licence MIT. citeturn17view2turn10search0  
- **Fission-AI/OpenSpec** releases + licence MIT. citeturn13view1turn10search5  
- **bmad-code-org/BMAD-METHOD** releases + licence/trademark notice. citeturn13view0turn10search6  
- **gsd-build/get-shit-done** releases + licence MIT. citeturn8search2turn11search1  
- **eyaltoledano/claude-task-master** releases + licence Commons Clause. citeturn6view3turn10search3  
- **Priivacy-ai/spec-kitty** releases + README (workflow, motivations). citeturn15view2turn11search8  
- **kirodotdev/Kiro** repo + releases (absence de releases). citeturn8search1turn8search5  
- **tesslio/spec-driven-development-tile** README/docs + licence MIT indiquée dans l’org. citeturn12search9turn12search12turn12search17  

### spillwave.com
- Résumé indexé “What Is GSD? Spec‑Driven Development Without the Ceremony”. citeturn3search1  
- Résumé indexé “Agentic Coding: GSD vs Spec Kit vs OpenSpec vs Taskmaster…”. citeturn3search0