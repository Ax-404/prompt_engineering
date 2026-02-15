# Prompts Coding Business - Développement Assisté par IA pour le Business

Ce dossier contient le prompt de développement assisté par IA optimisé pour le contexte business, combinant deux méthodologies puissantes.

## Prompt Disponible

### `workflow_orchestration_business.md` - Workflow Orchestration & Ralph Wiggum Methodology

**Prompt combiné** qui adapte les meilleures pratiques de développement au contexte business.

**Caractéristiques :**
- **Deux modes** : Workflow Orchestration (tâches simples) + Ralph Wiggum (projets complexes)
- **Business-focused** : Toujours considère l'impact business et la valeur générée
- **Structuré** : Suit la structure du guide de prompt engineering
- **Complet** : Combine les deux méthodologies en un seul prompt cohérent

## Quand Utiliser Chaque Mode

### Mode Workflow Orchestration (Tâches Simples)
**Utiliser pour :**
- ✅ Tâche simple ou modérée (< 3 étapes)
- ✅ Correction de bug
- ✅ Petite amélioration
- ✅ Refactoring localisé
- ✅ Vous avez déjà une bonne compréhension du code

**Workflow :**
1. Plan Mode (si nécessaire)
2. Implémenter avec subagents
3. Vérifier (tests, logs, comportement)
4. Capturer Lessons

### Mode Ralph Wiggum (Projets Complexes)
**Utiliser pour :**
- ✅ Nouveau projet ou fonctionnalité majeure
- ✅ Tâche complexe (≥ 3 étapes ou décisions architecturales)
- ✅ Besoin de structurer les requirements
- ✅ Développement de zéro
- ✅ Refactoring architectural important
- ✅ Vous voulez des releases SLC structurées

**Workflow :**
1. **Phase 1 : Requirements** → `AUDIENCE_JTBD.md` + `specs/*.md`
2. **Phase 2 : Planning** → `IMPLEMENTATION_PLAN.md` (SLC release)
3. **Phase 3 : Building** → Implémentation itérative avec vérification
4. **Phase 4 : Release** → Test, mesure impact business, itération

## Intégration avec Master_of_all_for_business.md

Ce prompt est automatiquement utilisé par `Master_of_all_for_business.md` pour :
- Développement d'automatisations business
- Création de workflows techniques
- Implémentation de solutions business
- Intégration d'APIs business (marketing, sales, finance)

## Principes Clés

1. **Business Value First** : Toujours considérer l'impact business
2. **Jobs to Be Done** : Comprendre qui et pourquoi avant quoi
3. **SLC Releases** : Simple, Lovable, Complete - pas de MVPs cassés
4. **Plan Before Build** : Jamais implémenter sans plan
5. **Verification Before Done** : Standard staff engineer
6. **Lessons Learned** : Documenter et apprendre des erreurs

## Structure de Fichiers Recommandée

```
project/
├── AUDIENCE_JTBD.md              # Audience et Jobs to Be Done (Business Context)
├── IMPLEMENTATION_PLAN.md        # Plan d'implémentation actuel
├── specs/                        # Spécifications par activité
│   ├── activity_1.md
│   └── activity_2.md
├── src/                          # Code source
│   ├── lib/                      # Utilitaires partagés
│   └── ...
├── tasks/
│   ├── todo.md                   # Tâches en cours
│   └── lessons.md                # Leçons apprises
└── PROMPT_plan.md                # Prompt de planification
└── PROMPT_build.md               # Prompt d'implémentation
```

## Références

- [The Ralph Wiggum Technique](https://github.com/ghuntley/how-to-ralph-wiggum)
- [Jobs to Be Done Framework](https://jtbd.info/)
- [Simple, Lovable, Complete (SLC)](https://blog.asmartbear.com/slc.html)
- [Guide Prompt Engineering](../../guide_prompt_engineering.md)

---

*Dernière mise à jour : Février 2025*

