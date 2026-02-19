# Prompt N8N — Automatisation

Ce dossier contient des prompts structurés pour concevoir et générer des workflows **n8n** (automatisation no-code/low-code), selon les principes du guide de prompt engineering.

## Structure

Chaque prompt suit la structure du guide :
- **Contexte** : Rôle et expertise (Architecte de workflows n8n)
- **Objectif** : Génération de workflows JSON prêts à l'import
- **Instructions Détaillées** : Phases adaptatives (3–15 selon la complexité)
- **Skills Requis** : Compétences techniques nécessaires
- **Format de Sortie** : JSON n8n, guide de déploiement, documentation optionnelle
- **Contraintes** : Règles de validation et bonnes pratiques
- **Résultat Attendu** : Workflow importable + guide d’activation

## Liste des Prompts

1. **n8n_workflow_generator.md** — Générateur de workflows n8n prêts pour la production  
   - Découverte des exigences (questionnement socratique)  
   - Identification des opérations et structure du workflow  
   - Validation pré-vol (credentials, données de test)  
   - Cartographie logique et flux de données  
   - Configuration des nœuds et assemblage JSON  
   - Pattern matching et bonnes pratiques  
   - Génération JSON finale et validation  
   - Guide d’implémentation et déploiement  
   - Documentation optionnelle (Markdown, Notion, etc.)

## Utilisation

1. Ouvrir le fichier du prompt (ex. `n8n_workflow_generator.md`).
2. Copier le contenu complet.
3. L’utiliser comme instruction système ou prompt de tâche dans ton agent / LLM.
4. Décrire l’automatisation souhaitée (déclencheur, données, outils, résultat attendu).
5. Suivre les phases : le modèle guidera les clarifications, puis produira le JSON n8n et le guide de déploiement.

## Personnalisation

À adapter selon :
- Outils et intégrations (Google, Airtable, Stripe, Slack, etc.)
- Niveau technique (débutant → instructions détaillées ; avancé → JSON direct)
- Contexte métier (processus récurrents, points de douleur)
- Urgence (MVP rapide vs workflow entreprise complet)

## Principes Clés

- **Clarté avant vitesse** : Comprendre l’automatisation avant de générer le workflow.
- **Guider, pas dicter** : Questions de clarification quand la logique est floue.
- **Production-ready** : Gestion d’erreurs (retry, notify, log), validation, scénarios de test.
- **Activation, pas seulement création** : Livrer un guide de déploiement et de test.

## Références

- Guide de prompt engineering : `prompt engineering/guide_prompt_engineering.md`
- n8n : https://n8n.io

---

*Dernière mise à jour : Février 2025*
