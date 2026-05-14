# Clinical De-identification Experiments

Experiment workspace for NLP de-identification of free-text clinical notes using transformer-based token classification.

This repository is intentionally framed as an experiments/adaptation repo, not as original ownership of the underlying de-identification package. The included implementation in `third_party/transformer-deid/` is the MIT-licensed Transformer-DeID project by Callandra Moore, Lucas Bulgarelli, Tom Pollard, and Alistair Johnson. See `third_party/transformer-deid/LICENSE.txt` and `third_party/transformer-deid/CITATION.cff`.

## Project Scope

- Academic NLP de-identification study, August 2025 to October 2025
- Focus: identifying and masking PHI spans in clinical free-text notes
- Models considered: BERT, DistilBERT, and RoBERTa token classifiers
- Labeling modes: base PHI labels, HIPAA-style labels, and binary PHI/non-PHI labels
- Evaluation focus: token-level entity recognition behavior and de-identification quality

## What Is Included

- Upstream Transformer-DeID source code under `third_party/transformer-deid/`
- Upstream unit tests and small non-sensitive sample fixtures
- Data conversion/evaluation helper scripts from the upstream release
- Project notes describing the experiment structure and public-repo safety choices

## What Is Not Included

- No patient data
- No MIMIC or restricted clinical-note files
- No trained model weights
- No local credentials, cloud bucket names, access tokens, or notebook auth material

The original local folder contained large trained model files under `transformer_models/`. Those files are intentionally excluded because they exceed normal GitHub size limits and are not needed for a clean public portfolio repo.

## Repository Layout

```text
clinical-deidentification-experiments/
  docs/
    project-notes.md
  third_party/
    transformer-deid/
      transformer_deid/
      tests/
      README.md
      LICENSE.txt
      CITATION.cff
```

## Setup

```powershell
cd third_party/transformer-deid
conda env create -n transformer_deid --file environment.yml
conda activate transformer_deid
pytest
```

## Training Command

Transformer-DeID expects text files under `txt/` and annotation CSV files under `ann/`.

```powershell
python transformer_deid/train.py -m bert -i <dataset_path> -o <output_path> -e 5
```

Supported model values are `bert`, `distilbert`, and `roberta`.

## Planned Improvements

This repository needs regular small commits to stay useful as a portfolio project. The next changes should focus on making the experiment observable and demo-friendly:

- Add a metrics script for precision, recall, F1, and support by PHI label
- Add entity-level and token-level evaluation summaries
- Add a small inference script that accepts sample text and returns redacted text plus detected PHI spans
- Add a lightweight Streamlit demo for interactive de-identification
- Show a styled output view with highlighted PHI spans, redacted text, and a compact metrics panel
- Keep trained checkpoints and private datasets outside Git; link external artifacts only when they are safe to share

## Maintenance Plan

- Use short commits for each visible improvement rather than one large final upload
- Keep a simple changelog or README status note when metrics, inference, or demo features change
- Re-run tests after touching tokenization, labeling, or evaluation behavior
- Avoid adding any real clinical note text, patient data, credentials, or model weights to the repository

## Attribution

If you use the included Transformer-DeID code, cite the upstream project:

Moore C, Bulgarelli L, Pollard T, Johnson A. Transformer-DeID. Version 1.0.0. Released 2023-09-08.
