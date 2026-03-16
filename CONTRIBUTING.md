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

## Pull Requests

1. Crée ta branche depuis `main` à jour : `git checkout -b feat/ma-feature main`
2. Fais tes commits en suivant la convention
3. Push ta branche : `git push -u origin feat/ma-feature`
4. Ouvre une PR vers `main` en utilisant le template
5. Demande une review à au moins **1 membre** de l'équipe
6. Merge après approbation (squash merge recommandé)

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
