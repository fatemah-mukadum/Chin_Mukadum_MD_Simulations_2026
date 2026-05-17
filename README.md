# Chin_Mukadum_MD_Simulations_2026

This repository contains molecular dynamics (MD) simulation setup files, selected outputs, and analysis notebooks for the manuscript "Force-modulated structural landscape of the catch bonding F-actin crosslinker alpha-actinin-4".

## Repository contents

- `analysis/CH1_CH2_500ns_Replicas.ipynb`: plots CH-domain-to-actin distance traces from 500 ns replica COLVAR output files for CH1-pointed and CH2-pointed weak-state models.
- `analysis/Map_Correlation.ipynb`: computes CryoJax map-correlation values between ACTN4 ABD coordinates from MD trajectories and the segmented weak-state cryo-EM density map.
- `CH1_pointed/`, `CH2_pointed/`, `CH1_reverseface/`, `CH2_reverseface/`: GROMACS input files, topology files, starting structures, selected run files, and selected COLVAR outputs for the tested ACTN4 ABD orientations.
- `cryo-struct/wtactn4_segmented_resampled.mrc`: segmented/resampled weak-state cryo-EM map used by the map-correlation notebook.
- `environment.yaml`: conda environment specification for running the analysis notebooks.

## System requirements

The analysis notebooks were run on the NYU HPC system.

Tested system:

- OS: Linux `6.12.0-124.52.1.el10_1.x86_64`, glibc `2.35`
- Python: `3.13.12`
- cryojax: `0.5.5`
- jax: `0.9.1`
- jaxlib: `0.9.1`
- equinox: `0.13.5`
- mdtraj: `1.11.1.post1`
- numpy: `2.4.2`
- pandas: `3.0.1`
- matplotlib: `3.10.8`
- scipy: `1.17.1`
- mrcfile: `1.5.4`
- ipykernel: `7.2.0`

The plotting notebook can be run on a normal desktop or laptop. The map-correlation notebook is more computationally demanding because it loads MD trajectories and renders per-frame simulated densities; an HPC node or workstation is recommended.

No custom compiled software is required for the analysis notebooks beyond the Python packages listed in `environment.yaml`.

## Installation guide

Install conda, then create the analysis environment from the repository root:

```bash
conda env create -f environment.yaml
conda activate actn4-md-analysis
python -m ipykernel install --user --name actn4-md-analysis --display-name "ACTN4 MD analysis"
```

Typical installation time on a normal desktop computer is expected to be approximately 10-30 minutes, depending on network speed and package solving time. Installation may take longer on shared HPC filesystems.

## Demo data and expected output

This repository includes the COLVAR files needed to run the 500 ns replica plotting analysis in `analysis/CH1_CH2_500ns_Replicas.ipynb`.

To run the demo:

```bash
conda activate actn4-md-analysis
cd analysis
jupyter notebook CH1_CH2_500ns_Replicas.ipynb
```

Run all cells in the notebook. The expected output is a plot comparing CH1-pointed and CH2-pointed orientation distance traces across four 500 ns replicas, plus a single-orientation plot for the CH2-pointed replicas. These plots reproduce the distance-trace analysis used to assess stability of candidate weak-state binding poses.

Expected runtime for this demo on a normal desktop computer is less than 5 minutes.

## Map-correlation analysis

The map-correlation notebook requires external full trajectory files that are too large for this GitHub repository. These trajectory files will be provided to reviewers through a separate Dropbox download.

After downloading the trajectory archive from Dropbox, place or symlink it as a sibling directory of this repository so that the following paths exist relative to the repository root:

```text
../Chin_Mukadum_Paper_Trajs/CH1_pointed/CH1_PE_replica3_extended_1microsecond_withwater.xtc
../Chin_Mukadum_Paper_Trajs/CH1_reverseface/CH1_PE_reverseface_1microsecond_withwater.xtc
../Chin_Mukadum_Paper_Trajs/CH2_pointed/CH2_PE_replica3_extended_1microsecond_withwater.xtc
../Chin_Mukadum_Paper_Trajs/CH2_reverseface/CH2_PE_reverseface_1microsecond_withwater.xtc
```

The notebook also uses the repository-provided cryo-EM map:

```text
cryo-struct/wtactn4_segmented_resampled.mrc
```

To run the map-correlation analysis:

```bash
conda activate actn4-md-analysis
cd analysis
jupyter notebook Map_Correlation.ipynb
```

Run the notebook cells after confirming that the trajectory paths and chain selections match the downloaded trajectories and topology PDB files. The expected output is a plot of map correlation coefficient versus simulation time for the tested ACTN4 ABD orientation(s).

Expected runtime depends on trajectory size and available CPU/GPU resources. On an HPC node, the analysis may take minutes to hours depending on the number of frames processed.

## Instructions for use on new data

To use the notebooks on new trajectories:

1. Place the trajectory file(s) in an accessible directory.
2. Update the `xtc_files`, `pdb_path`, and `labels` variables in `analysis/Map_Correlation.ipynb`.
3. Confirm the ACTN4 ABD atom selection with `mdtraj` before running the full correlation calculation.
4. Confirm that the cryo-EM map path points to the segmented/resampled map to compare against.
5. Run the notebook and inspect the correlation trace.

For the replica distance plots, add new COLVAR files under the same directory structure or update the `base_dir`, `dirs`, `replicas`, and `headers` variables in `analysis/CH1_CH2_500ns_Replicas.ipynb`.

## MD simulation files

The simulation setup files in this repository include GROMACS `.tpr`, `.mdp`, topology `.top`/`.itp`, starting PDB structures, PLUMED input files, and selected COLVAR outputs. The manuscript Methods section describes the MD protocol, including GROMACS 2023, CHARMM36, TIP3P water, 50 mM NaCl, NVT/NPT equilibration, production simulations, replica simulations, and map-correlation analysis with CryoJax.

The full production trajectories are provided externally through Dropbox because of file size.

## Code description in the manuscript

The relevant code functionality is described in the manuscript Methods section under "Molecular dynamics simulations", including the CryoJax map-correlation procedure. The analysis notebooks in this repository implement the plotting and map-correlation analysis described there.

## Repository link

GitHub repository:

```text
https://github.com/fatemah-mukadum/Chin_Mukadum_MD_Simulations_2026
```

## Notes

- The plotting demo can be run using only files in this repository.
- The map-correlation analysis additionally requires the Dropbox trajectory archive.
- The repository includes the segmented/resampled cryo-EM map required by the map-correlation notebook.
- If running on a system without GPU support, JAX should fall back to CPU execution, but runtime may be longer.

## Contact

For questions about the MD simulations or analysis notebooks, please contact the manuscript authors.
