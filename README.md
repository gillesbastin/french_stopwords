# French Stopwords

Standard text mining software or libraries often include default stopwords lists designed for pre-processing corpora. However, these standard lists — which can be accessed through the [stopwords R library](https://github.com/quanteda/stopwords) a dependency of [Quanteda](https://github.com/quanteda/) text mining solution — are often insufficient for languages other than English and lack consistent curation or ongoing improvements. For example, the [Snowball](https://snowballstem.org/projects.html) list, a widely utilized solution in text mining, comprises only 164 tokens. Above all, it lacks very common and simple coordinating conjunctions such as "ni", "donc" or "car". Another frequently used list, [stopwords-iso](https://github.com/stopwords-iso/stopwords-fr/tree/master), consists of 691 tokens for French, which is substantial. However, a closer inspection reveals weaknesses with verbs and numbers, as well as problems with missing accents. At the same time, the list also includes meaningful and unambiguous words that do not really qualify as stopwords, such as "nécessaire", "nouveau" or "valeur".

This repository contains a carefully curated list of 887 stopwords for preprocessing French texts, specifically designed for text mining tasks. I have used this list on several occasions, mainly for preprocessing news corpora. I believe that it is both comprehensive and effective for this type of task. With its help — typically by simply removing the words in the list (as well as punctuation and numbers) from a tokenized version of a corpus, the size of a standard French text document can be reduced by 50 % without much loss of meaning.

In addition, the repository also contains a list of 342 adverbial locutions which can also be used — albeit with more caution — in French text preprocessing.

## Aim

Stopwords are words that are generally deemed insignificant or too ambiguous for meaningful interpretation (or both) in the context of text mining. They are generally removed from a corpus before its analysis with text mining methods such as occurrence or co-occurrence analysis, classification, principal components analysis, topic modeling, etc. Although the stopwords lists approach is being challenged by more statistical or AI-driven approaches for stopword removal, such lists are still very valuable for natural language processing (NLP) and widely used.

Removing stopwords in text preprocessing is a good ideas in many respects. Because stopwords are very common, it helps speed up the processing of text data (which can be very time-consuming for large corpora). Because they do not contribute significantly to the meaning of a document, it also helps increase the statistical importance of content words with greater semantic meaning and makes them more prominent in visual representations of the text. Consequently, removing stopwords in a document before text analysis helps reduce noise in the data and increases the quality of the results.

## Content of the depository

Because the specifif format of a stopwords list depends on how it is going to be used, I have constituted to different lists of stopwords from this research.

- french_stopwords is the list of stopwords *per se*. It only includes single words (or tokens), as opposed to expressions or locutions, that are to be used after the tokenization of a text document or a series of texts in a dataframe. This list should be used before tokenization only if you can be sure that words boundaries will be respected. The list contains small words or even isolated letters that can be found in many other words. Thus, using something like str_detect(text, list) or sub() or `stringr::str_replace_all()` would be very dangerous. french_stopwords contains XXX lines.
- french_stoplocs is a list of locutions that can be considered as stopwords. It is interesting to deal with those expressions before tokenization because the tokens used in each locution can have a very different meaning when isolated. Thus removing those expressions is a good idea but it can only be performed before tokenization (for instance "tant bien que mal" means with difficulties but has nothing to do with good and evil). Due to the lenght of locutions, there is no risks to use str_detect(). french_stoplocs contains XXX lines.

## Methodology

### Sources

Various sources, including previous lists, Wikimedia dictionary, websites and ChatGPT have been used to generate lists of stopwords in various domains. These lists have then been carefully curated in order to adapt them for use in NLP tasks.

### Boundaries

#### french_stopwords

french_stopwords is made of tokens (character strings without whitespaces). It includes the following grammatical categories : Coordination conjunctions ; Adverbs (especially space and time) ; Auxiliaries ("être" and "avoir") as well as other vers often used as auxiliaries ("devoir", "pouvoir", "falloir", "faire", "aller", "dire", "mettre", "passer") ; cardinal numbers from zero to 1 billion : ordinal numbers ; days of the week ; time units ; months.
- Auxiliaries (list)
- Cardinal numbers from zero to 1 billion
- Ordinal numbers from zero to 1 billion
- Days of the week
- Time units
- Months

#### french_stoplocs

- manner adverbs such as…
- Punctuation
- Numbers in digits
- Special characters
- Emojis

### Formats

The following rules have been applied while constituting the lists :

- The tokens and locutions are spelled with accents and special caracters
- They are spelled lower case
- Tokens or locutions made of other tokens are not included (for instance "par laquelle" is not in the locutions' list because "par" and "laquelle" are in in the words list).
- The lists have been transformed into .csv files for interoperability issues.

## How to use the lists

The typical use case of a stopwords list is to remove all stopwords it contains from the documents analyzed.

### Precautions

- The list is for use on clean textual data written in French. For instance it does not include common graphical variations of stopwords due to spelling mistakes.
- In particular, all tokens in the list contain accents when needed. So check that your corpus contains them too.
- Another remarkable feature is that only one apostrophe has been retained whereas french corpora often contain two ( "’"/U+2019 and "'"/U+0027). The list is written with the "straight" or "vertical" apostrophe ("'"). So make sure that "slanted" ("typographic") apostrophes (which are actually right single quotation marks are replaced by straight ones in the corpus before using the list (for instance with `dplyr::mutate(text = str_replace_all(text, "’", "'")`)
- The decision to consider a word as a stopword should always be made with the research question and the specific corpus in mind. Some words may have a very low level of significance in certain contexts but considerably higher significance in others. Therefore, it is advisable to carefully review and, if necessary, modify the list before applying it.
