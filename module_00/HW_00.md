---
jupytext:
  formats: md:myst,ipynb
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.4
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
---

```{code-cell} ipython3
import numpy as np
import matplotlib.pyplot as plt
plt.style.use('fivethirtyeight')
import pandas as pd
```

# HW_00 - Generative AI writing analysis

In this assignment, you will generate instructions on brushing your teeth. You can use [ChatGPT](https://chatgpt.com/)

Some metrics to add to the generated instructions:

- number of strokes per minute
- total brushing time
- time spent per tooth 
- number of teeth or total area to brush on teeth
- deflection of brush bristles for proper cleaning
- what else can you think of?

+++

## Prompt Input and Output

-> _copy-paste your prompts and outputs here_

this is a test   _!_!_!_!_!_!!_!_!_!_!_!!!!1!_!_!-!-1!!!_!__!___!__!_!

+++

## Revised document

-> _copy-paste the document here, then edit the output to remove passive phrasing and add specific ideas from your own research or experience (try quantifying any phrases such as 'many', 'fewer', 'more important', etc._

Another TEST

+++

## Document analysis

- Make a list of all the improvements and changes you made to document
- use the `tf_idf.cosineSimilarity` function to compare the AI version to your own

Write a report on your intellectual property  in the 'revised document'. 
- How much can you claim as yours?
- How many ideas came from AI?
- How many ideas came from you?
- Is this a _new_ document?
- If this work was made by you and another person-not AI-would you need to credit this person as a coauthor?
- What else can you discuss about this comparison and this process?

_run the cell below to get your `tf_idf` functions ready to run_

```{code-cell} ipython3
import multiprocessing as mp
import numpy as np
import pandas as pd
pd.set_option('display.max_rows', None)
pd.set_option('display.max_colwidth', None)
import nltk
nltk.download('stopwords', quiet=True)

nltk.download('punkt')

from nltk.tokenize import word_tokenize
from nltk.corpus import stopwords
from nltk.stem import PorterStemmer
import sys

# https://medium.com/@mifthulyn07/comparing-text-documents-using-tf-idf-and-cosine-similarity-in-python-311863c74b2c

def preprocess_text(text):
    # lowercasing
    lowercased_text = text.lower()

    # cleaning 
    import re 
    remove_punctuation = re.sub(r'[^\w\s]', '', lowercased_text)
    remove_white_space = remove_punctuation.strip()

    # Tokenization = Breaking down each sentence into an array
    # from nltk.tokenize import word_tokenize
    tokenized_text = word_tokenize(remove_white_space)

    # Stop Words/filtering = Removing irrelevant words
    # from nltk.corpus import stopwords
    # stopwords = set(stopwords.words('english'))
    stopwords_removed = [word for word in tokenized_text if word not in stopwords.words()]

    # Stemming = Transforming words into their base form
    #from nltk.stem import PorterStemmer
    ps = PorterStemmer()
    stemmed_text = [ps.stem(word) for word in stopwords_removed]
    
    # Putting all the results into a dataframe.
    df = pd.DataFrame({
        'DOCUMENT': [text],
        'LOWERCASE' : [lowercased_text],
        'CLEANING': [remove_white_space],
        'TOKENIZATION': [tokenized_text],
        'STOP-WORDS': [stopwords_removed],
        'STEMMING': [stemmed_text]
    })

    return df


def calculate_tfidf(df):
    # Call the preprocessing result
    #df = preprocessing(corpus)
        
    # Make each array row from stopwords_removed to be a sentence
    stemming = df['STEMMING'].apply(' '.join)
    
    # Count TF-IDF
    from sklearn.feature_extraction.text import TfidfVectorizer
    vectorizer = TfidfVectorizer()
    tfidf_matrix = vectorizer.fit_transform(stemming)
    
    # Get words from stopwords array to use as headers
    feature_names = vectorizer.get_feature_names_out()

    # Combine header titles and weights
    df_tfidf = pd.DataFrame(tfidf_matrix.toarray(), columns=feature_names)
    df_tfidf = pd.concat([df, df_tfidf], axis=1)

    return df_tfidf



def cosineSimilarity(df):
    # Call the TF-IDF result
    df_tfidf = calculate_tfidf(df)
    
    # Get the TF-IDF vector for the first item (index 0)
    vector1 = df_tfidf.iloc[0, 6:].values.reshape(1, -1)

    # Get the TF-IDF vector for all items except the first item
    vectors = df_tfidf.iloc[:, 6:].values
    
    # Calculate cosine similarity between the first item and all other items
    from sklearn.metrics.pairwise import cosine_similarity
    cosim = cosine_similarity(vector1, vectors)
    cosim = pd.DataFrame(cosim)
    
    # Convert the DataFrame into a one-dimensional array
    cosim = cosim.values.flatten()

    # Convert the cosine similarity result into a DataFrame
    df_cosim = pd.DataFrame(cosim, columns=['COSIM'])

    # Combine the TF-IDF array with the cosine similarity result
    df_cosim = pd.concat([df_tfidf, df_cosim], axis=1)

    return df_cosim[['DOCUMENT', 'STEMMING', 'COSIM']]
```

```{code-cell} ipython3

```
