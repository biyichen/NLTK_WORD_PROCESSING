# NLTK_WORD_PROCESSING

#### The tokenization process means dividing large parts into widgets. use NLTK tokens to split the text. This is something you might think, it's too simple, you don't need to use NLTK's tokenizer, you can use regular expressions to split sentences, because each sentence has punctuation and spaces.

#### Then look at the following text: 'Hello Mr. Adam, how are you? '
#### So if you use punctuation to split, 'Hello Mr','Adam','how are you' will be considered each individual sentence, but if you use NLTK:
```
from nltk.tokenize import sent_tokenize
import nltk
nltk.download('punkt')

mytext = "Hello Mr. Adam, how are you? I hope everything is going well. Today is a good day, see you dude."
print(sent_tokenize(mytext))
```
#### Will return the result as "['Hello Mr. Adam, how are you?', 'I hope everything is going well.', 'Today is a good day, see you dude.']"

#### Could also split the sentence into words. The word Mr. has not been separated. NLTK uses the PunktSentenceTokenizer of the punkt module, which is part of NLTK.tokenize. And this tokenizer is trained to work in multiple languages.
```
from nltk.tokenize import word_tokenize
mytext = "Hello Mr. Adam, how are you? I hope everything is going well. Today is a good day, see you dude."
print(word_tokenize(mytext))
```
#### Will return the result as " ['Hello', 'Mr.', 'Adam', ',', 'how', 'are', 'you', '?', 'I', 'hope', 'everything', 'is', 'going', 'well', '.', 'Today', 'is', 'a', 'good', 'day', ',', 'see', 'you', 'dude', '.']"

#### Non-English Tokenize
```
from nltk.tokenize import sent_tokenize
mytext = "Bonjour M. Adam, comment allez-vous? J'espère que tout va bien. Aujourd'hui est un bon jour."
print(sent_tokenize(mytext,"french"))
```
#### Will return the result as "['Bonjour M. Adam, comment allez-vous?', "J'espère que tout va bien.", "Aujourd'hui est un bon jour."]"

#### Synonym processing
#### Use the nltk.download() installation interface, one of which is WordNet. WordNet is a database built for natural language processing. It includes some synonym groups and some short definitions.
```
from nltk.corpus import wordnet
import nltk
nltk.download()
syn = wordnet.synsets("pain")
print(syn[0].definition())
print(syn[0].examples())

//You can use WordNet to get synonyms like this

from nltk.corpus import wordnet
  
synonyms = []
for syn in wordnet.synsets('Computer'):
    for lemma in syn.lemmas():
        synonyms.append(lemma.name())
print(synonyms)
```
#### Will return the result as " ['computer', 'computing_machine', 'computing_device', 'data_processor', 'electronic_computer', 'information_processing_system', 'calculator', 'reckoner', 'figurer', 'estimator', 'computer']"

#### Antonym processing
```
from nltk.corpus import wordnet
  
antonyms = []
for syn in wordnet.synsets("small"):
    for l in syn.lemmas():
        if l.antonyms():
            antonyms.append(l.antonyms()[0].name())
print(antonyms)
```
#### Will return the result as " ['large', 'big', 'big']"

#### Stem extraction
#### In language morphology and information retrieval, stemming is the process of removing the affixes to get the roots. For example, the working stem is work. Search engines use this technique when indexing pages, so many people write different versions of the same word. There are many algorithms to avoid this, the most common being the Boolean stem algorithm. NLTK has a class called PorterStemmer, which is the implementation of this algorithm:
```
from nltk.stem import PorterStemmer
  
stemmer = PorterStemmer()
print(stemmer.stem('working'))
print(stemmer.stem('worked'))
```
#### Will return the result as "work, work"

#### Non-English stem extraction
#### In addition to English, SnowballStemmer also supports 13 languages. Supported languages:
```
from nltk.stem import SnowballStemmer
  
print(SnowballStemmer.languages)
```
#### Will return the result as "'danish', 'dutch', 'english', 'finnish', 'french', 'german', 'hungarian', 'italian', 'norwegian', 'porter', 'portuguese', 'romanian', 'russian', 'spanish', 'swedish'"

#### You can use the stem function of the SnowballStemmer class to extract non-English words like this.
```
from nltk.stem import SnowballStemmer
  
french_stemmer = SnowballStemmer('french')
  
print(french_stemmer.stem("French word"))
```
#### Word variant reduction
#### A word variant restore is similar to a stem, but the difference is that the result of a variant restore is a real word. Unlike stemming, when you try to extract certain words, it produces similar words:
```
from nltk.stem import PorterStemmer
  
stemmer = PorterStemmer()
  
print(stemmer.stem('increases'))
```
#### Will return the result as "increas"

#### Now, if you use NLTK's WordNet to perform a variant restore of the same word, the correct result:
```
from nltk.stem import WordNetLemmatizer
  
lemmatizer = WordNetLemmatizer()
  
print(lemmatizer.lemmatize('increases'))

```
#### Will return the result as "increase"

#### The result may be a synonym or a different word of the same meaning. Sometimes when you restore a word to a variant, you always get the same word. This is because the default part of the language is a noun. To get a verb, you can specify

```
from nltk.stem import WordNetLemmatizer
  
lemmatizer = WordNetLemmatizer()
  
print(lemmatizer.lemmatize('playing', pos="v"))
```
#### Will return the result as "play"

#### In fact, this is also a good way to compress text, and finally get the text from the original 50% to 60%. The result can also be a verb (v), a noun (n), an adjective (a), or an adverb (r):
```
from nltk.stem import WordNetLemmatizer
  
lemmatizer = WordNetLemmatizer()
print(lemmatizer.lemmatize('playing', pos="v"))
print(lemmatizer.lemmatize('playing', pos="n"))
print(lemmatizer.lemmatize('playing', pos="a"))
print(lemmatizer.lemmatize('playing', pos="r"))
```
#### Will return the result as "play,playing,playing,playing"

#### The difference between stems and variants
```
from nltk.stem import WordNetLemmatizer
from nltk.stem import PorterStemmer
  
stemmer = PorterStemmer()
lemmatizer = WordNetLemmatizer()
print(stemmer.stem('stones'))
print(stemmer.stem('speaking'))
print(stemmer.stem('bedroom'))
print(stemmer.stem('jokes'))
print(stemmer.stem('lisa'))
print(stemmer.stem('purple'))
print('----------------------')
print(lemmatizer.lemmatize('stones'))
print(lemmatizer.lemmatize('speaking'))
print(lemmatizer.lemmatize('bedroom'))
print(lemmatizer.lemmatize('jokes'))
print(lemmatizer.lemmatize('lisa'))
print(lemmatizer.lemmatize('purple'))
```
#### The result will be: stone, speak, bedroom, joke, lisa, purpl.
#### The result will be:stone, speaking, bedroom, joke, lisa, purple.
