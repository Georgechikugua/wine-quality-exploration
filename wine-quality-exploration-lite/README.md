# Wine Quality Exploration

This is a small exploratory data analysis project based on the white wine subset of the UCI Wine Quality dataset. It follows a simple workflow from data auditing and visualization to feature standardization, KMeans clustering, and interpretation.

## Research Questions

1. What are the main relationships among the physicochemical features?
2. What cluster structure can KMeans identify after feature standardization?
3. If `quality` is excluded from clustering, do the resulting clusters show different quality distributions?

## Dataset

The analysis uses 4,898 white wine samples. Each sample contains 11 physicochemical measurements and one sensory quality score. The score ranges from 0 to 10 in the dataset description, although the observed white wine scores range from 3 to 9.

The `quality` variable is excluded from the KMeans input features and is used only after clustering to compare the resulting groups.

The data files and original description are stored in `data/wine-quality/`. The red wine file is retained as part of the original dataset download but is not used in this notebook.

## Main Findings

- Residual sugar and density have a strong positive correlation (`r ≈ 0.84`), while alcohol and density have a strong negative correlation (`r ≈ -0.78`).
- Among the tested values from `k=2` to `k=8`, `k=2` has the highest silhouette score. The score is still fairly low (`≈ 0.21`), so the clusters are useful descriptive profiles rather than clearly separated natural groups.
- One cluster has relatively higher residual sugar, density, and sulfur dioxide, while the other has relatively higher alcohol and pH.
- About 29.8% of the lower-sugar, higher-alcohol cluster has a quality score of 7 or above, compared with about 9.4% of the other cluster. Both clusters still have a median quality score of 6, so they should not be treated as simple “high-quality” and “low-quality” groups.

## Project Structure

```text
wine-quality-exploration/
├── data/
│   └── wine-quality/
│       ├── winequality-red.csv
│       ├── winequality-white.csv
│       └── winequality.names
├── figures/
├── notebooks/
│   └── 01_data_exploration.ipynb
├── .gitignore
├── README.md
└── requirements.txt
```

## Python Environment

The project was developed with Python 3.12. The main dependencies are:

- pandas
- matplotlib
- scikit-learn
- ipykernel

To create a local environment and open the notebook:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook notebooks/01_data_exploration.ipynb
```

On Windows, activate the environment with `.venv\Scripts\activate` instead. The `.venv` directory is intentionally excluded from Git because each user can recreate it from `requirements.txt`.

## Limitations

- KMeans results depend on feature scaling, the chosen number of clusters, and the assumption that clusters can be represented by distances from their centers.
- The relatively low silhouette score indicates substantial overlap between the two clusters.
- The quality scores are imbalanced and are based on sensory evaluations.
- The threshold `quality >= 7` is a practical summary used in this analysis, not an official definition of high-quality wine.
- The dataset contains 937 duplicated rows. They are retained because there are no sample identifiers, so identical measurements cannot be confidently classified as accidental duplicates.
- The results describe associations in this dataset and do not establish causal relationships.

## Data Source

P. Cortez, A. Cerdeira, F. Almeida, T. Matos, and J. Reis (2009). “Modeling wine preferences by data mining from physicochemical properties.” *Decision Support Systems*, 47(4), 547–553. [https://doi.org/10.1016/j.dss.2009.05.016](https://doi.org/10.1016/j.dss.2009.05.016)

This is a learning-oriented exploratory project rather than a novel research contribution.
