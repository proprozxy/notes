## NLP

### 1 Data Collection

#### 1.1 Open Database



#### 1.2 Crawlers



### 2 Data Processing

#### 2.1 Cleaning

##### 2.1.1 Remove Special Characters

Use regular expressions or string replacement operations.

```python
import re

text = "Hello, <b>World</b>!"
cleaned_text = re.sub(r'<.*?>', '', text)  # Remove HTML tags
print(cleaned_text)  # Output: "Hello, World!"

```

```python
text = "This   is  an example sentence.\n\n\n"
cleaned_text = ' '.join(text.split())
print(cleaned_text)  # Output: "This is an example sentence."

```

##### 2.1.2 Convert to Lowercase

Standardize the text's case.

```python
text = "Hello World"
lowercase_text = text.lower()
print(lowercase_text)  # Output: "hello world"

```

##### 2.1.3 Spelling Correction

Use spelling correction tools (e.g., NLTK, TextBlob).

```python
from textblob import TextBlob

text = "Helo Worlld"
corrected_text = TextBlob(text).correct()
print(corrected_text)  # Output: "Hello World"

```



#### 2.2 Tokenization

Break down a text into individual words or tokens.

```python
from nltk.tokenize import word_tokenize

text = "This is an example sentence."
tokens = word_tokenize(text)
print(tokens)  # Output: ['This', 'is', 'an', 'example', 'sentence', '.']

```



#### 2.3 Stopwords Removal

Use a list of stopwords to remove common but low-information words, such as "and," "the," etc.

```python
from nltk.corpus import stopwords

def remove_stopwords(text):
    stop_words = set(stopwords.words("english"))
    words = word_tokenize(text)
    filtered_words = [word for word in words if word.lower() not in stop_words]
    return " ".join(filtered_words)

text = "This is an example sentence."
filtered_text = remove_stopwords(text)
print(filtered_text)  # Output: "example sentence ."

```



#### 2.4 Stemming / Lemmatization

 Reduces words to their base or dictionary form.

```python
from nltk.stem import WordNetLemmatizer

lemmatizer = WordNetLemmatizer()
word = "running"
lemma = lemmatizer.lemmatize(word, pos="v")
print(lemma)  # Output: "run"

```



### 3 Text Analysis

#### 3.1 Syntax Analysis

Analyze sentence structure, including identifying words, phrases, and clauses within the text.

```python
import spacy

nlp = spacy.load("en_core_web_sm")
text = "This is an example sentence."
doc = nlp(text)
for token in doc:
    print(token.text, token.dep_, token.head.text)
    
    # Output:
    # This nsubj is
    # is ROOT is
    # an det sentence
    # example compound sentence
    # sentence attr is
    # . punct is
    
```



#### 3.2 NER

Identify and extract named entities from the text.

```python
import spacy

nlp = spacy.load("en_core_web_sm")
text = "Apple Inc. was founded by Steve Jobs in Cupertino."
doc = nlp(text)
for ent in doc.ents:
    print(ent.text, ent.label_)
    
	# Output:
    # Apple Inc. ORG
    # Steve Jobs PERSON
    # Cupertino GPE
    
```



#### 3.3 Sentiment Analysis

Analyze the sentiment of the text.

```python
from textblob import TextBlob

text = "I love this markdown."
blob = TextBlob(text)
sentiment = blob.sentiment.polarity
if sentiment > 0:
    print("Positive sentiment")  # Output: "Positive sentiment" 
elif sentiment < 0:
    print("Negative sentiment")
else:
    print("Neutral sentiment")
    
```



#### 3.4 Topic Modeling

Apply algorithms such as LDA or NMF to discover topics within the text.

```python

```



### 4 Feature Extraction

#### 4.1 Bag of Words

BoW represents text data as a vector, where each element of the vector represents the frequency of a corresponding word in the text. This model assumes that the words in the text are independent of each other and ignores the order and grammatical structure of the words.

```python
from sklearn.feature_extraction.text import CountVectorizer

# Create a text dataset
corpus = [
    'This is the first document.',
    'This document is the second document.',
    'And this is the third one.',
    'Is this the first document?'
]

# Create the Bag of Words model
vectorizer = CountVectorizer()

# Transform the text dataset into a Bag of Words vector
X = vectorizer.fit_transform(corpus)

# Get the vocabulary
vocab = vectorizer.get_feature_names_out()

# Convert the Bag of Words vector to a sparse matrix
print("Bag of Words Vector:")
print(X.toarray())

# Display the vocabulary
print("Vocabulary:")
print(vocab)

# Output:
# Bag of Words Vector:
# [[0 1 1 1 0 0 1 0 1]
#  [0 2 0 1 0 1 1 0 1]
#  [1 0 0 1 1 0 1 1 1]
#  [0 1 1 1 0 0 1 0 1]]
# Vocabulary:
# ['and' 'document' 'first' 'is' 'one' 'second' 'the' 'third' 'this']

```

**Ignoring Word Order and Grammar**

The BoW model treats words in text as independent, thus disregarding word order and grammatical structure. This means it cannot capture contextual information between words, leading to semantic loss.

**High-Dimensional Sparsity**

BoW-generated vectors are often highly sparse, especially when the vocabulary is large or the text dataset is extensive. This results in a high-dimensional feature space, which may require more storage and computational resources.

**Inability to Handle New Vocabulary**

When constructing the vocabulary in BoW, it assumes that all words in the text dataset are known. It struggles to effectively handle unknown vocabulary when new words appear.

**Not Suitable for Long Texts**

For long texts, BoW features may become very large, potentially leading to the curse of dimensionality, particularly in classification tasks.



#### 4.2 TF-IDF

TF-IDF, which stands for Term Frequency-Inverse Document Frequency, is widely used in text feature extraction aimed at assessing the importance of words within a document or a corpus of documents. 

**Term Frequency - TF:**

- TF represents how frequently a word occurs within a document.
- Typically, it can be calculated as the number of times a word appears in the document (raw term frequency) or as a normalized version, such as relative term frequency (the term frequency divided by the total number of words in the document).
- TF measures a word's importance within an individual document.

**Inverse Document Frequency - IDF:**

- IDF assesses a word's importance within the entire corpus of documents.

- Words with a higher IDF value are considered unique to the entire corpus because they do not appear frequently in all documents.

- The IDF is often calculated using the formula: 
  $$
  IDF(t)=log(\frac{N + 1}{1 + df(t)}) + 1
  $$
  where $N$ is the total number of documents, and $df(t)$ is the number of documents that contain the term $t$.

**TF-IDF Calculation:**

- The TF-IDF value is the product of TF and IDF.
- It measures a word's importance within a document while taking into account the importance of the word within the entire corpus.
- Words with high TF-IDF values are those that occur frequently within an individual document but are rare in the entire dataset, indicating their uniqueness.

```python
from sklearn.feature_extraction.text import TfidfVectorizer

# Create a text dataset
corpus = [
    "This is the first document.",
    "This document is the second document.",
    "And this is the third one.",
    "Is this the first document?"
]

# Create a TF-IDF model
tfidf_vectorizer = TfidfVectorizer()

# Transform the text dataset into TF-IDF vectors
tfidf_matrix = tfidf_vectorizer.fit_transform(corpus)

# Get the vocabulary
feature_names = tfidf_vectorizer.get_feature_names_out()

# Convert the TF-IDF vectors into a sparse matrix
print("TF-IDF Vectors:")
print(tfidf_matrix.toarray())

# Display the vocabulary
print("Vocabulary:")
print(feature_names)

# Output:
# TF-IDF Vectors:
# [[0.         0.46979139 0.58028582 0.38408524 0.         0.         0.38408524 0.         0.38408524]
# [0.         0.6876236  0.         0.28108867 0.         0.53864762 0.28108867 0.         0.28108867]
# [0.51184851 0.         0.         0.26710379 0.51184851 0.         0.26710379 0.51184851 0.26710379]
# [0.         0.46979139 0.58028582 0.38408524 0.         0.         0.38408524 0.         0.38408524]]
# Vocabulary:
# ['and' 'document' 'first' 'is' 'one' 'second' 'the' 'third' 'this']
```



#### 4.3 N-gram

N-gram is used to split text into consecutive n words or character sequences. The main idea of N-gram is to capture local features and contextual information in text.



#### 4.4 Word Embeddings

Word Embeddings is a technique for mapping words into a continuous vector space, where each word is represented as a vector. These vectors are automatically learned from large-scale text data, often using deep learning methods such as Word2Vec, GloVe, or FastText.



### 5 ML / DL

#### BERT



### 6 Training

#### 6.1 Overfitting

##### 6.1.1 L1 Regularization - Lasso

##### 6.1.2 L2 Regularization - Ridge

##### 6.1.3 Early Stopping



### 7 Evaluation

#### 7.1 Accuracy

Represent the ratio of correctly classified samples to the total number of samples.
$$
Accuracy =
$$


#### 7.2 Precision

Show the model's ability to correctly classify positive cases among all cases it classified as positive.
$$
Precision =
$$


#### 7.3 Recall

Show the model's ability to correctly classify positive cases among all actual positive cases. 
$$
Recall =
$$


#### 7.4 F1 Score

The harmonic mean of precision and recall.
$$
F1 =
$$


#### 7.5 ROC Curve / AUC

It plots the False Positive Rate (FPR) on the x-axis and the True Positive Rate (TPR) on the y-axis for different threshold values. The area under the ROC curve (AUC) is also a metric used to measure a classification model's performance. A higher AUC value (closer to 1) indicates better model performance.
$$
FPR=
\\
TPR=
$$




