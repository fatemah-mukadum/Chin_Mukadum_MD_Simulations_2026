# Chin_Mukadum_MD_Simulations_2026

This repository contains MD simulation setup files, selected outputs, and analysis notebooks for the manuscript "Force-modulated structural landscape of the catch bonding F-actin crosslinker alpha-actinin-4".

## Contents

- `analysis/CH1_CH2_500ns_Replicas.ipynb`: plots CH-domain-to-actin distance traces from 500 ns replica COLVAR files.
- `analysis/Map_Correlation.ipynb`: computes CryoJax map-correlation values between ACTN4 ABD MD trajectories and the segmented weak-state cryo-EM map.
- `CH1_pointed/`, `CH2_pointed/`, `CH1_reverseface/`, `CH2_reverseface/`: GROMACS inputs, topologies, starting structures, selected run files, and selected COLVAR outputs.
- `cryo-struct/wtactn4_segmented_resampled.mrc`: segmented/resampled weak-state cryo-EM map used for map correlation.
- `environment.yaml`: conda environment for the analysis notebooks.

## Environment

The notebooks were run on the NYU HPC system with Python 3.13.12 and CryoJax 0.5.5. Other package versions are listed in `environment.yaml`.

## Trajectories

Full trajectory files are not stored in this repository because of file size. They are available from NYU Box:

https://nyu.box.com/s/kev5y3sp2tm5l3mbowaai5e81u93wqo7

## Running the notebooks

The replica notebook uses COLVAR files included in this repository. The map-correlation notebook also requires the NYU Box trajectories and `cryo-struct/wtactn4_segmented_resampled.mrc`.

## Simulation files

The repository includes GROMACS `.tpr`, `.mdp`, topology `.top`/`.itp`, PLUMED input files, starting PDB structures, selected COLVAR outputs, analysis notebooks, and the cryo-EM map used for map correlation. The manuscript Methods section describes the full MD protocol and CryoJax analysis.
