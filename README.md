# Clean the Netflix Dataset

Learn to clean the Netflix dataset using Python and Pandas effectively.

## Project Description

In this project, I load the [Netflix Movies and TV Shows dataset](https://www.kaggle.com/datasets/shivamb/netflix-shows) from Kaggle and clean it using Pandas. The dataset has missing values, wrong data types, and mixed-type columns, which is exactly the kind of mess you find in real data.

The goal is not just to drop nulls, but to understand why values are missing and make deliberate decisions about each column.

## Project Requirements

- Download the Netflix dataset from [Kaggle](https://www.kaggle.com/datasets/shivamb/netflix-shows).
- Inspect the DataFrame with `.info()`, `.describe()`, and `.head()`.
- Identify and handle missing values column by column.
- Fix mixed-type columns (e.g., duration stored as `"90 min"`).
- Parse date columns into proper `datetime` objects.
- Export the cleaned DataFrame to a new CSV file.

## Technologies

- Python
- Pandas
- Jupyter Notebook

## Getting Started

1. Clone this repository:

   ```bash
   git clone <repository-url>
   cd netflix-data-cleaning
   ```

2. Install the dependencies:

   ```bash
   pip install -r requirements.txt
   ```

3. Open the notebook with JupyterLab and run all cells:

   ```bash
   jupyter lab netflix_data_cleaning.ipynb
   ```

The dataset is downloaded automatically with [`kagglehub`](https://github.com/Kaggle/kagglehub), so there is no need to download or unzip anything by hand.

## Project Structure

```
netflix-data-cleaning/
├── netflix_data_cleaning.ipynb   # Cleaning process, step by step
├── requirements.txt              # Project dependencies
├── README.md
├── .gitignore
└── data/
    └── clean/
        └── netflix_clean.csv     # Final cleaned dataset
```

## Cleaning Decisions

| Column | Issue | Decision | Why |
|---|---|---|---|
| `director` | ~30% missing | Filled with `"Unknown"` | Dropping those rows would lose a third of the dataset, and the rest of their data is valid |
| `cast`, `country` | ~9% missing | Filled with `"Unknown"` | Same criterion as `director`, for consistency |
| `date_added` | 10 missing, all TV shows | Kept as `NaT` | The date can't be deduced from another column, and the rest of those rows is complete |
| `date_added` | Stored as text | Parsed to `datetime`; added `year_added` and `month_added` | Enables time-based analysis |
| `duration` | Minutes and seasons mixed in one text column | Split into `duration_min` (movies) and `seasons` (TV shows); original dropped | Minutes and seasons can't be averaged together |
| `rating` / `duration` | 3 movies had their duration stored in `rating` | Moved the value to `duration`; set `rating` to `"Unknown"` | The data was in the wrong column |
| `rating` | 4 missing, plus `NR` and `UR` meaning the same | Missing filled with `"Unknown"`; `UR` unified into `NR` | A single label per meaning |

`duration_min` and `seasons` contain nulls by design: movies have no seasons and TV shows have no minutes.

## What I Practiced

- Reading a dataset before transforming it.
- Making deliberate decisions about missing values, column by column.
- Fixing mixed-type columns and converting data types.
- Parsing dates into proper `datetime` objects.
- Exporting a clean dataset ready for analysis.

## Data Source

[Netflix Movies and TV Shows](https://www.kaggle.com/datasets/shivamb/netflix-shows) by Shivam Bansal, available on Kaggle.