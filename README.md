# ESS563 Final Project: Temporal Evolution of Aftershock Source Properties

## Project Overview

This project analyzes the temporal evolution of source properties (corner frequency, stress drop) in aftershocks following an underground explosion using P-wave pulse shape analysis. The analysis applies trace stretching methods to geophone array recordings to estimate relative changes in earthquake source characteristics.

## Key Features

- **Multi-station waveform stacking**: Creates reference waveforms through cross-correlation-based alignment
- **Trace stretching analysis**: Quantifies relative pulse duration changes between events
- **Spectral corner frequency estimation**: Independent validation using Brune model fitting
- **Quality control framework**: Multi-criteria filtering for robust results
- **Temporal evolution tracking**: Monitors source property changes over aftershock sequences

## Data Description

- **Recording system**: 40-station surface geophone array (500 Hz sampling)
- **Event types**: Underground explosion aftershocks (Mw ~ -1 to 0)
- **Observation period**: ~1 hour following main explosion
- **Geometry**: Surface array ~250 m above source region

## Dependencies

See `requirements.txt` for Python package dependencies. Main packages:
- ObsPy (seismological data processing)
- NumPy (numerical operations)
- SciPy (signal processing, interpolation)
- Pandas (data management)
- Matplotlib (visualization)

## Installation

```bash
# Clone repository
git clone https://github.com/spri902/ESS563_FinalProject.git
cd ESS563_FinalProject

# Create conda environment (recommended)
conda env create -f environment.yml
conda activate aftershock-analysis

# OR install with pip
pip install -r requirements.txt
