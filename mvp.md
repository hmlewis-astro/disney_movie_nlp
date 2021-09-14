# Minimum Viable Product
## Disney Movie Marathon: What are we watching next?

The goal of this project is to create a recommendation system to make a movie recommendation based on the favorite Disney movies of two different users.

To do this, I am using movie summaries from [_Disney A to Z_](https://d23.com/disney-a-to-z/)&mdash;which generally include a brief plot overview, award highlights, character names, and actor credits (longer than 100 words, on average)&mdash;for every movie produced and released by Walt Disney Productions. The data consist of over 2100 movies, spanning films released during the 1920s (Walt Disney's _Alice Comedies_) through early 2020 (Pixar's _Onward_).

In pre-processing the data, I removed all digits and punctuation, I used spaCy in order to identify named entities (e.g., characters, actors), and to remove stop words. I also created a custom tokenizer to merge named entities into a single token, and to lemmatize all other tokens.

To begin building a topic model, I created a few baseline models using the `CountVectorizer` and `TfidfVectorizer`, with an `NMF` topic modeler and a small number of topic components (_n_ = 10); however, because large portions of the corpus are made up of extensive film _series_ featuring the same characters/themes (e.g., the _Alice Comedies_, Mickey Mouse and friends, several educational and safety series), `CorEx`, which allows "anchoring" of topic words, for semi-supervised topic modeling, can push the topic model towards these specific, previously identified subsets of words/characters.

I have opted to tune a model using the `CountVectorizer` and a `CorEx` topic model. Though I am continuing to tune the number of topics to use in this model, I have determined some important anchors to separate topics, including:
- `['mickey', 'mickey mouse', 'pluto', 'silly', 'symphony']`
- `['donald', 'donald duck', 'nephew']`
- `['oswald', 'lucky', 'rabbit']`
- `['educational']`
- `['pooh', 'piglet', 'eeyore']`

With only minimal tuning of the anchor strength

I will continue to...
