# Prompt Polymarket - Bibliothèque de Prompts pour Trading Polymarket

Ce dossier contient 3 prompts structurés pour le trading sur Polymarket et le développement/maintenance du projet PolyBot, basés sur le guide de prompt engineering.

## Structure

Chaque prompt est conçu pour un aspect spécifique du trading Polymarket et du développement du bot :

1. **Live Trading Assistant** : Assistance au trading en temps réel
2. **Code Review & Optimization** : Review et optimisation du code PolyBot
3. **Trading Strategy Researcher** : Recherche de stratégies de trading

## Liste des Prompts

### 1. Live Trading Assistant (`01_live_trading_assistant.md`)
**Objectif** : Assister le trader dans le trading en live sur Polymarket

**Fonctionnalités** :
- Surveillance du marché en temps réel
- Analyse de probabilités et opportunités
- Recommandations de trades avec gestion des risques
- Suivi des positions ouvertes
- Alertes et reporting en temps réel

**Use Cases** :
- Identifier les opportunités d'arbitrage
- Analyser les changements de probabilités
- Gérer les risques en temps réel
- Optimiser les positions

### 2. Code Review & Optimization Assistant (`02_code_review_optimization_assistant.md`)
**Objectif** : Review complet et optimisation du projet PolyBot

**Fonctionnalités** :
- Code review frontend et backend
- Analyse et amélioration des stratégies de trading
- Optimisation de la synchronisation frontend/backend
- Vérification du fonctionnement avec crypto en live
- Tests et validation

**Projet** : [PolyBot](https://github.com/Ax-404/PolyBot)

**Aspects couverts** :
- Architecture et structure
- Performance et optimisation
- Sécurité (surtout crypto)
- Stratégies de trading
- Synchronisation des systèmes

### 3. Trading Strategy Researcher (`03_trading_strategy_researcher.md`)
**Objectif** : Rechercher et analyser les stratégies de trading pour Polymarket

**Sources de recherche** :
- **arXiv** : Papiers académiques (q-fin, stat, ML, econ)
- **X.com** : Discussions et expériences de traders
- **Autres sources** : Forums, blogs, documentation

**Fonctionnalités** :
- Recherche multi-sources
- Analyse et catégorisation des stratégies
- Évaluation de faisabilité et performance
- Synthèse et recommandations
- Documentation avec références

**Catégories de stratégies** :
- Arbitrage
- Market Making
- Directional
- Mean Reversion
- Event-Based
- ML/AI

## Structure de Chaque Prompt

Chaque prompt suit la structure du guide de prompt engineering :

- **Contexte** : Définition du rôle et de l'expertise
- **Objectif** : But clair et spécifique
- **Instructions Détaillées** : Étapes précises par phase
- **Skills Requis** : Compétences techniques nécessaires
- **Format de Sortie** : Structure des outputs attendus
- **Contraintes** : Limitations et règles importantes
- **Résultat Attendu** : Bénéfices et outcomes

## Utilisation

Chaque prompt peut être utilisé directement avec OpenClaw ou tout autre agent AI. Il suffit de :

1. Ouvrir le fichier du prompt souhaité
2. Copier le contenu complet
3. L'envoyer à l'agent comme instruction système ou prompt de tâche
4. Adapter les paramètres spécifiques (marchés, positions, etc.)

## Intégration avec PolyBot

Ces prompts sont conçus pour travailler en synergie :

1. **Strategy Researcher** → Identifie de nouvelles stratégies
2. **Code Review Assistant** → Implémente et optimise les stratégies dans PolyBot
3. **Live Trading Assistant** → Utilise les stratégies pour trader en live

## Personnalisation

Avant d'utiliser un prompt, pensez à personnaliser :
- Vos préférences de trading (risque, horizon, etc.)
- Les marchés spécifiques à surveiller
- Les paramètres de votre instance PolyBot
- Vos objectifs de performance

## Références

- Guide de prompt engineering : `prompt engineering/guide_prompt_engineering.md`
- Projet PolyBot : https://github.com/Ax-404/PolyBot
- Polymarket : https://polymarket.com
- arXiv : https://www.arxiv.org

## Sécurité

⚠️ **Important** : Ces prompts sont conçus pour le trading avec de l'argent réel. Toujours :
- Tester en testnet d'abord
- Commencer avec de petits montants
- Vérifier la sécurité du code
- Gérer les risques activement
- Ne jamais compromettre la sécurité des clés privées

---

*Dernière mise à jour : Février 2025*

