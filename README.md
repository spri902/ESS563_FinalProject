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

import obspy
import pandas as pd
from aftershock_analysis import (
    extract_event_traces,
    get_reference_waveform_for_event,
    compare_waveforms_stretching,
    calculate_corner_frequency,
    analyze_temporal_evolution_robust
)

# Load data
stream = obspy.read('path/to/seismic/data')
df_picks = pd.read_csv('path/to/picks.csv')

# Get unique events
all_event_ids = get_unique_events(df_picks, sort_by_time=True)

# Select reference and comparison events
reference_event_id = all_event_ids[0]
comparison_event_ids = all_event_ids[1:51:5]  # Every 5th event

# Run temporal evolution analysis
results_df, qc_stats, ref_info = analyze_temporal_evolution_robust(
    stream, df_picks,
    reference_event_id=reference_event_id,
    comparison_event_ids=comparison_event_ids,
    pulse_window_start=0.01,
    pulse_window_end=0.04,
    stretch_max=0.50,
    min_stretch_cc=0.50,
    min_alignment_cc=0.50,
    min_snr=3.0
)

# Visualize results
plot_temporal_evolution_robust(results_df, ref_info, show_rejected=True)

# Save results
results_df.to_csv('temporal_evolution_results.csv', index=False)
