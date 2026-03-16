# ProofLedger

Plateforme de vérification et de gestion de documents comptables.

## Fonctionnalités

- **Upload multi-documents** — Import de pièces comptables sensibles (factures, devis, attestations…)
- **Classification automatique** — Catégorisation intelligente des documents uploadés
- **Extraction OCR** — Extraction des informations clés (SIREN/SIRET, montants, dates…)
- **Vérification intelligente** — Détection d'incohérences et de documents potentiellement frauduleux
- **Architecture Data Lake (Medallion)** — Stockage structuré en zones Bronze / Silver / Gold
- **Front-ends métiers** — CRM fournisseur et outil de conformité

## Architecture

```
┌──────────────┐     ┌──────────────────┐     ┌──────────────────┐
│   Frontend   │────▶│   Backend API    │────▶│    Data Lake      │
│  (Upload,    │◀────│  (REST API)      │◀────│                  │
│   CRM,       │     │                  │     │  Bronze (raw)    │
│   Conformité)│     │  - Upload        │     │  Silver (clean)  │
│              │     │  - OCR           │     │  Gold  (curated) │
│              │     │  - Classification│     │                  │
│              │     │  - Vérification  │     │                  │
└──────────────┘     └──────────────────┘     └──────────────────┘
```

### Pipeline de traitement

```
Document uploadé
    │
    ▼
[ Bronze ] Stockage brut (PDF/image + métadonnées)
    │
    ▼
[ OCR ] Extraction du texte
    │
    ▼
[ Classification ] Facture / Devis / Attestation / ...
    │
    ▼
[ Silver ] Données nettoyées + champs extraits (SIREN, montants, dates…)
    │
    ▼
[ Vérification ] Cohérence intra/inter-documents, détection de fraude
    │
    ▼
[ Gold ] Données enrichies → CRM + Outil de conformité
```

## Stack technique

À définir avec l'équipe (voir [issue #1](https://github.com/Calamia92/ProofLedger/issues/1)).

## Getting Started

### Prérequis

- Docker & Docker Compose
- Git

### Installation

```bash
git clone https://github.com/Calamia92/ProofLedger.git
cd ProofLedger
docker-compose up
```

> La configuration Docker sera mise en place dans l'[issue #4](https://github.com/Calamia92/ProofLedger/issues/4).

## Gestion de projet

- **Backlog & Planning** : [ProofLedger's Backlog](https://github.com/users/Calamia92/projects/8)
- **Conventions** : voir [CONTRIBUTING.md](./CONTRIBUTING.md)

### Planning

| Jour | Date | Focus |
|------|------|-------|
| J1 | Lun 16/03 | Setup, architecture, choix techniques |
| J2 | Mar 17/03 | Backend core (upload, bronze, OCR) |
| J3 | Mer 18/03 | Intelligence (classification, parsing, vérification) |
| J4 | Jeu 19/03 | Front-ends, gold, intégration |
| J5 | Ven 20/03 | Oral |

### Milestones

| Milestone | Description |
|-----------|-------------|
| M1 - Infrastructure & Setup | Init repo, CI/CD, Docker, conventions |
| M2 - Upload Multi-Documents | API upload, stockage, interface |
| M3 - Classification Automatique | Service de catégorisation des documents |
| M4 - Extraction OCR | OCR + parsing des champs clés |
| M5 - Vérification & Détection | Moteur de règles, détection d'incohérences |
| M6 - Data Lake / Medallion | Architecture Bronze / Silver / Gold |
| M7 - Front-ends Métiers | CRM fournisseur + outil de conformité |

## Contribuer

Voir [CONTRIBUTING.md](./CONTRIBUTING.md) pour les conventions de branching, commits et pull requests.

## Équipe

À compléter.
