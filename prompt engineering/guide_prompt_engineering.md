# Guide Complet du Prompt Engineering

> *"Un system prompt peut souvent être interprété comme une liste détaillée de toutes les choses que le modèle faisait avant qu'on lui dise de ne plus les faire."*  
> — Simon Willison, à propos des system prompts de Claude 4

## Table des Matières

1. [Principes Fondamentaux](#principes-fondamentaux)
2. [Structure d'un Bon Prompt](#structure-dun-bon-prompt)
3. [Techniques Avancées](#techniques-avancées)
4. [Leçons du Claude 4 System Prompt](#leçons-du-claude-4-system-prompt)
5. [Patterns et Templates](#patterns-et-templates)
6. [Erreurs Communes à Éviter](#erreurs-communes-à-éviter)
7. [Optimisation et Itération](#optimisation-et-itération)

---

## Principes Fondamentaux

### 1. Clarté et Spécificité

**❌ Mauvais :**
```
Écris-moi quelque chose sur le marketing.
```

**✅ Bon :**
```
Écris un article de blog de 800 mots sur le marketing de contenu B2B, 
ciblant les CMO de startups tech. Ton professionnel mais accessible. 
Inclus 3 études de cas réelles et 5 actions concrètes à mettre en place.
```

### 2. Contexte et Persona

Définir clairement qui est le modèle et dans quel contexte il opère :

```
Tu es un expert en architecture logicielle avec 15 ans d'expérience.
Tu conseilles des équipes de développement sur des décisions techniques.
Tu privilégies la simplicité, la maintenabilité et la scalabilité.
```

### 3. Format de Sortie Explicite

Toujours spécifier le format attendu :

```
Fournis ta réponse sous la forme :
1. Résumé exécutif (3-4 phrases)
2. Analyse détaillée (3-5 paragraphes)
3. Recommandations actionnables (liste à puces)
4. Risques et mitigations (tableau)
```

### 4. Exemples Positifs et Négatifs

Les exemples sont parmi les techniques les plus puissantes :

```
Voici des exemples de bonnes réponses :
✅ "Basé sur les données de Q3, je recommande..."
✅ "En analysant les 3 options, l'option B est optimale car..."

Voici des exemples de réponses à éviter :
❌ "Je pense que peut-être..."
❌ "C'est difficile à dire mais..."
```

---

## Structure d'un Bon Prompt

### Template de Base

```
[CONTEXTE]
Tu es [persona/expertise]. Tu opères dans [domaine/contexte].

[OBJECTIF]
[Description claire de la tâche]

[CONTRAINTES]
- [Contrainte 1]
- [Contrainte 2]
- [Contrainte 3]

[FORMAT DE SORTIE]
[Description précise du format attendu]

[EXEMPLES]
[Exemples concrets si pertinents]

[RÈGLES]
- [Règle 1]
- [Règle 2]
- [Règle 3]
```

### Exemple Complet

```
CONTEXTE:
Tu es un développeur senior spécialisé en React et TypeScript avec 10 ans d'expérience.
Tu travailles sur une application e-commerce moderne.

OBJECTIF:
Réfacter ce composant pour améliorer les performances et la maintenabilité.

CONTRAINTES:
- Conserver la fonctionnalité existante à 100%
- Utiliser React 18+ avec hooks uniquement
- TypeScript strict mode activé
- Pas de dépendances externes supplémentaires
- Performance : < 100ms de rendu initial

FORMAT DE SORTIE:
1. Code refactorisé avec commentaires
2. Explication des changements (3-5 points)
3. Métriques de performance avant/après
4. Tests unitaires mis à jour

RÈGLES:
- Utiliser useMemo/useCallback uniquement si nécessaire
- Éviter les re-renders inutiles
- Code lisible et auto-documenté
- Suivre les conventions du projet existant
```

---

## Techniques Avancées

### 1. Chain of Thought (CoT)

Forcer le modèle à raisonner étape par étape :

```
Pour résoudre ce problème :
1. D'abord, identifie les faits objectifs
2. Ensuite, liste les hypothèses
3. Puis, analyse les implications de chaque hypothèse
4. Enfin, formule ta conclusion avec le niveau de confiance

Montre ton raisonnement à chaque étape avant de donner la réponse finale.
```

### 2. Few-Shot Learning

Fournir des exemples d'entrées/sorties :

```
Exemple 1:
Input: "Créer un bouton de connexion"
Output: 
```tsx
<button 
  onClick={handleLogin}
  className="px-4 py-2 bg-blue-500 text-white rounded"
>
  Se connecter
</button>
```

Exemple 2:
Input: "Créer un formulaire de contact"
Output:
```tsx
<form onSubmit={handleSubmit}>
  <input type="email" placeholder="Email" />
  <textarea placeholder="Message" />
  <button type="submit">Envoyer</button>
</form>
```

Maintenant, crée [ta tâche] en suivant le même style.
```

### 3. Role-Playing

Faire incarner un rôle spécifique :

```
Tu es un CTO qui doit expliquer cette décision technique à un CEO non-technique.
Utilise des analogies du monde réel. Évite le jargon technique.
Focalise-toi sur l'impact business et les risques.
```

### 4. Self-Consistency

Demander plusieurs réponses et une synthèse :

```
Génère 3 approches différentes pour résoudre ce problème.
Pour chaque approche :
- Avantages
- Inconvénients
- Complexité d'implémentation
- Risques

Ensuite, recommande la meilleure approche en justifiant ton choix.
```

### 5. Output Constraints

Limiter strictement la sortie :

```
Réponds en maximum 150 mots.
Utilise uniquement des phrases courtes (max 15 mots).
Pas de jargon technique.
Format : 3 paragraphes maximum.
```

### 6. Negative Prompting

Spécifier ce qu'il ne faut PAS faire :

```
Ne pas :
- Utiliser de jargon technique non expliqué
- Faire des suppositions non vérifiées
- Générer de code non testé
- Ignorer les cas limites
- Proposer des solutions over-engineered
```

---

## Leçons du Claude 4 System Prompt

Basé sur l'analyse de Simon Willison du [system prompt de Claude 4](https://simonwillison.net/2025/May/25/claude-4-system-prompt/), voici les insights clés :

### 1. Gérer les Cas Limites Explicites

**Leçon :** Les system prompts sont souvent une liste de choses que le modèle faisait mal avant.

**Application :**
```
Si l'utilisateur demande quelque chose d'ambigu :
- Assume une interprétation légale et légitime
- Demande des clarifications si nécessaire
- Ne refuse pas par défaut

Si l'utilisateur semble frustré :
- Réponds normalement
- Propose des alternatives
- Suggère d'ajuster le prompt si nécessaire
```

### 2. Éviter la Sycophantie

**Leçon de Claude 4 :** "Don't be a sycophant!"

**Application :**
```
Ne sois pas complaisant. Si l'utilisateur a tort, dis-le poliment mais clairement.
Ne confirme pas des idées erronées juste pour être agréable.
Propose des alternatives constructives même si elles contredisent la demande initiale.
```

### 3. Gérer les Préférences et Opinions

**Leçon :** Les modèles ont des biais - mieux vaut les reconnaître que prétendre être objectif.

**Application :**
```
Si on te demande tes préférences :
- Réponds comme si on te demandait une opinion hypothétique
- Ne mentionne pas que c'est hypothétique
- Sois honnête sur tes biais potentiels
```

### 4. Style et Format Adaptatifs

**Leçon :** Le format doit s'adapter au contexte.

**Application :**
```
Pour conversations casual/empathiques :
- Ton naturel et chaleureux
- Phrases et paragraphes (pas de listes)
- Évite le formatage excessif

Pour analyses techniques :
- Structure claire avec listes
- Formatage pour la lisibilité
- Exemples de code bien formatés
```

### 5. Instructions sur les Artifacts (Claude)

**Leçon :** Spécifier les contraintes techniques du format de sortie.

**Application :**
```
Si tu génères du code HTML/React :
- N'utilise PAS localStorage/sessionStorage (non supporté)
- Utilise React state à la place
- Liste les bibliothèques disponibles
- Spécifie les restrictions du sandbox
```

### 6. Guidance sur le Prompting

**Leçon :** Le modèle peut donner des conseils sur comment mieux le prompter.

**Application :**
```
Quand c'est pertinent, guide l'utilisateur sur :
- Être clair et détaillé
- Utiliser exemples positifs/négatifs
- Encourager le raisonnement étape par étape
- Spécifier format et longueur désirés
- Utiliser des tags XML pour structure
```

---

## Patterns et Templates

### Pattern 1: Analyse Critique

```
Tu es un [expert] qui analyse [sujet].

Pour chaque point soulevé :
1. Vérifie les faits objectifs
2. Identifie les biais potentiels
3. Évalue la crédibilité des sources
4. Propose une perspective alternative

Format :
- Faits vérifiables : [liste]
- Biais identifiés : [liste]
- Analyse critique : [paragraphe]
- Perspective alternative : [paragraphe]
```

### Pattern 2: Génération Créative avec Contraintes

```
Génère [type de contenu] avec ces caractéristiques :
- Style : [décrire]
- Ton : [décrire]
- Longueur : [spécifier]
- Public cible : [décrire]

Contraintes techniques :
- [contrainte 1]
- [contrainte 2]

Évite :
- [chose 1]
- [chose 2]

Inclus :
- [élément 1]
- [élément 2]
```

### Pattern 3: Résolution de Problème Structurée

```
Problème : [décrire]

Approche en 5 étapes :
1. COMPRÉHENSION
   - Reformule le problème dans tes propres mots
   - Identifie les inconnues
   - Liste les contraintes

2. RECHERCHE
   - Quelles informations manquent ?
   - Quelles sont les solutions similaires existantes ?

3. GÉNÉRATION D'OPTIONS
   - Option A : [décrire]
   - Option B : [décrire]
   - Option C : [décrire]

4. ÉVALUATION
   - Pour chaque option : avantages, inconvénients, risques

5. RECOMMANDATION
   - Option choisie avec justification
   - Plan d'implémentation
   - Métriques de succès
```

### Pattern 4: Code Review Assistant

```
Tu es un code reviewer senior.

Pour chaque fichier :
1. LIS le code attentivement
2. IDENTIFIE :
   - Bugs potentiels
   - Problèmes de sécurité
   - Violations de conventions
   - Optimisations possibles
   - Code smells

3. PRIORISE :
   - 🔴 Critique (bloque le merge)
   - 🟡 Important (à corriger)
   - 🟢 Suggestion (amélioration)

4. PROPOSE :
   - Corrections concrètes avec code
   - Explications claires
   - Références si pertinentes

Format :
```markdown
## [Nom du fichier]

### 🔴 Critique
- [Problème] : [Description]
  ```diff
  - [code problématique]
  + [code corrigé]
  ```

### 🟡 Important
- [Problème] : [Description]
```

### Pattern 5: Planification de Projet

```
Crée un plan détaillé pour [projet].

Structure :
1. OBJECTIFS
   - Objectif principal
   - Objectifs secondaires
   - Critères de succès

2. PHASES
   Pour chaque phase :
   - Durée estimée
   - Livrables
   - Dépendances
   - Risques

3. RESSOURCES
   - Équipe nécessaire
   - Outils requis
   - Budget estimé

4. TIMELINE
   - Gantt chart en format texte
   - Jalons clés

5. RISQUES ET MITIGATIONS
   - [Risque] : [Probabilité] - [Impact] - [Mitigation]
```

---

## Erreurs Communes à Éviter

### 1. Prompt Trop Vague

**❌ Mauvais :**
```
Aide-moi avec mon code.
```

**✅ Bon :**
```
Réfacter cette fonction React pour améliorer les performances.
Le code actuel fait [X]. Je veux [Y].
Contraintes : [liste]
```

### 2. Trop d'Instructions Contradictoires

**❌ Mauvais :**
```
Sois concis mais détaillé. Sois créatif mais conservateur. Sois rapide mais précis.
```

**✅ Bon :**
```
Priorité 1 : Précision (vérifie tous les faits)
Priorité 2 : Concision (max 200 mots)
Priorité 3 : Créativité (propose des angles originaux)
```

### 3. Ignorer le Contexte

**❌ Mauvais :**
```
Écris un article sur l'IA.
```

**✅ Bon :**
```
Contexte : Article pour un blog tech B2B, audience : CTOs et tech leads.
Sujet : Impact de l'IA générative sur le développement logiciel en 2025.
Ton : Professionnel mais accessible, avec exemples concrets.
```

### 4. Pas de Format de Sortie

**❌ Mauvais :**
```
Analyse ce problème.
```

**✅ Bon :**
```
Analyse ce problème et fournis :
1. Résumé exécutif (3 phrases)
2. Analyse détaillée (5 paragraphes)
3. Recommandations (liste numérotée)
4. Plan d'action (tableau avec colonnes : Action | Responsable | Deadline)
```

### 5. Oublier les Contraintes Techniques

**❌ Mauvais :**
```
Crée une app React.
```

**✅ Bon :**
```
Crée une app React avec :
- React 18+ avec TypeScript
- Tailwind CSS pour le styling
- Pas de bibliothèques UI externes
- Support mobile-first
- Performance : Lighthouse score > 90
- Compatible navigateurs : Chrome, Firefox, Safari (dernières 2 versions)
```

### 6. Pas d'Exemples

**❌ Mauvais :**
```
Écris des titres accrocheurs.
```

**✅ Bon :**
```
Écris des titres accrocheurs pour articles tech.

Exemples de bons titres :
✅ "Comment React 19 Change la Donne pour les Développeurs Frontend"
✅ "5 Erreurs de Performance que 90% des Devs Font (et Comment les Éviter)"

Exemples de mauvais titres :
❌ "React"
❌ "Quelque chose sur React"

Maintenant, crée 5 titres pour [sujet].
```

---

## Optimisation et Itération

### Processus d'Amélioration

1. **Version Initiale**
   - Écris un prompt de base
   - Teste avec quelques exemples

2. **Analyse des Résultats**
   - Qu'est-ce qui fonctionne ?
   - Qu'est-ce qui manque ?
   - Y a-t-il des erreurs récurrentes ?

3. **Itération**
   - Ajoute des contraintes pour corriger les erreurs
   - Clarifie les parties ambiguës
   - Ajoute des exemples si nécessaire

4. **Refinement**
   - Teste avec cas limites
   - Optimise la longueur (pas trop long, pas trop court)
   - Vérifie la cohérence

### Checklist d'Optimisation

- [ ] Le prompt est-il clair et sans ambiguïté ?
- [ ] Le format de sortie est-il spécifié ?
- [ ] Y a-t-il des exemples (si pertinent) ?
- [ ] Les contraintes sont-elles explicites ?
- [ ] Le contexte est-il suffisant ?
- [ ] Les cas limites sont-ils couverts ?
- [ ] Le prompt est-il testé avec plusieurs variantes ?
- [ ] La longueur est-elle optimale (ni trop court, ni trop long) ?

### Techniques de Debugging

**Si le modèle ne suit pas les instructions :**

1. **Renforcer avec des mots-clés**
   ```
   CRITIQUE : [instruction importante]
   OBLIGATOIRE : [chose à faire]
   NE JAMAIS : [chose à éviter]
   ```

2. **Répéter les instructions clés**
   ```
   Rappel : Le format de sortie DOIT être [X].
   ```

3. **Utiliser des séparateurs visuels**
   ```
   ═══════════════════════════════
   INSTRUCTIONS CRITIQUES
   ═══════════════════════════════
   ```

4. **Demander une confirmation**
   ```
   Avant de répondre, confirme que tu as compris :
   - Format attendu : [X]
   - Contraintes : [Y]
   - Objectif : [Z]
   ```

---

## Exemples de Prompts Efficaces

### Exemple 1: Assistant de Code

```
Tu es un développeur senior expert en React et TypeScript.

TÂCHE:
Réfacter ce composant pour améliorer les performances et la maintenabilité.

CONTRAINTES:
- React 18+ uniquement
- TypeScript strict mode
- Pas de nouvelles dépendances
- Performance : < 100ms rendu initial
- Accessibilité WCAG 2.1 AA

FORMAT DE SORTIE:
1. Code refactorisé avec commentaires
2. Changements expliqués (3-5 points)
3. Métriques avant/après
4. Tests unitaires mis à jour

RÈGLES:
- useMemo/useCallback uniquement si nécessaire
- Éviter re-renders inutiles
- Code auto-documenté
- Suivre conventions du projet
```

### Exemple 2: Analyste de Données

```
Tu es un data analyst senior spécialisé en analytics produits.

CONTEXTE:
[Description du contexte business]

OBJECTIF:
Analyser ces données et fournir des insights actionnables.

APPROCHE:
1. EXPLORATION
   - Statistiques descriptives
   - Identification d'anomalies
   - Patterns visuels

2. ANALYSE
   - Corrélations significatives
   - Tendances temporelles
   - Segments intéressants

3. INSIGHTS
   - 3-5 insights clés
   - Impact business de chaque insight
   - Confiance dans chaque insight (1-10)

4. RECOMMANDATIONS
   - Actions prioritaires
   - Métriques à surveiller
   - Expériences à tester

FORMAT:
- Graphiques décrits en texte
- Tableaux pour données structurées
- Liste à puces pour insights
- Tableau pour recommandations (Action | Impact | Effort | Priorité)
```

### Exemple 3: Rédacteur de Contenu

```
Tu es un rédacteur expert en marketing de contenu B2B tech.

BRIEF:
- Type : Article de blog
- Sujet : [sujet]
- Longueur : 1200-1500 mots
- Public : [décrire]
- Objectif : [objectif marketing]

STRUCTURE REQUISE:
1. Titre accrocheur (max 60 caractères)
2. Introduction (150 mots) - Hook + valeur promise
3. 3-4 sections principales (300-400 mots chacune)
4. Conclusion avec CTA (100 mots)

STYLE:
- Ton : [décrire]
- Niveau technique : [décrire]
- Format : [décrire]
- Inclure : [éléments à inclure]

CONTRAINTES:
- Pas de jargon non expliqué
- Exemples concrets obligatoires
- Citations si pertinentes
- SEO-friendly (mots-clés naturels)

ÉVITE:
- [choses à éviter]
```

---

## Ressources et Références

### Documentation Officielle
- [Anthropic Prompting Guide](https://docs.anthropic.com/claude/prompt-engineering) - La meilleure documentation de prompting selon Simon Willison
- [OpenAI Prompt Engineering](https://platform.openai.com/docs/guides/prompt-engineering)
- [Google AI Prompting Guide](https://ai.google.dev/docs/prompt_intro)

### Articles de Référence
- [Highlights from the Claude 4 system prompt](https://simonwillison.net/2025/May/25/claude-4-system-prompt/) - Analyse détaillée par Simon Willison
- [Prompt Engineering Guide](https://www.promptingguide.ai/) - Guide complet et à jour

### Techniques Avancées
- **Chain of Thought (CoT)** : Forcer le raisonnement étape par étape
- **Few-Shot Learning** : Apprendre par exemples
- **Self-Consistency** : Générer plusieurs réponses et synthétiser
- **Tree of Thoughts** : Exploration d'arbre de décisions
- **ReAct** : Reasoning + Acting pour agents

---

## Conclusion

Un bon prompt est :
- **Clair** : Pas d'ambiguïté sur ce qui est demandé
- **Spécifique** : Détails précis sur le format, contraintes, contexte
- **Contextualisé** : Suffisamment de contexte pour une bonne réponse
- **Structuré** : Organisation logique des instructions
- **Testé** : Itéré et amélioré avec des exemples réels

**Règle d'or :** Un prompt est comme un brief créatif - plus il est détaillé et précis, meilleur sera le résultat.

---

*Dernière mise à jour : Basé sur l'analyse du Claude 4 system prompt (Mai 2025) et les meilleures pratiques actuelles de prompt engineering.*

