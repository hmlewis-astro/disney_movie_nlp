# Project Write-Up
## Disney Movie Recommender


### Abstract

The goal of this project was to create a content-based recommendation system to make a movie recommendation based on the favorite Disney movies of two different people. I utilized movie summaries from [_Disney A to Z_](https://d23.com/disney-a-to-z/) for every movie produced and released by Walt Disney Productions. The spaCy library is used for preprocessing and tokenizing the data, and the final model takes advantage of the use of anchor topics in CorEx to create a semi-supervised topic model. The model is incorporated into a recommendation system that can make recommendations based on the favorite Disney movie of one person _or_ the favorite Disney movies or two people.


### Design

While traditional TV viewing has been dropping over the course of the coronavirus pandemic, video streaming via Netflix, Hulu, Prime Video, Disney+, YouTube, etc. has increased by more than 60% (Nielsen via [Variety](https://variety.com/2020/digital/news/coronavirus-quarantine-life-media-consumption-data-increase-1203535472/)). With (nearly) the entire Disney movie catalog available on Disney+, it has become much easier to binge-watch your favorite classic Disney animated films, Pixar, and Marvel movies. However, choosing a movie to watch becomes a much more difficult task when the opinions of two (or more!) people are involved.

In this project, I created a recommendation system to make recommendations based on the favorite Disney movies of two different users. The recommendation system employs a topic model based on the written summaries of Disney movies, which will be analyzed using natural language processing.


### Data

Summaries&mdash;generally including a brief plot overview, award highlights, character names, and actor credits (longer than 100 words, on average)&mdash;for every movie produced and released by Walt Disney Pictures were scraped from [_Disney A to Z_](https://d23.com/disney-a-to-z/). The data consist of over 2100 movies, spanning films released during the 1920s (Walt Disney's _Alice Comedies_) through early 2020 (Pixar's _Onward_).

Note, this website was last updated in March 2020 (around the start of the coronavirus pandemic); movies that have been released since then (e.g., Soul, Cruella, Luca) are not included in the scraped data. Television shows (e.g., shows on ABC, which is a Disney company) are also not included in the scraped data.


### Algorithms

#### NLP
In pre-processing the data, I removed all digits and punctuation, and converted a handful of non-ascii/unicode characters to proper, ascii format. I used spaCy in order to identify named entities (e.g., characters, actors), and to remove stop words, including some custom stop words (e.g., film, video, studio, etc.). I also created a custom tokenizer to merge named entities into tokens (rather than creating n-grams), and to lemmatize all other tokens. The CountVectorizer is used, as this is the default intended to be used with the CorEx topic model.


#### Topic Model
CorEx is used for topic modeling, because it allows for the use of domain knowledge of Disney movie themes and categories to guide the model towards specific topics. The final model has 27 topics, including the following anchored topics (`anchor_strength = 3`):
- ['mickey', 'mickey mouse', 'pluto']
- ['donald', 'donald duck', 'nephew']
- ['live', 'action']
- ['academy', 'award']
- ['pooh', 'tigger', 'piglet']
- 'educational'

Below are a few of the topic-word distributions from the final model:
- **Animated movies**: voice, animate, animated, theater, imax, dvd, animation, animator, king, jim cummings
- **Award winning movies**: academy award, nominate, award, academy, best, version, winner, james algar, jiminy cricket, later
- **Romantic movies**: marry, soon, husband, parent, child, romance, sister, local, lady, happy
- **Sports movies**: high, team, coach, hope, college, school, object, double, football, building
- **Heroes vs. villains**: hero, hold, planet, mind, villain, extraordinary, earth, powerful, power, leader


#### Recommendation System
The model is incorporated into a recommendation system that can make recommendations based on the favorite Disney movie of one person _or_ the favorite Disney movies or two people.

In the case where one person provides their favorite movie, e.g., Movie A, the recommendation system calculates the cosine distance between the provided movie and all other available movies&mdash;cosine distances between Movie A and Movies B, C, D, etc.&mdash;returning the _n_ movies with the smallest distances.

In the case where the favorite movies of two people are provided, e.g., Movie A and Movie B, the recommendation system calculates the cosine distance between each movie and all other available movies&mdash;cosine distances between Movie A and Movies C, D, E, etc., and cosine distances between Movie B and Movies C, D, E, etc. The movies available for recommendation (Movies C, D, E...) are scored based on the sum of their ranked distance from each input movie. That is, if Movie C has the smallest cosine distance to Movie A (rank 1) but the third smallest cosine distance to Movie B (rank 3) it receives a score of 4 (= 1 + 3). The _n_ movies with the lowest scores are recommended to the two people. Some example recommendations are shown in the [recommendation notebook](https://github.com/hmlewis-astro/disney_movie_nlp/blob/main/recommender_d23.ipynb).

The recommender currently references movies by their index in the imported dataframe; in the future, movies will be referenced by exact matches to the title.


### Tools
- Selenium, and BeautifulSoup for web scraping
- Pandas for data exploration and text formatting
- Regex for text formatting
- Scikit-learn for vectorization of text data, topic modeling, and building and tuning the final model
- SpaCy for preprocessing, tokenizing, and lemmatizing the text data
- CorEx for topic modeling
- Matplotlib for plotting and visualizations


### Communication

In addition to the slides and visuals presented here, the write-up will be included in a forthcoming blog post. I may (in the more distant future) implement the recommendation system as a webapp for public use.
