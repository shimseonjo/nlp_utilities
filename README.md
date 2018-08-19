# NLP Utilities

Library with utility functions and wrapper classes to perform various NLP functions, including:
* Document cleaning
* Tokenization and lemmatizing
* Quick topic modeling (LSA, LDA) interface

## Installing

For now, you'll need to clone or download the repo, using:

```git clone https://github.com/seantrott/nlp_utilities.git```

Then add `nlp_utilities` to your `PYTHONPATH`, replacing `DIR` with the path to whatever directory `nlp_utilities` is stored in.

```export PYTHONPATH="{DIR}/nlp_utilties":$PYTHONPATH```

## Using NLP Utilities

### Text cleaning and tokenization

The `TextCleaner` module has several simple scripts for cleaning and tokenizing documents for the purpose of topic modeling, sentiment analysis, word2vec modeling, and more.

Under the hood this mostly consists of `BeautifulSoup`, `regex`, and `nltk`, but the purpose of `TextCleaner` is to bundle all these together for easy use.

```
from nlp_utilities import TextCleaner

text = '<b>Webpage title.</b>Something else http://somelink.com www.link link.org'
TextCleaner.remove_hyperlinks(text)
TextCleaner.strip_html(text)
```

Or use the `TextCleaner.clean(...)` utility method to bundle these methods into a single call:

```
TextCleaner.clean(text)
```

#### Preprocessing

You can also turn a document into a list of word tokens using `tokenize_words`. This requires instantiating `TextCleaner`.

```
tc = TextCleaner()
tc.tokenize_words('the quick brown fox', remove_stops=True)
```


### Topic Modeling

NLP Utilities has a wrapper class for topic modeling, using either Latent Semantic Analysis (LSA) or Latent Dirichlet Allocation (LDA). Using either is straightforward:

```
from nlp_utilities import TopicModeler

example_documents = ['the cat ate the mouse',
                     'the man ate the pie',
                     'birds like to eat pies',
                     'the bird ate the mouse']
tm = TopicModeler(transformer_name='lsa', num_topics=3)

tm.fit(example_documents)
topics = tm.transform(example_documents)

```

Instead of using `fit` and `transform` separately, you can also use `fit_transform` directly:

```
topics = tm.fit_transform(example_documents)
```

## To do

Add utilities for:
* Document classification
* Sentiment analysis
* LWIC
