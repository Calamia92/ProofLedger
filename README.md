# ProofLedger

Plateforme de vérification et de gestion de documents comptables.

## Fonctionnalités

- **Upload multi-documents** — Import de pièces comptables sensibles (factures, devis, attestations SIRET, URSSAF, Kbis, RIB)
- **Classification automatique** — Catégorisation intelligente via NLP/NER
- **Extraction OCR** — Extraction des informations clés (SIREN/SIRET, montants HT/TTC/TVA, dates…)
- **Vérification intelligente** — Détection d'incohérences inter-documents et de fraude potentielle
- **Architecture Data Lake (Medallion)** — Stockage structuré en zones Bronze / Silver / Gold sur MinIO
- **Orchestration Airflow** — Pipeline DAG automatisé (ingestion → OCR → extraction → validation)
- **Front-ends métiers** — CRM fournisseur et outil de conformité avec auto-remplissage IA

## Stack technique

| Composant | Technologie |
|-----------|-------------|
| Frontend | React (MERN) |
| Backend | Node.js / Express (MERN) |
| Base de données | MongoDB (MERN) |
| OCR | Tesseract / EasyOCR |
| NLP / NER | spaCy / Transformers |
| Data Lake | MinIO (compatible S3) |
| Orchestration | Apache Airflow |
| Dataset | Faker (Python) + API SIRENE INSEE |
| Conteneurisation | Docker / Docker Compose |

## Architecture

```
┌──────────────┐     ┌──────────────────┐     ┌──────────────────┐
│   Frontend   │────▶│   Backend API    │────▶│   MinIO (S3)     │
│   (React)    │◀────│   (Express)      │◀────│                  │
│              │     │                  │     │  Bronze (raw)    │
│  - Upload    │     └────────┬─────────┘     │  Silver (clean)  │
│  - CRM       │              │               │  Gold  (curated) │
│  - Conformité│     ┌────────▼─────────┐     │                  │
│              │     │   Airflow (DAG)  │────▶│                  │
└──────────────┘     │                  │     └──────────────────┘
                     │  OCR → NER →     │
                     │  Validation →    │     ┌──────────────────┐
                     │  Auto-fill       │────▶│   MongoDB        │
                     └──────────────────┘     └──────────────────┘
```

### Pipeline de traitement (DAG Airflow)

```
Document uploadé
    │
    ▼
[ Bronze ] Stockage brut (MinIO raw-zone)
    │
    ▼
[ OCR ] Extraction du texte (Tesseract)
    │
    ▼
[ Classification ] NLP → Facture / Devis / Attestation / Kbis / RIB
    │
    ▼
[ NER ] Extraction d'entités (spaCy) → SIRET, montants, dates…
    │
    ▼
[ Silver ] Données nettoyées + JSON structuré (MinIO clean-zone)
    │
    ▼
[ Vérification ] Cohérence inter-documents, détection anomalies
    │
    ▼
[ Gold ] Données enrichies (MinIO curated-zone)
    │
    ├──▶ Auto-remplissage CRM
    └──▶ Auto-remplissage Outil de conformité
```

## Getting Started

### Prérequis

- Docker & Docker Compose
- Git
- Node.js (pour le dev frontend/backend)
- Python 3.x (pour Airflow, OCR, NER, génération de dataset)

### Installation

```bash
git clone https://github.com/Calamia92/ProofLedger.git
cd ProofLedger
docker-compose up
```

## Gestion de projet

- **Backlog & Planning** : [ProofLedger's Backlog](https://github.com/users/Calamia92/projects/9)
- **Conventions** : voir [CONTRIBUTING.md](./CONTRIBUTING.md)

### Planning

| Jour | Date | Focus |
|------|------|-------|
| J1 | Lun 16/03 | Setup, architecture, conception pipeline Airflow |
| J2 | Mar 17/03 | Backend core, MinIO, upload, OCR, DAG Airflow |
| J3 | Mer 18/03 | NER, classification, vérification, dataset Faker |
| J4 | Jeu 19/03 | Front-ends, auto-remplissage, Gold, monitoring |
| J5 | Ven 20/03 | Oral (25min + 15min Q&A) |

### Milestones

| Milestone | Description |
|-----------|-------------|
| M1 - Infrastructure & Setup | Init repo, CI/CD, Docker, conventions |
| M2 - Upload Multi-Documents | API upload, stockage, interface |
| M3 - Classification Automatique | Classification NLP des documents |
| M4 - Extraction OCR | Tesseract + NER spaCy |
| M5 - Vérification & Détection | Moteur de règles, détection d'incohérences |
| M6 - Data Lake / Medallion | MinIO : Bronze / Silver / Gold |
| M7 - Front-ends Métiers | CRM + outil de conformité + auto-remplissage |
| M8 - Orchestration Airflow | Pipeline DAG, monitoring, logs |

### Répartition des rôles

| Rôle | Responsabilités |
|------|----------------|
| Dataset (M1) | Génération dataset Faker + API SIRENE, scans bruités |
| OCR & Extraction (M1) | Tesseract, pipeline OCR, NER spaCy, JSON structuré |
| Front + API (M1) | Interface React, formulaires dynamiques, API Express |
| Data Lake (M2) | MinIO, zones Raw/Clean/Curated, sécurisation |
| Validation (M2) | Détection incohérences SIRET/TVA/dates, anomaly detection |
| Orchestration (M2) | Airflow DAG, monitoring, auto-remplissage |

## Contribuer

Voir [CONTRIBUTING.md](./CONTRIBUTING.md) pour les conventions de branching, commits et pull requests.
