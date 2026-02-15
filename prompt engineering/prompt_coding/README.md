# Prompts Coding - Développement Assisté par IA

Ce dossier contient les prompts pour le développement assisté par IA, optimisés pour **Claude Code**, **Cursor**, et autres éditeurs avec support IA.

## Structure des Prompts

### 1. `workflow-orchestration.md` - Workflow Général
**Quand l'utiliser :** Pour la plupart des tâches de développement quotidiennes.

**Caractéristiques :**
- Plan mode par défaut pour tâches non-triviales
- Utilisation massive de subagents
- Vérification avant marquer comme terminé
- Capture de lessons apprises
- Gestion de tâches structurée

**Idéal pour :**
- Corrections de bugs
- Petites fonctionnalités
- Refactoring ciblé
- Tâches de maintenance

### 2. `ralph-wiggum-methodology.md` - Méthodologie Structurée
**Quand l'utiliser :** Pour les projets complexes, nouvelles fonctionnalités majeures, ou développement de zéro.

**Caractéristiques :**
- Structure en 3 phases : Requirements → Planning → Building
- Jobs to Be Done (JTBD) first
- Releases SLC (Simple, Lovable, Complete)
- Spécifications structurées (`specs/*.md`)
- Plan d'implémentation détaillé
- Utilisation massive de subagents parallèles (250-500)

**Idéal pour :**
- Nouveaux projets
- Fonctionnalités majeures
- Refactoring architectural
- Développement de produits

## Quand Utiliser Quelle Méthodologie ?

### Utiliser `workflow-orchestration.md` si :
- ✅ Tâche simple ou modérée (< 3 étapes)
- ✅ Correction de bug
- ✅ Petite amélioration
- ✅ Refactoring localisé
- ✅ Vous avez déjà une bonne compréhension du code

### Utiliser `ralph-wiggum-methodology.md` si :
- ✅ Nouveau projet ou fonctionnalité majeure
- ✅ Tâche complexe (≥ 3 étapes ou décisions architecturales)
- ✅ Besoin de structurer les requirements
- ✅ Développement de zéro
- ✅ Refactoring architectural important
- ✅ Vous voulez des releases SLC structurées

## Workflow Recommandé

### Pour Tâches Simples
```
1. Charger `workflow-orchestration.md`
2. Plan mode (si nécessaire)
3. Implémenter
4. Vérifier
5. Capturer lessons
```

### Pour Projets Complexes
```
1. Phase Requirements (LLM conversation)
   - Définir audience et JTBD → `AUDIENCE_JTBD.md`
   - Créer specs par activité → `specs/*.md`

2. Phase Planning (Ralph Loop - Mode Plan)
   - Charger `ralph-wiggum-methodology.md` → `PROMPT_plan.md`
   - Analyser specs + code existant
   - Déterminer release SLC
   - Générer `IMPLEMENTATION_PLAN.md`
   - **Humain vérifie le plan**

3. Phase Building (Ralph Loop - Mode Build)
   - Charger `ralph-wiggum-methodology.md` → `PROMPT_build.md`
   - Implémenter tâches priorisées
   - Vérifier chaque implémentation
   - Mettre à jour le plan

4. Release & Itération
   - Tester la release complète
   - Documenter lessons
   - Retour à Phase 2 pour prochaine release
```

## Intégration avec OpenClaw

Ces prompts sont conçus pour être utilisés avec **OpenClaw Business** (instance de coding) :

- **Modèle par défaut** : Kimi K2 2.5 (pour la plupart des tâches)
- **Modèle alternatif** : Claude Code (pour code review critique, sécurité, refactoring complexe)

Voir `prompt_openclaw.md` pour les règles de sélection de modèle.

## Structure de Fichiers Recommandée

```
project/
├── AUDIENCE_JTBD.md              # (Ralph) Audience et Jobs to Be Done
├── IMPLEMENTATION_PLAN.md        # (Ralph) Plan d'implémentation actuel
├── specs/                        # (Ralph) Spécifications par activité
│   ├── activity_1.md
│   └── activity_2.md
├── tasks/                        # (Workflow) Gestion de tâches
│   ├── todo.md                   # Tâches en cours
│   └── lessons.md                # Leçons apprises
├── src/                          # Code source
│   ├── lib/                      # Utilitaires partagés
│   └── ...
└── PROMPT_plan.md                # (Ralph) Prompt de planification
└── PROMPT_build.md               # (Ralph) Prompt d'implémentation
```

## Principes Communs

Les deux méthodologies partagent ces principes :

1. **Plan Before Build** : Toujours planifier avant d'implémenter
2. **Verification Before Done** : Ne jamais marquer comme terminé sans preuve
3. **Subagents Strategy** : Utiliser des subagents pour garder le contexte propre
4. **Lessons Learned** : Documenter et apprendre des erreurs
5. **Simplicity First** : Chaque changement doit être aussi simple que possible
6. **No Laziness** : Trouver la root cause, pas de correctifs temporaires

## Références

- [The Ralph Wiggum Technique](https://github.com/ghuntley/how-to-ralph-wiggum)
- [Jobs to Be Done Framework](https://jtbd.info/)
- [Simple, Lovable, Complete (SLC)](https://blog.asmartbear.com/slc.html)
- [Guide Prompt Engineering](../guide_prompt_engineering.md)

---

*Dernière mise à jour : Février 2025*

