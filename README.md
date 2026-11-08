# Bibliothèque de skills Claude Code

Mes skills Claude Code, rangés dans un plugin que j'installe à la demande dans mes projets.

## Contenu

| Skill | Commande | Rôle |
|---|---|---|
| conformite | `/outils:conformite` | Contrôle le repo avec la grille du carnet d'apprentissage et écrit `docs/conformite-claude.md` |

## Installer dans un projet

Dans le terminal du Codespace du projet, à la racine :

```bash
claude plugin marketplace add Tsukee007/claude-skills --scope project
claude plugin install outils@tsukee-skills --scope project
git add .claude/settings.json && git commit -m "Ajoute la bibliothèque de skills" && git push
```

Le réglage est enregistré dans `.claude/settings.json` du projet : il reste valable dans chaque nouveau Codespace de ce repo. Si un nouveau Codespace ne le propose pas, relance seulement la ligne `claude plugin install`.

## Mettre à jour un projet après une modification de la bibliothèque

```bash
claude plugin marketplace update tsukee-skills
claude plugin update outils@tsukee-skills
```

Puis `/reload-plugins` dans une session ouverte.

## Ajouter un skill

1. Copie `modele-skill/SKILL.md` dans `plugins/outils/skills/<nom-du-skill>/SKILL.md`.
2. Remplis le `name` (identique au nom du dossier), la `description` et les instructions.
3. Vérifie avec `claude plugin validate .`, puis commit et push.

Règles : une description précise, des consignes vérifiables, `disable-model-invocation: true` pour tout skill qui a des effets (déploiement, envoi, push).

## Structure

```
.claude-plugin/marketplace.json      le catalogue
plugins/outils/.claude-plugin/plugin.json
plugins/outils/skills/<nom>/SKILL.md un dossier par skill
modele-skill/SKILL.md                modèle pour en créer un nouveau
```
