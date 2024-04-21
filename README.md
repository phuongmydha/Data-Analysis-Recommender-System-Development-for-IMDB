### Data Preprocessing
<div>
  <h4>Data Formatting Adjustment:</h2>
  <ul>
    <li>Merging 2 datasets for more details</li>
    <li>Some columns stored as a string instead of a list. Using the 'ast' library to process these columns and convert them to the appropriate format.</li>
  </ul>
</div>
<div>
  <h4>Handling Missing Values:</h2>
  <ul>
    <li>Checking by calculating the percentage of missing values for each column. If the percentage of rows with missing values is less than 95% of the dataset, I am going to remove those rows.</li>
  </ul>
</div>
<div>
  <h4>Handling 0 Values:</h2>
  <ul>
    <li>Some columns such as: revenue and budget, can not retain 0 value.</li>
    <li>Examining the frequency of zero values in these columns and decide whether to impute or remove them. If the proportion of zeros in a column exceeds 5%, I'm going to fill them with the column's mean; otherwise, I may opt to eliminate rows with zero values.</li>
  </ul>
</div>
<div>
  <h4>Handling Outliers Using</h2>
  <ul>
    <li>Box Plot graph - Outliers check</li>
    <li>Using the IQR rule to identify outliers.</li>
  </ul>
</div>
