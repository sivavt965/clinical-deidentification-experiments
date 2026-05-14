# Project Notes

## Goal

The project explored clinical-note de-identification as a healthcare NLP task: given free-text medical notes, identify spans that correspond to protected health information and support downstream anonymization.

## Data Format

The upstream package expects stand-off annotations:

- `txt/`: one text document per clinical note
- `ann/`: one `.gs` annotation file per document, using the same file stem

Only the small upstream test fixtures are included here. Real clinical notes and restricted datasets must stay outside the public repository.

## Label Schemes

The included `transformer_deid/label.json` defines three useful views of the PHI task:

- Base labels: separate PHI categories such as names, locations, ages, dates, identifiers, contacts, and professions
- HIPAA-style labels: maps non-HIPAA categories away from PHI where appropriate
- Binary labels: collapses all PHI categories into a PHI/non-PHI decision

## Experiment Flow

1. Convert or organize data into the expected `txt/` and `ann/` structure.
2. Fine-tune a transformer token-classification model.
3. Evaluate token-level and entity-level behavior.
4. Compare errors across PHI categories and model architecture.
5. Keep raw data, checkpoints, and credentials out of Git.

## Public Repo Safety

The local B-disk folder contained trained transformer model weights. They are intentionally omitted here. If model artifacts are ever needed, store them in a release asset, Hugging Face model repo, or Git LFS with clear provenance and data-access constraints.
