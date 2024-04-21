x## Data Preprocessing
<div>
  <h4>Data Formatting Adjustment:</h4>
  <ul>
    <li>Merging 2 datasets for more details</li>
    <li>Some columns stored as a string instead of a list. Using the 'ast' library to process these columns and convert them to the appropriate format.</li>
  </ul>
</div>
<div>
  <h4>Handling Missing Values:</h4>
  <ul>
    <li>Checking by calculating the percentage of missing values for each column. If the percentage of rows with missing values is less than 95% of the dataset, I am going to remove those rows.</li>
  </ul>
</div>
<div>
  <h4>Handling 0 Values:</h4>
  <ul>
    <li>Some columns such as: revenue and budget, can not retain 0 value.</li>
    <li>Examining the frequency of zero values in these columns and decide whether to impute or remove them. If the proportion of zeros in a column exceeds 5%, I'm going to fill them with the column's mean; otherwise, I may opt to eliminate rows with zero values.</li>
  </ul>
</div>
<div>
  <h4>Handling Outliers Using</h4>
  <ul>
    <li>Box Plot graph - Outliers check</li>
    <li>Using the IQR rule to identify outliers.</li>
  </ul>
</div>

## Univariate analysis 
<div>
  <h4>Numeric Variables:</h4>
  <ul>
    <li>Utilizing boxplots and histograms for:</li>
    <ul>
      <li>Detecting outliers</li>
      <li>Assessing mean and variance</li>
      <li>Understanding the distribution</li>
      <li>Checking distribution symmetry and skewness</li>
    </ul>
  </ul>
</div>
<div>
  <h4>Categorical Variables:</h4>
  <ul>
    <li>Using bar charts and pie charts for:</li>
    <ul>
      <li>Visualizing frequency distribution</li>
      <li>Identifying most common values</li>
      <li>Comparing categories</li>
      <li>Communicating findings</li>
    </ul>
  </ul>
</div>

## Hypotheis Testing
## Segmentaion and Clustering:
<div>
  <h4>Using KMeans for:</h4>
  <ul>
    <li>
      <h4>Grouping based on common characteristics:</h4>
      <ul>
        <li>Identifying film groups with common features such as genre, country of production, language, to gain a deeper understanding of audience preferences.</li>
        <li>Example: Action films, horror films, films from European countries, etc.</li>
      </ul>
    </li>
    <li>
      <h4>Predicting ratings and commercial success:</h4>
      <ul>
        <li>Discovering clusters of films that tend to receive high ratings and achieve high revenue, aiding in predicting success before film release.</li>
        <li>Example: Films highly praised by critics, films surpassing average revenue, etc.</li>
      </ul>
    </li>
    <li>
      <h4>Analyzing audience behavior:</h4>
      <ul>
        <li>Understanding viewers' movie-watching habits through variables such as viewing time, broadcast dates, access sources, to shape marketing and promotion strategies.</li>
        <li>Example: Weekend movie-watching audience, viewers preferring online platforms, etc.</li>
      </ul>
    </li>
    <li>
      <h4>Identifying trends and distinctions between film groups:</h4>
      <ul>
        <li>Distinguishing films from major production studios and independent ones, recognizing trends in the film industry.</li>
        <li>Example: Films from major studios like Disney, Warner Bros., independent films, documentaries, etc.</li>
      </ul>
    </li>
  </ul>
</div>

## Recommendation System
<div>
  <h3>Demographic Filtering</h3>
  <ul>
    <li>This code segment is used to create a Weighted Rating system for movies based on the number of ratings and the average rating score.</li>
    <li>First, computing the average rating score (C) for all movies based on the 'vote_average' column and determines the rating count threshold (m) using the 0.9 quantile of the 'vote_count' column.</li>
    <li>Then, a copy of the DataFrame movies is created, and movies with a rating count greater than or equal to the threshold m are filtered and stored in the DataFrame q_movies.</li>
    <li>A function weighted_rating(x, m, C) is defined to calculate the weighted rating score for each movie based on the given formula.</li>
    <li>The weighted_rating function is applied to each row in the DataFrame q_movies to calculate the score for each movie.</li>
    <li>Finally, the DataFrame q_movies is sorted in descending order based on the 'score' column, so that movies with the highest scores appear first.</li>
  </ul>
  <h5>RESULT</h5>
  <p>The DataFrame q_movies will contain a list of movies sorted by weighted rating, where movies with high ratings and a large number of reviews will be positioned at the top of the list. This prioritizes popular and highly rated movies when displaying results to users.</p>
  <h5>EVALUATE</h5>
  <ul>
    <li>Although this proposed method is easy to implement and understand, it may not be sensitive to the specific preferences of individual users, especially for new users of the service or when there is limited behavioral data available.</li>
    <li>Therefore, the team will proceed with transitioning to Content-Based Filtering system to provide a more personalized and accurate experience for users.</li>
  </ul>
</div>

### Content-based Filtering
<div>
  <h4>KMeans Clustering Method</h4>
  <p>In this method, the team will cluster movies based on the data in the 'genres' column.</p>
  <ol>
    <li>The team first uses MultiLabelBinarizer from the scikit-learn library to transform the 'genres' column containing multiple values into a binary matrix format to be used in the kmeans model.</li>
    <li>Dimensionality reduction is performed using the PCA method on the binary matrix created from the 'genres' column to reduce it to 2 dimensions, allowing the algorithm to work more efficiently, enhancing clustering capabilities, and providing a more intuitive representation in a 2-dimensional space.</li>
    <li>After reducing the dimensionality of the data, the team evaluates k clusters using the Silhouette method to choose the best k for the algorithm. Based on the Silhouette scores chart, the team finds that k=11 is the optimal value and proceeds to build the kmeans model.</li>
  </ol>
</div>

<div align = "center">
  ![image33](https://github.com/phuongmydha/Data-Analysis-Recommender-System-Development-for-IMDB/assets/166359916/c95b4b7e-6d3c-433e-bbbc-b2e6842d003f)
</div>
  

<div>
  <ol>
    <li> I continue to build a movie recommendation system based on the clustering model just created.
    <li>First, the presence of the movie in the DataFrame movies is checked. If the movie does not exist, the function returns a message "Movie not found." If the movie exists, its cluster is retrieved from the 'cluster' column and all movies belonging to the same cluster are filtered, retaining information about the title and genres.</li>
    <li>The selected movie is removed from the list of movies belonging to the same cluster to avoid it appearing in the recommendation list, and a DataFrame containing a list of movies belonging to the same cluster as the selected movie is returned. This is the list of movies that the system suggests users may be interested in.</li>
  </ol>
  <h5>RESULT</h5>
  <p>It can be seen that the system has provided fairly accurate recommendations for movies with similar genres.</p>
</div>

<div>
  <h4>Cosine Similarity Method</h4>
  <p>In this recommendation system, the team will use the following attributes as metadata to find correlations between movies: cast, director, keywords, genres, production_companies, overview.</p>
  <ol>
    <li>The team extracts the necessary attributes from the available columns.</li>
    <li>The team proceeds to clean the data in each extracted attribute by converting each element in each column into a lowercase string and removing whitespace.</li>
    <li>Next, the team creates soup, a string containing all the extracted metadata that the team wants to provide for vectorization. The team wants the system to prioritize director metadata more than the other metadata by tripling the weight for each row containing director metadata.</li>
    <li>The team applies a technique in NLP (Natural Language Processing) called Stemming to normalize and reduce the length of words, helping the model understand equivalent meanings of words despite potential variations in grammatical forms.</li>
    <li>The text data in the 'soup' column of the DataFrame movies is converted into a count matrix, where each row corresponds to a sample (text) and each column corresponds to a word appearing in the 'soup' column.</li>
    <li>The stop_words='english' parameter is used to remove English stop words from the text, commonly used words that often do not carry significant meaning.</li>
    <li>The purpose of creating a text count matrix is to reflect the frequency of each word's appearance in the text samples. This matrix can be used as input for machine learning models to perform tasks such as text classification, term clustering, or other tasks related to natural language processing.</li>
    <li>The team observes that there are 28,404 different words in each soup column.</li>
    <li>After creating the count matrix, the team calculates the correlation of the count matrix using the cosine_similarity function available in the sklearn library.</li>
    <li>After calculating the correlation of the count matrix, a function is built to provide movie recommendations based on similarity.</li>
  </ol>
  <h5> EVALUATE </h5>
  <ul>
    <li>This system focuses on the content of the movies, independent of user data. This is useful when there is limited user data or when users are new to the platform. </li>
    <li>Computing cosine similarity between movies can be done quickly, especially with a not overly large dataset. </lii>
    <li>However, there are still some limitations with this system. It does not utilize feedback from users, meaning it does not adjust recommendations based on user viewing behavior. </li>
    <li>Additionally, if there is not enough information in the content of the movies or if the movie dataset is not diverse, the system may struggle to generate accurate recommendations. </li>
    <li>Therefore, to achieve optimal performance, the team will consider integrating other methods such as Collaborative Filtering. </li>
  </ul>
</div>

### Collaborative Filtering- Using Itembased Filtering
