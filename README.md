# Rocket Piston Ensemble

This repository provides a lightweight notebook for inspecting and visualizing the Rocket Piston ensemble dataset.

The full dataset is hosted on Harvard Dataverse:

- Dataset: https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/TELZAW

The paper using this data is:

- PRX Intelligence **1**, 013012, published 18 August 2026
- DOI: https://doi.org/10.1103/dldf-7tfm
- Journal page: https://journals.aps.org/prxintelligence/abstract/10.1103/dldf-7tfm

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
