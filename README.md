# French Stopwords

Stopwords are words that are generally deemed either insignificant or too ambiguous for meaningful interpretation in the context of text mining, and thus are removed from a corpus before analysis.

Standard text mining software or libraries often include default stopwords lists designed for pre-processing corpora. However, these standard lists — which can be accessed through the [stopwords R library](https://github.com/quanteda/stopwords) a dependency of [Quanteda](https://github.com/quanteda/) text mining solution — are recognized as insufficient for languages other than English and lack consistent curation or ongoing improvements. For example, the [Snowball](https://snowballstem.org/projects.html) list, a widely utilized solution in text mining, comprises only 164 tokens. Notably, it lacks very common and simple coordinating conjunctions like "ni," "donc," or "car." Another frequently employed list, [stopwords-iso](https://github.com/stopwords-iso/stopwords-fr/tree/master), consists of 691 tokens for French, which is substantial. However, a closer inspection reveals weaknesses in terms of verbs and numbers, as well as issues with missing accents. In the same time, it doubtfully includes words that can be considered meaningful and unambiguous, such as "droite," "nécessaire," "nouveau," and "valeur."

This repository comprises a carefully curated list of stopwords designed for preprocessing French texts, specifically tailored for text mining tasks.

## Aim

Although stopwords lists are being challenged by more statistical or AI-driven approaches, they are still very valuable for natural language processing (NLP). This is mainly because stopwords are very common. Removing them thus helps speed up the processing of text data (which can be very time-consuming for large corpora). Because they do not contribute significantly to the meaning of a document, removing stopwords also helps increase the statistical importance of content words with greater semantic meaning and makes them more prominent in visual representations of the text. Consequently, removing stopwords in a document before text analysis helps reduce noise in the data and increases the quality of the results.

## Content of the depository

Because the specifif format of a stopwords list depends on how it is going to be used, I have constituted to different lists of stopwords from this research.

- french_stopwords is the list of stopwords *per se*. It only includes single words (or tokens), as opposed to expressions or locutions, that are to be used after the tokenization of a text document or a series of texts in a dataframe. This list should be used before tokenization only if you can be sure that words boundaries will be respected. The list contains small words or even isolated letters that can be found in many other words. Thus, using something like str_detect(text, list) or sub() or `stringr::str_replace_all()` would be very dangerous.
- french_stoplocs is a list of locutions that can be considered as stopwords. It is interesting to deal with those expressions before tokenization because the tokens used in each locution can have a very different meaning when isolated. Thus removing those expressions is a good idea but it can only be performed before tokenization (for instance "tant bien que mal" means with difficulties but has nothing to do with good and evil). Due to the lenght of locutions, there is no risks to use str_detect().

## Methodology

### Sources

Various sources, including previous lists, Wikimedia dictionary, websites and ChatGPT have been used to generate lists of stopwords in various domains. These lists have then been carefully curated in order to adapt them for use in NLP tasks.

### Formats

The following rules have been applied while constituting the lists :

- The tokens and locutions are spelled with accents and special caracters
- They are spelled lower case
- Tokens or locutions made of other tokens are not included (for instance "par laquelle" is not in the locutions' list because "par" and "laquelle" are in in the words list).
- The lists have been transformed into .csv files for interoperability issues.

### Boundaries

#### What is Included in the List?

- Coordination conjunctions
- Adverbs
- Auxiliaries (list)
- Cardinal numbers from zero to 1 billion
- Ordinal numbers from zero to 1 billion
- Days of the week
- Time units
- Months

#### What is Not Included?

- manner adverbs such as…
- Punctuation
- Numbers in digits
- Special characters
- Emojis

## Use case

The typical use case of a stopwords list is to remove all stopwords it contains from the documents analyzed.

## Precautions

- The list is for use on clean textual data written in French. For instance it does not include common graphical variations of stopwords due to spelling mistakes. In particular, all tokens in the list contain accents when needed. So check that your corpus contains them too. Another remarkable feature is that only one apostrophe has been retained whereas french corpora often contain two ( "’"/U+2019 and "'"/U+0027). The list is written with the "straight" or "vertical" apostrophe ("'"). So make sure that "slanted" ("typographic") apostrophes (which are actually right single quotation marks are replaced by straight ones in the corpus before using the list (for instance with mutate(text = str_replace_all(text, "’", "'"))
- The decision to consider a word as a stopword should always be made with the research question and the specific corpus in mind. Some words may have a very low level of significance in certain contexts but considerably higher significance in others. Therefore, it is advisable to carefully review and, if necessary, modify the list before applying it.

## Size

The list...
