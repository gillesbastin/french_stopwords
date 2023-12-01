# French Stopwords

Stopwords are words that are generally deemed either insignificant or too ambiguous for meaningful interpretation in the context of text mining, and thus are removed from a corpus before analysis.

Standard text mining software or libraries often include default stopwords lists designed for pre-processing corpora. However, these standard lists are recognized as insufficient for languages other than English and lack consistent curation or ongoing improvements. For example, the Snowball list, a widely utilized solution in text mining, comprises only 164 tokens. Notably, it lacks very common and simple coordinating conjunctions like "ni," "donc," or "car." Another frequently employed list, [stopwords-iso](https://github.com/stopwords-iso/stopwords-fr/tree/master), consists of 691 tokens for French, which is substantial. However, a closer inspection reveals weaknesses in terms of verbs and numbers, as well as issues with missing accents. In the same time, it doubtfully includes words that can be considered meaningful and unambiguous, such as "droite," "nécessaire," "nouveau," and "valeur."[^1]

This repository comprises a carefully curated list of stopwords designed for preprocessing French texts, specifically tailored for text mining tasks.

## Aim

Although stopwords lists are being challenged by more statistical or AI-driven approaches, they are still very valuable for natural language processing (NLP). This is mainly because stop words are very common. Removing them thus helps speed up the processing of text data (which can be very time-consuming for large corpora). Because they do not contribute significantly to the meaning of a document, removing stopwords also helps increase the statistical importance of content words with greater semantic meaning and makes them more prominent in visual representations of the text. Consequently, removing stop words in a document before text analysis helps reduce noise in the data and increases the quality of the results.

## Principles

- **Adaptability**: The list is designed to be used at any stage of text pre-processing. Its typical use is with a text variable in a dataframe before tokenization (using `stringr::str_replace_all()`, for instance). However, it can also be applied after tokenization (using `anti_join()` in R, for instance). In that case, perform tokenization without lemmatization or stemming to ensure stopwords are not affected and are successfully removed.

- **Economy**: Regular expressions that can be considered as stopwords are not included in the list if they are made up of stopwords from the list (such as "par laquelle" or "peu ou prou"). Otherwise, they are included to help remove ambiguous expressions from the text while preserving non-ambiguous terms they are composed of ("tant bien que mal").

- **Portability**: The list is provided as a CSV file.

## Methodology

Various sources, including previous lists, Wikimedia dictionary, websites and ChatGPT have been used to generate lists of stopwords in various domains. These lists have then been carefully curated in order to adapt them for use in NLP tasks.

Two distinct sets of stopwords have been constituted from this work :

- french_stopwords is the list of stopwords 

## What is Included in the List?

- Coordination conjunctions
- Adverbs
- Auxiliaries
- Cardinal numbers from zero to 1 billion
- Ordinal numbers from zero to 1 billion
- Days of the week
- Time units
- Months

## What is Not Included?

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

[^1]: See stopwords library
