# French Stopwords

This repository contains a curated list of stopwords intended for pre-processing French texts for text mining purposes.

Standard text mining software or libraries often include default stopwords lists designed for pre-processing corpora. The typical use of such lists is to suppress all occurrences of the stopwords from the corpus. This helps increase the statistical weight of other words, their significance for analysis, and enhances the lexical distance between clusters in common text mining methods like hierarchical classification, principal components analysis, or topic modeling. Stopwords are generally considered either insignificant or too ambiguous for interpretation in text mining.

However, these standard lists are known to be inadequate for languages other than English and are not consistently curated or improved over time. For instance, the Snowball list...[^1]

To address this, I have compiled a more comprehensive list of stopwords.

## Principles

- **Adaptability**: The list is designed to be used at any stage of text pre-processing. Its typical use is with a text variable in a dataframe before tokenization (using `stringr::str_replace_all()`, for instance). However, it can also be applied after tokenization (using `anti_join()` in R, for instance). In that case, perform tokenization without lemmatization or stemming to ensure stopwords are not affected and are successfully removed.

- **Economy**: Regular expressions that can be considered as stopwords are not included in the list if they are made up of stopwords from the list (such as "par laquelle" or "peu ou prou"). Otherwise, they are included to help remove ambiguous expressions from the text while preserving non-ambiguous terms they are composed of ("tant bien que mal").

- **Portability**: The list is provided as a CSV file.

## Methodology



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

## Precautions

- The list is for use on clean textual data written in French. For instance it does not include common graphical variations of stopwords due to spelling mistakes. In particular, all tokens in the list contain accents when needed. So check that your corpus contains them too. Another remarkable feature is that only one apostrophe has been retained whereas french corpora often contain two ( "’"/U+2019 and "'"/U+0027). The list is written with the "straight" or "vertical" apostrophe ("'"). So make sure that "slanted" ("typographic") apostrophes (which are actually right single quotation marks are replaced by straight ones in the corpus before using the list (for instance with mutate(text = str_replace_all(text, "’", "'"))
- The decision to consider a word as a stopword should always be made with the research question and the specific corpus in mind. Some words may have a very low level of significance in certain contexts but considerably higher significance in others. Therefore, it is advisable to carefully review and, if necessary, modify the list before applying it.

## Size

The list...

[^1]: See stopwords library
