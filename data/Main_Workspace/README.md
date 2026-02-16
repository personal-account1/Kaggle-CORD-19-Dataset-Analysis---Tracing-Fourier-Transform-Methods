# Tracing Fourier-Transform Methods in CORD-19 Literature

This repository analyzes how Fourier-transform–based structural-biology methods (for example, X-ray crystallography and electron diffraction) are described and used in the COVID-19 literature, with a focus on papers that investigate the SARS‑CoV‑2 spike protein. The analysis uses the CORD‑19 dataset to perform document classification, temporal trend analysis, and interpretable NLP to identify method-specific vocabulary and timelines.

## Table of Contents
- Project overview
- Goals and hypotheses
- Dataset
- Methods and pipeline
- Getting started
- Repository structure
- Results and reproducibility
- Contributing
- License and contact

## Project Overview
This project seeks to quantify and interpret the textual footprint of Fourier-transform–based methods in COVID‑19 publications. By identifying and classifying papers that discuss crystallography / diffraction / electron density workflows applied to the SARS‑CoV‑2 spike protein, we aim to:

- Measure when and how structural-method papers appeared during the pandemic.
- Build an NLP classifier to identify method-focused literature.
- Extract interpretable terms and phrases that characterize the structural biology workflow.

## Goals and Hypotheses
- Hypothesis: Papers discussing spike‑protein structure and Fourier/X‑ray methods use a distinct vocabulary and cluster temporally (e.g., concentrated early in the pandemic).
- Evaluation target: a classifier with precision and recall > 0.75 on held‑out abstracts for the “structural-method” label, and a set of interpretable features/terms mapping to crystallography concepts (e.g., "diffraction", "electron density", "R‑factor").

## Dataset
Primary source: the Allen Institute's CORD‑19 corpus (metadata, abstracts, and full‑text where available). The pipeline ingests CORD‑19 metadata, filters documents by relevance (spike protein, structural methods), and constructs labeled datasets for training and evaluation.

## Methods and Pipeline
- Data ingestion: load and normalize CORD‑19 metadata and full texts.
- Filtering & labeling: identify candidate papers using keyword rules and manual curation to produce training labels for "structural‑method".
- Feature extraction: tokenization, TF‑IDF, n‑grams, and domain‑specific phrase extraction; optional embeddings for deeper analysis.
- Modeling: baseline classifiers (Logistic Regression, Random Forest) and modern text models as appropriate.
- Interpretation: feature importance, SHAP or similar methods, and temporal trend plots to visualize method adoption and discussion over time.

## Getting Started
Prerequisites
- Python 3.9+ (recommended)
- Typical libraries: pandas, scikit‑learn, nltk/spacy, gensim, matplotlib/seaborn, jupyter

Quickstart
1. Clone the repository.
2. Place the CORD‑19 dataset files (metadata and full text) in the `data/` directory (create it if missing).
3. Create a Python virtual environment and install dependencies (example):

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

4. Run the ingestion script (example):

```bash
python scripts/ingest_cord19.py --data-dir data/ --out data/processed/
```

5. Run the analysis notebook or scripts found in `notebooks/` and `scripts/`.

## Repository Structure
- `data/` — raw and processed datasets (not tracked in VCS)
- `notebooks/` — exploratory analysis and figures
- `scripts/` — ingestion, labeling, training, and evaluation scripts
- `results/` — generated outputs, models, and figures
- `requirements.txt` — Python dependencies
- `README.md` — this file

Adjust paths and filenames in scripts to match your local layout.

## Results and Reproducibility
- The repository includes notebooks that reproduce the main EDA figures and classification results.
- Save trained models and evaluation artifacts to `results/` and record experiment metadata (hyperparameters, data splits).

Recommendations for reproducibility
- Pin dependency versions in `requirements.txt`.
- Use fixed random seeds and document data filtering steps.

## Contributing
- If you want to contribute: open an issue describing your proposed change, fork the repository, and submit a pull request.
- For dataset additions or sensitive changes, include a short note explaining the provenance and any preprocessing applied.

## License and Contact
Specify license information here (e.g., MIT, CC BY). For questions or collaboration requests, open an issue or contact the repository owner.

----
If you’d like, I can: add a `requirements.txt`, scaffold `scripts/ingest_cord19.py`, or convert exploratory notebooks into runnable pipelines. Tell me which next step you prefer.

## Workspace & Data (data/Main_Workspace)
This repository includes a `data/Main_Workspace` folder with collected artifacts used for the CORD‑19 analysis. Current contents (as committed) include:

- `data/Main_Workspace/metadata.csv` — large CORD‑19 metadata CSV (≈ 980 MB)
- `data/Main_Workspace/transformer_model_complete.pth` — pretrained model weights (≈ 267 MB)
- `data/Main_Workspace/Updated CORD-19 Analysis.ipynb` — analysis notebook used for EDA & figures
- `data/Main_Workspace/CORD-19 Presentation (Final).pptx` — presentation file
- `data/Main_Workspace/metadata.readme` — short notes about the metadata file

Extraction note: these files were originally uploaded as a ZIP and extracted into the repository workspace (see `data/`); the large binary and CSV were retained for analysis.

Git LFS migration and push status
- The large binary files above exceed typical GitHub soft limits and were migrated to Git LFS to keep the repository healthy.
- The repository history was rewritten using `git lfs migrate import --include="*.pth,*.csv"` and the cleaned `main` branch was force-pushed to the remote. The LFS objects were uploaded successfully.

