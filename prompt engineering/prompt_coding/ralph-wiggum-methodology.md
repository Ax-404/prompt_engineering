# Ralph Wiggum Methodology for AI-Assisted Development

> **Méthodologie de développement assisté par IA qui réduit les coûts de développement logiciel de manière drastique.**  
> Basée sur [The Ralph Wiggum Technique](https://github.com/ghuntley/how-to-ralph-wiggum)

## Vue d'Ensemble

La méthodologie Ralph Wiggum structure le développement en **3 phases, 2 prompts, 1 boucle** :

1. **Phase 1 : Define Requirements** (Conversation LLM)
2. **Phase 2 : Planning** (Prompt de planification)
3. **Phase 3 : Building** (Prompt d'implémentation)

Cette méthodologie est optimale pour **Claude Code**, **Cursor**, et autres éditeurs avec support IA.

---

## Phase 1 : Define Requirements (Conversation LLM)

### Objectif
Transformer une idée de projet en spécifications structurées basées sur les "Jobs to Be Done" (JTBD).

### Workflow

#### 1.1 Identifier l'Audience et les JTBD
- **Qui** : Définir l'audience cible (utilisateurs finaux, développeurs, clients, etc.)
- **Pourquoi** : Identifier les "Jobs to Be Done" (résultats désirés par l'audience)
- **Format** : Générer `AUDIENCE_JTBD.md`

**Exemple de structure :**
```markdown
# Audience & Jobs to Be Done

## Audience : [Nom de l'audience]
- **Profil** : [Description]
- **Contexte** : [Contexte d'utilisation]

## Jobs to Be Done
1. **[JTBD 1]** : [Résultat désiré]
2. **[JTBD 2]** : [Résultat désiré]
3. **[JTBD 3]** : [Résultat désiré]
```

#### 1.2 Définir les Activités
Pour chaque JTBD, identifier les **activités** nécessaires pour l'accomplir.

**Pour chaque activité :**
- Définir les **niveaux de capacité** (basic → enhanced)
- Définir les **résultats désirés** à chaque niveau
- Générer `specs/ACTIVITY_NAME.md`

**Exemple de structure :**
```markdown
# Activity: [Nom de l'activité]

## Job to Be Done
[Lien vers le JTBD]

## Niveaux de Capacité

### Basic
- **Capacités** : [Liste]
- **Résultat désiré** : [Description]
- **Critères de succès** : [Métriques]

### Enhanced
- **Capacités** : [Liste]
- **Résultat désiré** : [Description]
- **Critères de succès** : [Métriques]
```

#### 1.3 Utiliser des Subagents pour Charger le Contexte
- Utiliser des subagents pour charger des informations depuis des URLs
- Charger la documentation existante
- Analyser le code existant avec des subagents parallèles

**Exemple :**
```
Utiliser jusqu'à 250 subagents Sonnet en parallèle pour analyser :
- `src/lib/*` (utilitaires partagés)
- `src/*` (code source principal)
- Documentation externe (URLs)
```

---

## Phase 2 : Planning (Prompt de Planification)

### Objectif
Analyser toutes les specs et le code existant pour créer un plan d'implémentation structuré.

### Prompt de Planification (PROMPT_plan.md)

```
0a. Étudier @AUDIENCE_JTBD.md pour comprendre qui on construit pour et leurs Jobs to Be Done.
0b. Étudier `specs/*` avec jusqu'à 250 subagents Sonnet en parallèle pour apprendre les activités JTBD.
0c. Étudier @IMPLEMENTATION_PLAN.md (si présent) pour comprendre le plan actuel.
0d. Étudier `src/lib/*` avec jusqu'à 250 subagents Sonnet en parallèle pour comprendre les utilitaires & composants partagés.
0e. Pour référence, le code source de l'application est dans `src/*`.

1. Séquencer les activités dans `specs/*` en une carte de parcours utilisateur pour l'audience dans @AUDIENCE_JTBD.md. Considérer comment les activités s'enchaînent et quelles dépendances existent.

2. Déterminer la prochaine release SLC (Simple, Lovable, Complete). Utiliser jusqu'à 500 subagents Sonnet pour comparer `src/*` contre `specs/*`. Utiliser un subagent Opus pour analyser les résultats. Ultrathink. Étant donné ce qui est déjà implémenté, recommander quelles activités (à quels niveaux de capacité) forment la prochaine release la plus précieuse. Préférer des tranches horizontales minces - la portée la plus étroite qui délivre encore de la vraie valeur. Une bonne tranche est Simple (étroite, réalisable), Lovable (les gens veulent l'utiliser), et Complete (accomplit pleinement un travail significatif, pas un aperçu cassé).

3. Utiliser un subagent Opus (ultrathink) pour analyser et synthétiser les résultats, prioriser les tâches, et créer/mettre à jour @IMPLEMENTATION_PLAN.md comme une liste à puces triée par priorité des éléments encore à implémenter pour la release SLC recommandée. Commencer le plan par un résumé de la release SLC recommandée (ce qui est inclus et pourquoi), puis lister les tâches priorisées pour cette portée. Considérer les TODOs, placeholders, implémentations minimales, tests ignorés - mais limités à la release. Noter les découvertes hors portée comme travail futur.

IMPORTANT : Planifier uniquement. Ne PAS implémenter quoi que ce soit. Ne PAS supposer que la fonctionnalité manque ; confirmer d'abord avec une recherche de code. Traiter `src/lib` comme la bibliothèque standard du projet pour les utilitaires et composants partagés. Préférer des implémentations consolidées et idiomatiques là-bas plutôt que des copies ad-hoc.

OBJECTIF ULTIME : Nous voulons atteindre la prochaine release la plus précieuse pour l'audience dans @AUDIENCE_JTBD.md. Considérer les éléments manquants et planifier en conséquence. Si un élément manque, rechercher d'abord pour confirmer qu'il n'existe pas, puis si nécessaire créer la spécification à specs/FILENAME.md. Si vous créez un nouvel élément, documenter le plan pour l'implémenter dans @IMPLEMENTATION_PLAN.md en utilisant un subagent.
```

### Critères SLC (Simple, Lovable, Complete)

**Simple** : Portée étroite que vous pouvez livrer rapidement. Pas toutes les activités, pas toutes les profondeurs.

**Lovable** : Les gens veulent vraiment l'utiliser. Délicieux dans ses limites.

**Complete** : Accomplit pleinement un travail dans cette portée. Pas un aperçu cassé.

### Format de Sortie : IMPLEMENTATION_PLAN.md

```markdown
# Plan d'Implémentation

## Release SLC Recommandée : [Nom de la Release]

### Portée
- **Activités incluses** : [Liste]
- **Niveaux de capacité** : [Basic/Enhanced]
- **Justification** : [Pourquoi cette release est précieuse]

## Tâches Priorisées

### Priorité 1 (Critique)
- [ ] [Tâche 1] : [Description]
- [ ] [Tâche 2] : [Description]

### Priorité 2 (Important)
- [ ] [Tâche 3] : [Description]

### Priorité 3 (Amélioration)
- [ ] [Tâche 4] : [Description]

## Travail Futur (Hors Portée)
- [Élément découvert mais non inclus dans cette release]
```

---

## Phase 3 : Building (Prompt d'Implémentation)

### Objectif
Implémenter le plan de manière itérative avec vérification continue.

### Prompt d'Implémentation (PROMPT_build.md)

```
0a. Étudier @IMPLEMENTATION_PLAN.md pour comprendre le plan actuel.
0b. Étudier `src/lib/*` avec jusqu'à 250 subagents Sonnet en parallèle pour comprendre les utilitaires & composants partagés.
0c. Pour référence, le code source de l'application est dans `src/*`.

1. Analyser @IMPLEMENTATION_PLAN.md et identifier la prochaine tâche prioritaire non complétée.

2. Implémenter la tâche :
   - Utiliser les utilitaires de `src/lib/*` quand possible
   - Suivre les conventions du projet existant
   - Écrire des tests pour la nouvelle fonctionnalité
   - Vérifier que le code compile/exécute correctement

3. Vérifier l'implémentation :
   - Lancer les tests
   - Vérifier les logs
   - Comparer le comportement avant/après
   - Se demander : "Est-ce qu'un staff engineer validerait ça ?"

4. Mettre à jour @IMPLEMENTATION_PLAN.md :
   - Cocher la tâche complétée
   - Noter toute découverte ou problème
   - Ajuster les priorités si nécessaire

5. Si la tâche est complétée et vérifiée, passer à la suivante. Sinon, corriger et revérifier.

IMPORTANT : 
- Ne PAS marquer une tâche comme terminée sans l'avoir prouvée dans le main
- Ne PAS introduire de nouveaux bugs
- Toujours challenger son propre travail avant de le présenter
- Si ça part en vrille → STOP immédiatement et re-plan

OBJECTIF ULTIME : Implémenter toutes les tâches de la release SLC recommandée avec qualité production.
```

### Boucle de Vérification

Après chaque implémentation :

1. **Tests** : Lancer tous les tests pertinents
2. **Logs** : Vérifier les logs pour erreurs/avertissements
3. **Comportement** : Comparer avant/après (diff de comportement)
4. **Qualité** : Se demander si un staff engineer validerait
5. **Documentation** : Mettre à jour le plan et les lessons

---

## Principes Clés

### 1. Jobs to Be Done (JTBD) First
- Toujours commencer par comprendre **qui** et **pourquoi** avant **quoi**
- Les specs sont dérivées des JTBD, pas l'inverse

### 2. SLC Releases (Simple, Lovable, Complete)
- Préférer des releases étroites mais complètes plutôt que des MVPs cassés
- Chaque release doit délivrer de la vraie valeur, pas juste un aperçu

### 3. Massive Parallel Subagents
- Utiliser jusqu'à 250-500 subagents en parallèle pour l'analyse
- Déléguer la recherche, l'exploration, l'analyse à des subagents
- Garder le contexte principal propre

### 4. Plan Before Build
- **JAMAIS** implémenter sans plan
- Le plan doit être vérifié par l'humain avant l'implémentation
- Si le plan est mauvais, re-plan, ne pas continuer à construire

### 5. Verification Before Done
- Ne jamais marquer une tâche comme terminée sans preuve
- Tests, logs, comportement - tout doit être vérifié
- Standard staff engineer

### 6. Lessons Learned Loop
- Après chaque correction utilisateur → mettre à jour `tasks/lessons.md`
- Écrire une règle personnelle qui empêche de refaire l'erreur
- Relire les lessons au démarrage de chaque session

---

## Structure de Fichiers Recommandée

```
project/
├── AUDIENCE_JTBD.md              # Audience et Jobs to Be Done
├── IMPLEMENTATION_PLAN.md        # Plan d'implémentation actuel
├── specs/                        # Spécifications par activité
│   ├── activity_1.md
│   ├── activity_2.md
│   └── ...
├── src/                          # Code source
│   ├── lib/                      # Utilitaires partagés (bibliothèque standard)
│   └── ...
├── tasks/
│   ├── todo.md                   # Tâches en cours
│   └── lessons.md                # Leçons apprises
└── PROMPT_plan.md                # Prompt de planification
└── PROMPT_build.md               # Prompt d'implémentation
```

---

## Workflow Complet

### Étape 1 : Requirements (Conversation LLM)
1. Discuter l'idée du projet avec l'LLM
2. Identifier l'audience et les JTBD → `AUDIENCE_JTBD.md`
3. Pour chaque JTBD, identifier les activités
4. Pour chaque activité, créer `specs/ACTIVITY_NAME.md`
5. Utiliser des subagents pour charger le contexte (URLs, docs, code)

### Étape 2 : Planning (Ralph Loop - Mode Plan)
1. Charger `PROMPT_plan.md`
2. Analyser `AUDIENCE_JTBD.md`, `specs/*`, code existant
3. Utiliser 250-500 subagents pour l'analyse parallèle
4. Déterminer la prochaine release SLC
5. Générer/mettre à jour `IMPLEMENTATION_PLAN.md`
6. **Humain vérifie le plan** → Si mauvais, re-plan. Si bon, continuer.

### Étape 3 : Building (Ralph Loop - Mode Build)
1. Charger `PROMPT_build.md`
2. Analyser `IMPLEMENTATION_PLAN.md`
3. Implémenter la prochaine tâche prioritaire
4. Vérifier (tests, logs, comportement)
5. Mettre à jour le plan
6. Répéter jusqu'à ce que la release soit complète

### Étape 4 : Release & Iteration
1. Vérifier que la release SLC est complète
2. Tester la release complète
3. Documenter les lessons apprises
4. Retour à l'Étape 2 pour la prochaine release

---

## Adaptation pour Cursor / Claude Code

### Cursor
- Utiliser les **Composer** pour la phase de planification
- Utiliser les **Chat** pour l'implémentation itérative
- Créer des **@files** pour référencer les specs et plans
- Utiliser les **@codebase** pour l'analyse du code existant

### Claude Code
- Utiliser les **subagents** pour l'analyse parallèle massive
- Utiliser **ultrathink** pour la synthèse et la planification
- Utiliser les **@mentions** pour référencer les fichiers de specs
- Utiliser les **artifacts** pour visualiser les plans

### Autres Éditeurs
- Adapter les prompts selon les capacités de l'éditeur
- Utiliser les fonctionnalités de multi-fichier pour les specs
- Utiliser les fonctionnalités de recherche pour l'analyse du code

---

## Anti-Patterns (À Éviter)

❌ **Implémenter sans plan** : Toujours planifier d'abord  
❌ **Ignorer les JTBD** : Les specs doivent être dérivées des besoins utilisateur  
❌ **Releases trop larges** : Préférer des tranches étroites mais complètes  
❌ **Sauter la vérification** : Ne jamais marquer comme fait sans preuve  
❌ **Ignorer les lessons** : Toujours documenter et apprendre des erreurs  
❌ **Over-engineering** : Simplicité d'abord, élégance ensuite  
❌ **Continuer quand ça part en vrille** : STOP et re-plan immédiatement  

---

## Exemple Concret

### Projet : Système de Gestion de Tâches

**Phase 1 : Requirements**
- Audience : Développeurs solo
- JTBD : "Organiser mes tâches de développement efficacement"
- Activités : Créer tâche, Lister tâches, Marquer complété, Filtrer par projet

**Phase 2 : Planning**
- Release SLC 1 : "Créer et Lister" (Simple, Lovable, Complete)
- Plan : Implémenter création + liste basique, tests, UI simple

**Phase 3 : Building**
- Implémenter création de tâches
- Implémenter liste de tâches
- Tests + vérification
- Release complète et testée

**Phase 4 : Prochaine Release**
- Release SLC 2 : "Marquer complété + Filtres"
- Répéter le cycle

---

## Références

- [The Ralph Wiggum Technique - GitHub](https://github.com/ghuntley/how-to-ralph-wiggum)
- [Jobs to Be Done Framework](https://jtbd.info/)
- [Simple, Lovable, Complete (SLC) - Jason Cohen](https://blog.asmartbear.com/slc.html)

---

*Dernière mise à jour : Février 2025*

