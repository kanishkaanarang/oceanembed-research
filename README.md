# OceanEmbed: Satellite-Embedding-Based Reconstruction of Subsurface Ocean Temperature

Research repository for a satellite-embedding deep learning framework that reconstructs
subsurface ocean temperature at 15 standard depth levels (0-1000 m) across the North Indian
Ocean, using only surface satellite observations (SST, SSS, SSH, surface currents, surface winds).

This repository accompanies a manuscript submitted to **IGARSS 2027**. It is a research
continuation of an earlier hackathon prototype (SIH 2026); this repo contains the full,
independently reproducible research pipeline used for the paper's reported results.

## Motivation

Direct subsurface ocean measurements (Argo floats) are spatially and temporally sparse.
Satellite surface observations are continuous but do not directly observe the water column.
This project learns a compact satellite "embedding" that captures the relationship between
surface conditions and subsurface structure, validated independently against real,
never-trained-on observational data.

## Repository Structure
data/raw/ Downloaded satellite/reanalysis source files (not committed)
data/processed/ Regridded, masked, split-ready training arrays (not committed)
notebooks/ Numbered research notebooks, one per pipeline stage
src/ Reusable Python modules imported by the notebooks
results/ Generated figures, model checkpoints, and result tables
paper/ Manuscript drafts, bibliography, submission-ready figures
literature/ Annotated bibliography and related-work notes


## Notebooks

| # | Notebook | Purpose |
|---|----------|---------|
| 01 | data_ingestion | Pulls SST, SSS, SSH, currents, winds, GLORYS (target), INCOIS (validation) |
| 02 | preprocessing_and_splits | Regrids to 0.25 deg daily grid, builds ocean mask, temporal train/val/test split |
| 03 | baseline_model | XGBoost point-prediction baseline |
| 04 | deep_model_training | CNN encoder-decoder embedding model |
| 05 | incois_validation | Final independent validation against INCOIS gridded Argo |
| 06 | explainability | SHAP (baseline) and attribution analysis (deep model) |
| 07 | paper_figures_and_tables | Every figure/table used in the manuscript |

## Data Sources

| Variable | Source | Access |
|---|---|---|
| SST, SSS, SSH, GLORYS (target) | Copernicus Marine Service | `copernicusmarine` package |
| Surface currents | NASA OSCAR (PO.DAAC) | `earthaccess` package |
| Surface winds | NASA CCMP (PO.DAAC) | `earthaccess` package |
| Argo floats | International Argo Program | `argopy` package |
| Independent validation | INCOIS gridded Argo | ERDDAP |

All datasets are free and publicly accessible.

## Reproducibility

- Train/validation/test split is **temporal** (by date range, not random), testing genuine
  generalization to an unseen time period.
- The test set is used exactly once, at the end, for the number reported in the paper.
- Model checkpoints and their preprocessing configuration are saved together in
  `results/models/`.

## Setup (GitHub Codespaces)

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

## Status

Work in progress - targeting submission to IGARSS 2027 (deadline 11 January 2027).

## Citation

(To be added once the paper is accepted / preprinted.)

## License

MIT License (code). Data usage subject to each provider's own terms
(Copernicus Marine, NASA Earthdata, Argo, INCOIS).