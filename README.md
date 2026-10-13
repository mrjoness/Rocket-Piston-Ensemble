# Rocket Piston Ensemble

This repository provides a lightweight notebook for inspecting and visualizing the Rocket Piston ensemble dataset, a collection of three-dimensional multi-rocket piston simulations of inertial confinement fusion (ICF) implosions at the National Ignition Facility (NIF).

The full dataset is hosted on Harvard Dataverse:

- **Dataset:** [Rocket Piston Ensemble — Harvard Dataverse](https://doi.org/10.7910/DVN/TELZAW)

## Related publications

The dataset and its underlying methodology are associated with three publications:

### 1. Simulation model

D. T. Casey et al., *"A multi-rocket piston model to study three-dimensional asymmetries in implosions at the National Ignition Facility"* (2024).

[Journal article](https://www.sciencedirect.com/science/article/pii/S1574181824000971)

Describes the multi-rocket piston simulation model used to generate the ensemble. This is the primary reference for the underlying simulation methodology.

### 2. Simulation-based shot reconstruction

J. H. Kunimune, D. T. Casey, B. Kustowski, M. Jones, et al., *"Reconstruction of residual kinetic energy in inertial-confinement fusion implosions at the National Ignition Facility using multiple heterogeneous data sources and neural networks."* **Physical Review E 113**, 065213 (2026).

- DOI: https://doi.org/10.1103/wvj3-xd6k
- [Journal article](https://journals.aps.org/pre/abstract/10.1103/wvj3-xd6k)

Demonstrates the use of physics-based models, neural networks, and Bayesian inference to reconstruct three-dimensional implosion properties from heterogeneous experimental diagnostics. This work motivates the use of simulation-based inference for experimental shot reconstruction.

### 3. Machine learning with the Rocket Piston ensemble

M. Jones, J. Kunimune, D. Casey, B. Kustowski, E. Kur, and K. Humbird, *"Joint Diffusion Approach to Multimodal Inference in Inertial Confinement Fusion."* **PRX Intelligence 1**, 013012 (2026).

- DOI: https://doi.org/10.1103/dldf-7tfm
- [Journal article](https://journals.aps.org/prxintelligence/abstract/10.1103/dldf-7tfm)

Introduces JointDiff, a multimodal generative surrogate trained on a large ensemble of three-dimensional multi-rocket piston simulations. The model supports forward prediction, inverse inference, and reconstruction of missing simulation outputs, with applications to experimental data from NIF.

## Repository contents

- `load_ensemble.ipynb` — example notebook for loading the arrays and making sample visualizations.
- `README.md` — this overview.

The large NumPy data files are intentionally not stored in this GitHub repository. Download them from the Dataverse record above.

## Expected data layout

After downloading the dataset, place or keep the data files in a directory named `rocket_piston_simulations/` next to the notebook:

```text
rocket_piston_ensemble/
├── load_ensemble.ipynb
├── README.md
└── rocket_piston_simulations/
    ├── inputs.npy
    ├── inputs_names.npy
    ├── output_scalars.npy
    ├── output_scalars_names.npy
    ├── output_images_chunk_01_of_10.npy
    ├── ...
    └── output_images_chunk_10_of_10.npy
```

## Data summary

The notebook expects:

- `inputs.npy`: input parameters, shape `(492901, 28)`
- `inputs_names.npy`: input parameter names, shape `(28,)`
- `output_scalars.npy`: scalar simulation outputs, shape `(492901, 12)`
- `output_scalars_names.npy`: scalar output names, shape `(12,)`
- `output_images_chunk_XX_of_10.npy`: image outputs split into 10 sequential chunks; together they represent shape `(492901, 3, 2, 32, 32)`

The image chunks are memory-mapped by the notebook and loaded sample-by-sample for plotting, so the full image tensor does not need to be loaded into RAM.

## Usage

Install the minimal Python packages needed for the notebook:

```bash
pip install numpy matplotlib jupyter
```

Then open and run:

```bash
jupyter notebook load_ensemble.ipynb
```

The notebook shows:

1. Input parameter distributions
2. Scalar output distributions
3. Yield versus selected input parameters
4. Example image outputs across the yield range

## Citation

If you use this dataset in published research, please cite the [Harvard Dataverse dataset](https://doi.org/10.7910/DVN/TELZAW) and the relevant publications listed above.

In particular:

- **Simulation methodology:** Casey et al. (2024)
- **Simulation-based shot reconstruction:** Kunimune et al., *Physical Review E* (2026)
- **Machine learning and multimodal surrogate modeling:** Jones et al., *PRX Intelligence* (2026)
