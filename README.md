# RecommendationMovie
Recommendation food Movie - Content-Based Filtering, Collaborative Filtering, Demographic Filtering

Summary:
This code implements a hybrid movie recommendation system using two main approaches: Content-Based Filtering and Collaborative Filtering (using Matrix Factorization). Below is a summary of the key steps taken:

1. Data Loading and Merging:
Two datasets, tmdb_5000_credits.csv and tmdb_5000_movies.csv, are loaded using pandas.
The two datasets are merged on the id column to combine movie metadata and credits data.
2. Weighted Rating Calculation (Content-Based Filtering):
The mean (C) of the vote_average and the 90th percentile (m) of the vote_count are calculated.
Movies with a vote_count above the 90th percentile are considered for the ranking.
A weighted rating function, based on the IMDb formula, is created to rank movies by both vote_count and vote_average.
3. Popular Movies Visualization:
A bar chart is created to visualize the top 10 most popular movies based on the popularity feature from the dataset.
4. TF-IDF Vectorization (Content-Based Filtering):
The TF-IDF (Term Frequency-Inverse Document Frequency) vectorizer is used to represent the text data (movie overviews) and remove English stop words.
The cosine similarity between movie overviews is calculated to determine movie similarity.
5. Recommendations Based on Overview:
A reverse mapping of movie indices and titles is created to find the most similar movies.
A get_recommendations function is written to retrieve the top 10 movies that are most similar to a given movie, based on the cosine similarity matrix.
6. Metadata Extraction and Cleaning:
The columns cast, crew, keywords, and genres are processed using Python’s literal_eval() to convert the JSON-like data into Python objects.
Helper functions get_director and get_list extract directors and the top 3 elements from cast, keywords, and genres.
Data cleaning is performed to format the extracted metadata (e.g., lowercasing, removing spaces).
7. Soup Creation for Content-Based Filtering:
A "soup" is created by combining metadata fields such as cast, director, keywords, and genres into a single string for each movie.
This allows for similarity matching between movies based on all these fields.
8. Count Vectorization (Content-Based Filtering):
A Count Vectorizer is applied to the "soup" of each movie to compute a new cosine similarity matrix for content-based recommendations.
A new get_recommendations function is created to recommend movies based on this enhanced similarity.
9. Collaborative Filtering using SVD (Matrix Factorization):
The SVD (Singular Value Decomposition) algorithm from the surprise library is used for collaborative filtering.
A smaller ratings_small.csv dataset is used, which contains user ratings for different movies.
The data is split into 5 folds using cross-validation, and the SVD model is trained on the full training set.
The model is used to predict ratings for users on specific movies, which allows for personalized movie recommendations.

Conclusion:
This code demonstrates a hybrid recommendation system that combines two powerful techniques:

Content-Based Filtering: By using metadata (e.g., movie overview, cast, crew, genres) and text similarity (TF-IDF and Count Vectorization), the system can recommend movies that are similar to a given movie based on content.
Collaborative Filtering: By using the SVD algorithm, the system learns from users' past ratings to recommend movies that are likely to align with the user's preferences.
Content-based recommendations can suggest similar movies based on their attributes, such as "The Dark Knight Rises" and "The Godfather".
Collaborative filtering recommendations are tailored to the user, predicting how a user would rate specific movies based on the behavior of other users with similar preferences.
By integrating both methods, the system can provide diverse and personalized recommendations, combining the strengths of each approach.
