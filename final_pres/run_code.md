# How To:
### Running the code in this repo

The code for this analysis is broken into multiple pieces to avoid re-running pieces that take a significant amount of time. To produce the results presented here, run the code in the following order:

- `scrape_d23.ipynb` &mdash; [this notebook](https://github.com/hmlewis-astro/disney_movie_nlp/blob/main/scrape_d23.ipynb) scrapes movie titles and summaries from [_Disney A to Z_](https://d23.com/disney-a-to-z/); the data are written to a csv file (`movie_summaries.csv`)
- `preprocess_d23.ipynb` &mdash; the data are clean, preprocessed, tokenized, and vectorized in [this notebook](https://github.com/hmlewis-astro/disney_movie_nlp/blob/main/preprocess_d23.ipynb); various topic models are explored, and the final topic model is selected and tuned; the resulting document-topic matrix is saved to a pickle file (`doc_topic_df.pkl`) to be used in a separate notebook that will produce the recommendations
- `recommender_d23.ipynb` &mdash; [this notebook](https://github.com/hmlewis-astro/disney_movie_nlp/blob/main/recommender_d23.ipynb) presents the final recommender; users can input one or two movies to receive recommendations
  - currently, movies are referenced by their index in the dataframe; in the future, movies will be referenced by exact matches to the title
