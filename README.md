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
