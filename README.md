# IMDB show reating mini porject Exploratory Data Analysis

This repository contains a Jupyter Notebook (`EDA_IMDB_mini_Project.ipynb`) that performs Exploratory Data Analysis (EDA) on a dataset of IMDB shows. The analysis aims to understand the characteristics of the dataset, identify relationships between different features, and visualize key insights.

## Dataset

The analysis uses a CSV file named `shows.csv`. This file is expected to be in the same directory as the Jupyter Notebook. The `pd.read_csv` function is configured with `on_bad_lines='skip'` and `engine='python'` for robust error handling during data loading.

## Notebook Contents

The Jupyter Notebook `EDA_IMDB_mini_Project.ipynb` includes the following sections:

- **Library Imports**: Imports necessary libraries such as `pandas`, `matplotlib.pyplot`, `seaborn`, and `numpy`.
- **Data Loading**: Reads the `shows.csv` file into a pandas DataFrame.
- **Initial Data Inspection**: Displays the first 10 rows of the DataFrame (`df.head(10)`), provides a concise summary of the DataFrame (`df.info()`), and generates descriptive statistics for all columns (`df.describe(include = 'all')`).
- **Missing Values Check**: Identifies and counts missing values in each column (`df.isnull().sum()`).
- **Data Cleaning and Preprocessing**:
    - **`imbd_votes`**: Removes commas and converts the column to a numeric data type.
    - **`duration`**: Converts the 'Xh Ym' format into total minutes and stores it in a new column `duration_minutes`.
    - **`genre`**: Splits the comma-separated genre strings into a multi-hot encoded format using `str.get_dummies()`.
    - **Column Dropping**: Removes original `title`, `certificate`, `duration`, and `genre` columns, as well as other potentially unused columns (`df_cleaned = df.drop(columns=['title', 'certificate', 'duration', 'genre'])`).
    - **Missing Value Handling**: Drops any remaining rows with missing values (`df_cleaned = df_cleaned.dropna()`).
- **Correlation Analysis**: Calculates the correlation matrix for numeric columns and specifically examines the correlation of `imbd_rating` with other features.
- **Visualizations**: Generates several plots to explore the data.

## Key Features Analyzed

- `rank`: Rank of the show.
- `show_id`: Unique identifier for the show.
- `title`: Title of the show.
- `year`: Release year.
- `link`: IMDB link to the show.
- `imbd_votes`: Number of IMDB votes.
- `imbd_rating`: IMDB rating of the show.
- `certificate`: Content rating/certificate.
- `duration`: Duration of the show (original format).
- `duration_minutes`: Duration converted to minutes (newly engineered feature).
- `genre`: Genre(s) of the show (original and multi-hot encoded).
- `cast_id`, `cast_name`: Information about the cast.
- `director_id`, `director_name`: Information about the director(s).
- `writer_id`, `writer_name`: Information about the writer(s).
- `storyline`: Brief description of the show's plot.
- `user_id`, `user_name`, `review_id`, `review_title`, `review_content`: User review information.

## Analysis Steps

1.  **Load Data**: The `shows.csv` file is loaded into a pandas DataFrame.
2.  **Initial Overview**: `df.head()`, `df.info()`, and `df.describe()` are used to get a quick understanding of the data structure, data types, and basic statistics.
3.  **Handle Missing Values**: Missing values in `certificate` and `duration` are identified. `certificate` and `duration` are dropped after `duration` is processed into `duration_minutes`. Any remaining missing values are handled by dropping the corresponding rows.
4.  **Data Type Conversion**: `imbd_votes` is converted from string (with commas) to numeric. `duration` is converted to `duration_minutes` (integer).
5.  **Feature Engineering (Genre)**: The `genre` column, which contains comma-separated values, is transformed into a multi-hot encoded format, creating new columns for each unique genre.
6.  **Correlation Analysis**: A correlation matrix is computed for all numeric columns to understand the relationships between them, with a specific focus on `imbd_rating`.
7.  **Data Visualization**: Various plots are generated to visualize distributions and relationships.

## Visualizations

The notebook generates the following plots:

-   **Scatter plot: Votes vs IMDb Rating**: Visualizes the relationship between the number of IMDB votes and the IMDB rating.
-   **Distribution plot of IMDb Ratings**: A histogram with a Kernel Density Estimate (KDE) to show the distribution of IMDB ratings across the dataset.
-   **Correlation heatmap of Numeric Features**: A heatmap displaying the correlations between all numeric features in the cleaned dataset.
-   **Average IMDb Rating by Top 10 Genres**: A bar plot showing the average IMDB rating for the top 10 most frequent genres.

## How to Run the Notebook

1.  **Clone the repository**:
    ```bash
    git clone https://github.com/ankita-sharma-08/IMDB_mini_project_for_EDA.git
    cd IMDB_mini_project_for_EDA
    ```
    Or just download the 'EDA_IMDB_mini_Project.ipynb' Jupyter Notebook
2.  **Ensure you have the dataset**: Place `shows.csv` in the root directory of the cloned repository.
3.  **Install dependencies**: It's recommended to use a virtual environment.
    ```bash
    pip install pandas matplotlib seaborn numpy
    ```
4.  **Open the Jupyter Notebook**:
    ```bash
    jupyter notebook EDA_IMDB_mini_Project.ipynb
    ```
5.  **Run all cells**: Execute all cells in the notebook to see the analysis and visualizations.

## Dependencies

-   `pandas`
-   `matplotlib`
-   `seaborn`
-   `numpy`
