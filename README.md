# NLP-Word-Embeds
NLP Word Emdendings Model - to aim is to create a custom embeddings for a given dataset instead of using pre-trained libraries.

## Preprocess data
Following techniques are used for Data Preprocessing:

1. Casefolding - data was converted to lower case to reduce the vocabulary size. Words like 'Hello' and 'hello' will be treated in similar fashion.
2. Tags and URL removal - The data contained some html tags and urls. As such, they will not add any extra information to our sentiment analysis task and removed to reduce overall vocabulary size.
3. Special Character removal - During character embedding, it was noticed that there were number of special/non-english characters in the dataset. Since, our libraries (nltk etc) are based on English languge only, it was decided to remove these characters. There is a chance of information loss (change in meaning/word) becasue of that.
4. Expand contractions - To make it easier for "stopword" removal step, all known cotractions (including capitalised ) were expanded. For example "Haven't" expanded to 'have not'.
5. Remove numbers and punctuations - Removed numbers and other punctuations that add noise to the dataset.
6. Tokenization :: chopping each review document into word sequence. Tokenization will further help in lemmatization, stopword removal to preprocess data.
7. Lemmetization :: Decided to use Lemmetization instead of stemming. Stemming can at times change the meaning of the word. Because our modeling is basic (only 1 window size for context), we can't rely on 1-window sized context for meaningful processing. Hence, decided to use only lemmatization instead of stemming.
8. Stopword removal :: Removed commonly occurring stopword using nltk library. stopwords are common repitive words that add extra noise to word processing. Perormed at the end to maximise commond word removal.

## Model Implementation
#### Word Embeddings
Model Selection

* Considering the size of the dataset, fasttext was ruled out. The n-grams used for fast text will need significantly higher resources that current colab environment.
* Using word2vec skipgram model - Between CBOW and skipgram, I decided to choose skipgram just for a trial.
Each section will have explanation on approach taken.

#### Data Preprocessing for Word Embeddings
* Merged train and test data to create master list of all available words.
* Padding - To make uniform input document length, we padded all documents based on maximum length of a document.
* Create Skipgrams - Based on unique word and index, skipgrams were created for numeric (index) representation of target and context word. Window size of more than 1 always crashes colab notebook and hence I kept it to minimum window size.
