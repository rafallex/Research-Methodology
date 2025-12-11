# TTD Analysis Pipeline for Antibiotic Susceptibility Testing

**Course:** 1MD048 Research Methodology, Uppsala University  
**Author:** Rafael Proença  
**Date:** December 2025

## Overview

This repository contains a Jupyter notebook implementing a Time-to-Detection (TTD) optimization pipeline for analyzing bacterial growth inhibition. The pipeline uses pre-computed Omnipose segmentation masks to compare control (REF) versus rifampicin-treated (RIF) *Mycobacterium smegmatis* bacteria and determines the earliest statistically valid detection of antibiotic treatment effects.

## Data

The segmentation mask data is available through **Studium** (course materials). Download and extract to a `data/` folder with the following structure:

```
data/
├── Original_data/           # Susceptible strain
│   ├── REF_raw_data.../
│   └── RIF_raw_data.../
└── HR/                      # Heteroresistant strain (optional)
    ├── HR_REF_masks/
    └── HR_RIF10_masks/
```

## Installation

```bash
pip install -r requirements.txt
```

Or install packages individually:

```bash
pip install numpy pandas matplotlib scikit-image scipy natsort
```

## Usage

1. Clone this repository
2. Download the mask data from Studium and place in a `data/` folder
3. Open `ttd_analysis.ipynb` in Jupyter Notebook or VS Code
4. Update `DATA_ROOT` in the configuration cell to point to your data folder
5. Run all cells in order
6. To switch datasets, change `DATASET_INDEX` (0 = Susceptible, 1 = HR)

## Expected Results

| Dataset | Best TTD | Method | Growth Inhibition |
|---------|----------|--------|-------------------|
| Susceptible | ~1010 min (16.8 h) | Relative diff (5%) | ~50-60% |
| Heteroresistant | ~670 min (11.2 h) | Ratio threshold (95%) | ~67% |

## Methods

The notebook implements four TTD detection methods:

1. **Relative Difference** — Detects when (REF-RIF)/REF exceeds a threshold
2. **Slope Change** — Detects divergence in growth rates using rolling regression
3. **Statistical (t-test)** — Detects statistically significant differences between conditions
4. **Ratio Threshold** — Detects when RIF/REF ratio drops below a threshold

## Output Files

The notebook generates:
- `ttd_analysis_results.png` — Main results figure
- `ttd_optimization_heatmap.png` — Parameter optimization visualization
- `mask_comparison.png` — Visual mask comparison
- `analysis_summary.csv` — Summary statistics
- `growth_timeseries.csv` — Time series data
- `ttd_optimization_results.csv` — All TTD optimization results

## License

This code is shared for educational purposes as part of the 1MD048 course reproducibility exercise.
