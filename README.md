# IHC_DATA_SORTED-

ihc-analysis/
├── data/
│   ├── sox2_prism_format.csv
│   └── pin1_prism_format.csv
├── notebooks/
│   ├── normalization_and_plots.ipynb
├── src/
│   └── quantile_normalize.py
└── README.md
import numpy as np

def quantile_normalize(m):
    """
    Perform quantile normalization on a 2D numpy array or pandas DataFrame.
    """
    sort_idx = np.argsort(m, axis=0)
    ranks = np.argsort(sort_idx, axis=0)
    sorted_cols = np.sort(m, axis=0)
    col_means = sorted_cols.mean(axis=1)
    return col_means[ranks]

from quantile_normalize import quantile_normalize
dn = quantile_normalize(df[['Sox2 H-score', 'Pin1 H-score']].values)
df_long.to_csv('data/sox2_prism_format.csv', index=False)
