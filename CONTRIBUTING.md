# Contributing to ProofLedger

## Branching Strategy

On utilise des **feature branches** depuis `main`.

```
main              ← branche stable, protégée
├── feat/upload-api       ← nouvelle fonctionnalité
├── feat/ocr-service
├── fix/siret-validation  ← correction de bug
├── chore/docker-setup    ← infra, config, CI
└── docs/architecture     ← documentation
```

### Convention de nommage des branches

```
<type>/<description-courte>
```

Types : `feat`, `fix`, `chore`, `docs`, `refactor`, `test`

Exemples :
- `feat/upload-endpoint`
- `fix/ocr-pdf-crash`
- `chore/ci-pipeline`

## Commits

On suit le format [Conventional Commits](https://www.conventionalcommits.org/) :

```
<type>(<scope>): <description>
```

Exemples :
- `feat(upload): add multi-file upload endpoint`
- `fix(ocr): handle rotated PDF pages`
- `chore(docker): add MinIO service`
- `docs(readme): update getting started`

## Mettre à jour sa branche avec main

Pendant que tu travailles sur ta branche, d'autres PR peuvent être mergées dans `main`. Pour éviter les conflits au moment de ta PR, mets ta branche à jour régulièrement :

```bash
# 1. Récupérer les dernières modifs de main
git fetch origin

# 2. Se placer sur sa branche
git checkout feat/ma-feature

# 3. Rebaser sa branche sur main
git rebase origin/main
```

### En cas de conflits pendant le rebase

```bash
# Git va te montrer les fichiers en conflit
# 1. Ouvre les fichiers marqués et résous les conflits (cherche les marqueurs <<<<<<< / ======= / >>>>>>>)
# 2. Une fois résolu, ajoute les fichiers
git add <fichier-résolu>

# 3. Continue le rebase
git rebase --continue

# Si c'est trop le bazar et que tu veux annuler le rebase
git rebase --abort
```

### Après le rebase

```bash
# Ton historique local a changé, il faut force push ta branche
git push --force-with-lease origin feat/ma-feature
```

> `--force-with-lease` est plus sûr que `--force` : il vérifie que personne d'autre n'a pushé sur ta branche entre-temps.

## Pull Requests

1. Crée ta branche depuis `main` à jour : `git checkout -b feat/ma-feature main`
2. Fais tes commits en suivant la convention
3. **Mets ta branche à jour** avec `main` avant de push (voir section ci-dessus)
4. Push ta branche : `git push -u origin feat/ma-feature`
5. Ouvre une PR vers `main` en utilisant le template
6. Demande une review à au moins **1 membre** de l'équipe
7. Merge après approbation (squash merge recommandé)

## Code Review

- Vérifie que le code fonctionne (teste localement si possible)
- Vérifie la cohérence avec l'architecture existante
- Sois constructif dans tes commentaires

## Structure du projet

```
ProofLedger/
├── backend/           # API backend
├── frontend/          # Application(s) front-end
├── data/              # Scripts et config Data Lake
├── docs/              # Documentation, schémas d'architecture
├── docker/            # Dockerfiles
├── .github/           # Templates PR/issues, CI/CD
├── docker-compose.yml
├── CONTRIBUTING.md
└── README.md
```

## Setup local

À compléter une fois la stack choisie. L'objectif est que `docker-compose up` lance tout le projet.
