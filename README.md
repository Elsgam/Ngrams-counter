# Ngrams-counter
In this workshop I'm going to determine the frequency of ten most used unigrams, bigrams and trigrams for an spam corpus obtained in Kaggle. You also can see the code and the spam data in this repository.

## Code to find the frequency of unigrams/bigrams/trigrams
Before, explain the code I want that you, like a reader, have in mind that this program is written in Python.

So, for the first part, we have to open our database. You can find it in this repository with the name: 'spam.csv'. Below, you have the code to open and read the data file:
```ruby
# Open the modules we're going to need:
import nltk, re, string, collections
from nltk.util import ngrams # function for making ngrams

# Open and read the Spam corpus:
with open("spam.csv", "r", encoding='latin-1') as file:
    text = file.read()

# check to make sure the file read in alright; let's print out the first 1000 characters
text[0:1000]
```

Once we have read the file, we do some preprocessing: 
```ruby
# let's do some preprocessing. We don't care about the XML notation, new lines 
# or punctuation marks other than periods. (We'll consider the end of the sentence
# a "word") We also don't want to consider capitalization. 

# get rid of all the XML markup
text = re.sub('<.*>','',text)

# get rid of the "ENDOFARTICLE." text
text = re.sub('ENDOFARTICLE.','',text)

# get rid of punctuation (except periods!)
punctuationNoPeriod = "[" + re.sub("\.","",string.punctuation) + "]"
text = re.sub(punctuationNoPeriod, "", text)

# make sure it looks ok
text[0:1000]
```

For the next step, we going to obtain the list of all the unigrams, bigrams and trigrams of our corpus:
```ruby
# first get individual words
tokenized = text.split()

# get a list of all the uni-grams
unigrams = ngrams(tokenized, 1)

# get a list of all the bi-grams
esBigrams = ngrams(tokenized, 2)

# and get a list of all the tri-grams
trigrams = ngrams(tokenized, 3)

# If you like, you can uncomment the next like to take a look at 
# the first ten to make sure they look ok. Please note that doing so 
# will consume the generator & will break the next block of code, so you'll
# need to re-comment it and run this block again to get it to work.
# list(esBigrams)[:10]
```

Now, we going to obtain the frequency of all the unigrams for then just show the ten most used:
```ruby
# get the frequency of the unigram:
unigramsFreq = collections.Counter(unigrams) 

# What are the ten words most used?
unigramsFreq.most_common(10)
```
### Results of unigrams
```
[(('to',), 2159),
 (('you',), 1812),
 (('a',), 1338),
 (('the',), 1207),
 (('I',), 1088),
 (('and',), 860),
 (('in',), 829),
 (('is',), 811),
 (('u',), 783),
 (('i',), 739)]
```

Just like we did with the unigrams, we going to find all the bigrams and print the ten most used:
```ruby
# get the frequency of each bigram in our corpus
esBigramFreq = collections.Counter(esBigrams)

# what are the ten most popular ngrams in this Spanish corpus?
esBigramFreq.most_common(10)
```
### Results of bigrams:
```
[(('are', 'you'), 104),
 (('in', 'the'), 86),
 (('have', 'a'), 80),
 (('want', 'to'), 78),
 (('will', 'be'), 78),
 (('to', 'be'), 78),
 (('in', 'a'), 74),
 (('to', 'get'), 72),
 (('you', 'are'), 71),
 (('have', 'to'), 70)]
```

Finally, we did the same process with claculate the ten trigrams most used: 
```
# get the frequency of each trigram
trigramFreq = collections.Counter(trigrams)

# what are the ten most popular tri-grams?
trigramFreq.most_common(10)
```
### Results of trigrams:
```
[(('Ill', 'call', 'later'), 39),
 (('hamSorry', 'Ill', 'call'), 38),
 (('have', 'won', 'a'), 23),
 (('I', 'miss', 'you'), 22),
 (('prize', 'GUARANTEED', 'Call'), 20),
 (('å£1000', 'cash', 'or'), 17),
 (('a', 'great', 'day'), 17),
 (('are', 'trying', 'to'), 16),
 (('Account', 'Statement', 'for'), 16),
 (('are', 'you', 'doing'), 16)]
```

## View in colab:
If you want to see the code working, just go to the next colab project and check for yourself the results: 
[Link code here](https://colab.research.google.com/drive/1GreSSmjDAhgvOPZk-LB7-00s1n1BYBdX?usp=sharing)
