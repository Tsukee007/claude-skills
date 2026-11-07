---
name: conformite
description: Contrôle la conformité du repo avec les bonnes pratiques Claude Code vues dans le carnet d'apprentissage, et écrit le rapport dans docs/conformite-claude.md.
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Bash(wc *), Bash(ls *)
---

Tu contrôles ce repo avec la grille ci-dessous. Réponds en français.

## Règles du contrôle
- Lecture seule : ne modifie aucun fichier du projet. Le seul fichier que tu écris est `docs/conformite-claude.md`.
- Pour chaque critère : ✅ si c'est vérifié dans le repo, ❌ sinon. Appuie chaque verdict sur ce que tu as réellement lu (fichier, ligne, commande).
- Pour chaque ❌ : propose la correction concrète en une ou deux lignes (contenu à ajouter, fichier à créer).
- N'affiche jamais un secret trouvé : indique seulement le fichier et la ligne.

## Grille

### claude-md : CLAUDE.md et mémoire projet
- c1 : un `CLAUDE.md` (ou `.claude/CLAUDE.md`) existe à la racine.
- c2 : il fait moins de 200 lignes (vérifie avec `wc -l`).
- c3 : il contient les commandes utiles : lancement en dev, build ou test, et le workflow git + déploiement.
- c4 : ses règles sont concrètes et vérifiables (pas de consignes vagues comme « code proprement »).
- c5 : il ne contient aucun secret (clé d'API, token, mot de passe, URL avec identifiants).
- c6 : `CLAUDE.local.md` est listé dans `.gitignore`.
- c7 : les fichiers de contexte du projet déjà présents à la racine sont importés avec `@chemin` plutôt que recopiés.

### slash-commands : commandes et skills
- c1 : au moins une commande projet existe dans `.claude/skills/<nom>/SKILL.md` ou `.claude/commands/<nom>.md` (en plus de celle-ci).
- c2 : chaque commande a une `description` dans son en-tête.
- c3 : les commandes qui ont des effets (déploiement, push, envoi) ont `disable-model-invocation: true`.

### subagents : sous-agents
- c1 : au moins un sous-agent existe dans `.claude/agents/`.
- c2 : chaque sous-agent a un `name` et une `description` précise de quand l'utiliser.

### hooks : hooks
- c1 : `.claude/settings.json` existe et contient une clé `hooks`.
- c2 : un hook `PreToolUse` protège les fichiers sensibles (`.env`…) ou bloque une commande dangereuse.

### mcp : serveurs MCP
- c1 : si le projet utilise des serveurs MCP, ils sont déclarés dans `.mcp.json` à la racine.
- c2 : `.mcp.json` ne contient aucun secret en dur (variables d'environnement à la place). S'il n'y a pas de `.mcp.json`, c2 est ✅.

### worktrees : worktrees
- c1 : `.claude/worktrees/` est listé dans `.gitignore`.
- c2 : un fichier `.worktreeinclude` liste les fichiers ignorés nécessaires au lancement (ex. `.env.local`).

## Rapport
1. Écris `docs/conformite-claude.md` avec : la date du jour, un tableau par thème (critère, verdict, preuve, correction), puis le score par thème (ex. `claude-md : 5/7`).
2. Termine ce fichier par le bloc ci-dessous, rempli avec tes verdicts (`true` = ✅, `false` = ❌), sans rien ajouter après :

```json
{"date":"AAAA-MM-JJ","resultats":{"claude-md":{"c1":true,"c2":true,"c3":true,"c4":true,"c5":true,"c6":true,"c7":true},"slash-commands":{"c1":true,"c2":true,"c3":true},"subagents":{"c1":true,"c2":true},"hooks":{"c1":true,"c2":true},"mcp":{"c1":true,"c2":true},"worktrees":{"c1":true,"c2":true}}}
```

3. Dans ta réponse, affiche le score par thème, les 3 corrections les plus utiles à faire en premier, et rappelle : « Copie le bloc JSON à la fin de docs/conformite-claude.md dans le carnet (Importer un rapport). »
