# Workflow Orchestration

> **Note** : Pour les projets complexes (≥ 3 étapes ou décisions architecturales), considérer l'utilisation de la [Méthodologie Ralph Wiggum](ralph-wiggum-methodology.md) qui structure le développement en phases Requirements → Planning → Building avec des specs structurées et des releases SLC (Simple, Lovable, Complete).

## 1. Plan Mode Default
- Entrer en **plan mode** pour toute tâche non-triviale (≥ 3 étapes ou décisions architecturales)
- Si ça part en vrille → **STOP** immédiatement et **re-plan** — ne pas continuer à pousser
- Utiliser le plan mode aussi pour les **étapes de vérification**, pas seulement pour construire
- Écrire des **spécifications détaillées de vérification** dès le départ

## 2. Subagent Strategy
- Utiliser les **subagents** sans modération pour garder le contexte principal propre
- Offloader : recherche, exploration, analyses parallèles
- Pour les problèmes complexes → **jeter plus de subagents** en parallèle
- **Une tâche = un subagent** → focus maximal
- Skip le mode "Self" quand on peut déléguer à un subagent

## 3. After ANY Improvement / Correction Loop
Après chaque correction faite par l'utilisateur :
- Mettre à jour `tasks/lessons.md` avec le **pattern exact** de l'erreur
- Écrire une **règle personnelle** qui empêche de refaire cette même erreur
- Itérer **sans pitié** sur ces leçons jusqu'à ce que le taux d'erreur chute drastiquement
- Relire les lessons au démarrage de chaque session pertinente

## 4. Verification Before Done
- **Ne jamais** marquer une tâche comme terminée sans l'avoir prouvé dans le main
- Comparer le comportement avant/après (diff de comportement)
- Se poser la question :  
  **« Est-ce qu'un staff engineer validerait ça ? »**
- Lancer les tests, vérifier les logs, démontrer la correction

## 5. Elegance (Balanced)
- Pour tout changement non-trivial → pause et se demander :  
  **« Existe-t-il une solution plus élégante ? »**
- Si la fix sent le « hack » → se dire :  
  « Je ne sais pas encore comment faire proprement → je n'implémente **pas** cette version moche »
- **Ne pas over-engineer** les fixes simples
- Toujours challenger son propre travail avant de le présenter

## 6. Autonomous Bug Fixing
- Bug report donné → **just fix it**, ne pas demander immédiatement de l'aide
- Pointer logs, erreurs, tests qui cassent → puis résoudre
- Zéro contexte de tests CI qui cassent doit être fourni par l'utilisateur

## Task Management

1. **Plan First** : Écrire le plan dans `tasks/todo.md` avec items checkables  
2. **Verify Plan** : Valider le plan avant de commencer l'implémentation  
3. **Explain Changes** : Résumé high-level des changements à chaque grosse étape  
4. **Track Progress** : Cocher / marquer les tâches au fur et à mesure  
5. **Document Results** : Ajouter une section review dans `tasks/todo.md`  
6. **Capture Lessons** : Mettre à jour `tasks/lessons.md` après chaque correction

## Core Principles

- **Simplicity First** : Chaque changement doit être **aussi simple que possible**  
- **No Laziness** : Trouver la **root cause**. Pas de correctifs temporaires. Standard senior dev.  
- **Minimal Impact** : Toucher **uniquement** ce qui est nécessaire. Éviter d'introduire de nouveaux bugs.