## Data Preprocessing
### Data Formatting Adjustment
To obtain more comprehensive information during analysis, the team merged two datasets: Movies and Credits. The resulting dataset included the following columns:
<div align = "center">
  <img width="277" alt="Screenshot 2024-04-21 at 13 07 41" src="https://github.com/phuongmydha/Data-Analysis-Recommender-System-Development-for-IMDB/assets/166359916/ae861855-98fe-4c7c-88b6-1c00bb953c2b">
</div>

However, upon exploring the dataset attributes, the team noticed some attributes with limited analytical significance. To streamline the analysis process and expedite processing, the team removed columns lacking analytical significance.

The dataset contains numerous text-based attributes about movies. However, these columns lacked appropriate formatting; for example, the 'genres' attribute for each movie was stored as a string instead of a list. The team used the 'ast' library to process these columns and convert them to the appropriate format. The processed dataset appeared as follows:

Specifically, for the 'crew' column, only information about the 'director' was needed. After extracting from the 'crew' column, a new column 'directors' was created as follows:

### Handling Missing Values
During detailed analysis, addressing issues potentially affecting dataset quality, leading to inaccurate results, is crucial. One such issue is missing values. To address missing values, the team first examined the current dataset information:

Count the number of missing values in each column:

It appears that the number of missing values in the dataset is not substantial. To determine the threshold for removing rows with missing values, the team calculated the percentage of missing values for each column. If the percentage of rows with missing values is less than 95% of the dataset, those rows can be discarded. First, the team calculated the threshold based on the percentage, then counted the initial number of rows, and finally removed rows with a lower number of null values.

### Handling 0 Values
The dataset contains many 0 values in columns such as revenue and budget. However, theoretically, revenue, expenses (as well as some similar quantitative columns) cannot be zero. Therefore, the team investigated the number of 0 values in the columns and either filled or removed rows accordingly.

Calculate the proportion of 0 values for each column:

If the proportion of 0 values in a column is >5%, the team filled the values with the column's mean. Otherwise, rows with 0 values could be removed.
Distribution of variables after handling 0 values:

Observation: Most quantitative variables are skewed, and the majority of skewed variables require transformation.

### Handling Outliers
In addition to missing values, another factor influencing dataset quality is outliers. A box plot illustrates the data distribution, showing features such as data spread, symmetry, and outliers. However, since 'vote_average' falls within the range [0, 10], no outlier removal is performed on this variable.

Box Plot graph - Outliers check:

The team used the 3-sigma rule to identify outliers. Here, the team chose to represent overall outliers using Boxplot and print detailed rows and columns containing outliers.

A clearer representation of the dataset distribution, including data spread, symmetry, and outliers, after using the 3-sigma rule to remove outliers.
