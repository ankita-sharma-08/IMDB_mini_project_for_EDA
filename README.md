Here's a README file for the `IMDB_project.ipynb` notebook, based on the provided content:

# IMDB Project Analysis

This Jupyter notebook (`IMDB_project.ipynb`) performs an exploratory data analysis and preprocessing on a dataset of IMDB shows. The goal is to understand the dataset's structure, clean and transform relevant columns, and identify potential relationships between features, particularly concerning IMDB ratings.

## Table of Contents

- [IMDB Project Analysis](#imdb-project-analysis)
  - [Table of Contents](#table-of-contents)
  - [Project Overview](#project-overview)
  - [Dataset](#dataset)
  - [Notebook Structure and Key Steps](#notebook-structure-and-key-steps)
    - [1. Data Loading, Exploration and Preprocessing](#1-data-loading-exploration-and-preprocessing)
    - [2. Data Cleaning and Transformation](#2-data-cleaning-and-transformation)
    - [3. Exploratory Data Analysis (EDA) and Visualization](#3-exploratory-data-analysis-eda-and-visualization)
  - [Dependencies](#dependencies)
  - [Usage](#usage)
  - [Results and Insights (Preliminary)](#results-and-insights-preliminary)

## Project Overview

This project analyzes a dataset containing information about IMDB shows. It focuses on data cleaning, feature engineering, and initial exploratory data analysis to uncover patterns and correlations, especially those related to `imbd_rating`.

## Dataset

The analysis uses a CSV file named `shows.csv`. Based on the notebook's output, the dataset contains 250 entries and 22 columns, including:

- `rank`: Rank of the show.
- `show_id`: Unique identifier for the show.
- `title`: Title of the show.
- `year`: Release year.
- `link`: IMDB link.
- `imbd_votes`: Number of IMDB votes (initially an object type with commas).
- `imbd_rating`: IMDB rating (float).
- `certificate`: Content rating (e.g., TV-MA, TV-G).
- `duration`: Duration of the show (e.g., "4h 58m").
- `genre`: Genre(s) of the show (comma-separated).
- `cast_id`, `cast_name`, `director_id`, `director_name`, `writer_id`, `writer_name`: Information about cast, director, and writer.
- `storyline`: Brief description of the plot.
- `user_id`, `user_name`, `review_id`, `review_title`, `review_content`: User review information.

**Missing Values:**
- `certificate`: 4 missing values.
- `duration`: 1 missing value.

## Notebook Structure and Key Steps

The notebook is organized into several key steps:

### 1. Data Loading, Exploration and Preprocessing

- **Loading Data**: The `shows.csv` file is loaded into a pandas DataFrame. Robust error handling (`on_bad_lines='skip', engine='python'`) is used during CSV reading.
- **Initial Inspection**:
    - `df.info()` is used to display the DataFrame's structure, including column names, non-null counts, and data types.
    - `df.isnull().sum()` is used to identify the count of missing values for each column.
    - `df.describe(include='all')` provides descriptive statistics for all columns.
    - `df.head()` displays the first few rows of the dataset for a quick visual inspection.

### 2. Data Cleaning and Transformation

- **`imbd_votes` Cleaning**:
    - Commas are removed from the `imbd_votes` column.
    - The column is then converted to a numeric data type.
- **`duration` Transformation**:
    - A custom function `convert_duration` is defined to parse duration strings (e.g., "4h 58m", "49m") into total minutes.
    - A new column `duration_minutes` is created.
- **`genre` Multi-hot Encoding**:
    - The `genre` column, which contains comma-separated genres, is transformed into a multi-hot encoded format using `str.get_dummies(sep=',')`. This creates new binary columns for each unique genre.
    - These new genre columns are concatenated back to the main DataFrame.
- **Column Dropping**:
    - Several original columns (`title`, `certificate`, `duration`, `genre`) are dropped as they are either transformed or deemed unused for subsequent analysis.
- **Handling Remaining Missing Values**:
    - Any remaining missing values in the `df_cleaned` DataFrame are dropped using `dropna()`.
- **Correlation Analysis**:
    - A correlation matrix is calculated for all numeric columns in the `df_cleaned` DataFrame, with a specific focus on correlations with `imbd_rating`.

### 3. Exploratory Data Analysis (EDA) and Visualization

- **Scatter Plot: Votes vs IMDb Rating**:
    - A scatter plot is generated to visualize the relationship between `imbd_votes` and `imbd_rating`.
- **Distribution Plot of IMDb Ratings**:
    - A histogram with a Kernel Density Estimate (KDE) is used to show the distribution of `imbd_rating`.
- **Correlation Heatmap**:
    - A heatmap is created to visualize the correlation matrix of all numeric features, providing an overview of relationships between variables.
- **Average IMDb Rating by Genre**:
    - The top 10 most frequent genres are identified.
    - A bar plot displays the average `imbd_rating` for each of these top 10 genres.

## Dependencies

The notebook requires the following Python libraries:

- `pandas`
- `matplotlib`
- `seaborn`

You can install these using pip:
```bash
pip install pandas matplotlib seaborn
```

## Usage

1. Ensure you have Jupyter Notebook or JupyterLab installed.
2. Place the `shows.csv` file in the same directory as the `IMDB_project.ipynb` notebook.
3. Open the notebook in Jupyter:
   ```bash
   jupyter notebook IMDB_project.ipynb
   ```
4. Run all cells in the notebook to execute the analysis.

## Results and Insights (Preliminary)

The initial analysis reveals:

- **Data Overview**: The dataset contains 250 entries with various details about IMDB shows, including ratings, votes, and genre information.
- **Data Quality**: Minor missing values were found in `certificate` and `duration`, which were handled during preprocessing.
- **Feature Engineering**: `imbd_votes` was converted to numeric, `duration` was converted to minutes, and `genre` was successfully multi-hot encoded.
- **Correlations**:
    - `imbd_rating` shows a positive correlation with `duration_minutes` (0.341432) and `imbd_votes` (0.252455).
    - `Documentary` genre has a notable positive correlation (0.305172) with `imbd_rating`, suggesting documentaries in this dataset tend to have higher ratings.
    - `rank` has a strong negative correlation (-0.800248) with `imbd_rating`, which is expected as lower ranks correspond to higher ratings.
- **Visualizations**: The generated plots provide visual insights into the distribution of ratings, the relationship between votes and ratings, and average ratings across different genres.
