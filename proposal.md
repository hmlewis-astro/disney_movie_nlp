# Project Proposal
## NEED NEW TITLE

### Question & Background:
NEED AN INTRO, MOTIVATING PARAGRAPH HERE

In this project, I aim to **create a recommendation engine to make recommendations based on movies that a user has enjoyed in the past**.


### Data description:
Summaries&mdash;generally including a brief plot overview, award highlights, character names, and actor credits (longer than 100 words, on average)&mdash;for every movie produced and released by Walt Disney Pictures will be scraped from [_Disney A to Z_](https://d23.com/disney-a-to-z/). The scraped data consist of over 2100 movie titles and summaries. Note, television shows (e.g., shows on ABC, which is a Disney company) are not included in the scraped data. This website was last updated in March 2020 (around the start of the COVID-19 pandemic), so movies that have been released since then (e.g., Soul, Cruella, Luca) are not included in the scraped data.


### Tools:
To scrape the _Disney A to Z_ website, the `requests` and `BeautifulSoup` packages in Python will be utilized, along with Selenium and ChromeDriver to allow each movie summary page to fully load before scraping. The scraped data will be stored in a `.csv` file, with rows corresponding to each movie. The data will be read in to Python and manipulated using the `pandas` package.

The text processing libraries/tools in `scikit-learn` and `NLTK` will be used to clean and pre-process the movie summaries, including removing stopwords and handling special characters. These tools will also be used to tokenize, lemmatize, and vectorize the summaries, and represent the data as a document-term matrix. I will also use NMF/LDA for **topic modeling**. I plan to use the results of the topic modeling to build a very basic **recommendation system** to suggest movies similar in topic to a user's provided favorite Disney movie.


### MVP:

The minimal viable product (MVP) for this project will likely be a complete, tuned topic model. This model will then be used to create user profiles to build a recommendation system as the final product.
