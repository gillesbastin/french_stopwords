# French Stopwords

Standard text mining software or libraries often include default stopwords lists designed for pre-processing corpora. However, these standard lists — which can be accessed through the [stopwords R library](https://github.com/quanteda/stopwords) a dependency of [Quanteda](https://github.com/quanteda/) text mining solution — are often insufficient for languages other than English and lack consistent curation or ongoing improvements. For example, the [Snowball](https://snowballstem.org/projects.html) list, a widely utilized solution in text mining, comprises only 164 tokens. Above all, it lacks very common and simple coordinating conjunctions such as "ni", "donc" or "car". Another frequently used list, [stopwords-iso](https://github.com/stopwords-iso/stopwords-fr/tree/master), consists of 691 tokens for French, which is substantial. However, a closer inspection reveals weaknesses with verbs and numbers, as well as problems with missing accents. At the same time, the list also includes meaningful and unambiguous words that do not really qualify as stopwords, such as "nécessaire", "nouveau" or "valeur".

This repository contains a carefully curated list of stopwords for preprocessing French texts, specifically designed for text mining tasks. I have used this list on several occasions, mainly for preprocessing news corpora. I believe that it is both comprehensive and effective for this type of task. With its help — typically by simply removing the words in the list (as well as punctuation and numbers) from a tokenized version of a corpus, the size of a standard French text document can be reduced by 50 % without much loss of meaning.

In addition, the repository also contains a list of adverbial locutions which can be used — albeit with more caution — in French text preprocessing.

## Aim

Stopwords are words that are generally deemed meaningless or too ambiguous (or both) for interpretation in the context of text mining. They are generally removed from a corpus before its processingh with text mining methods such as occurrence or co-occurrence analysis, classification, principal components analysis, topic modeling, etc. Typically, pronouns, adverbs, auxilliaries, determinants, conjunctions are considered as stopwords.

Removing stopwords in text preprocessing is a good ideas in many respects. Because stopwords are very common, it helps speed up the processing of text data (which can be very time-consuming for large corpora). Because they do not contribute significantly to the meaning of a document, it also helps increase the statistical importance of content words with greater semantic meaning and makes them more prominent in visual representations of the text. Consequently, removing stopwords in a document before text analysis helps reduce noise in the data and increases the quality of the results.

Although the stopwords lists approach for stopwords removal is now being challenged by more statistical or AI-driven approaches (for instance removing tokens based on their frequency in a corpus, or performing Part-of-Speech tagging on a corpus and removing tokens based on their grammatical classification), such lists are still very valuable for natural language processing (NLP) and widely used.

## Content of the depository

- `FRENCH_STOPWORDS` contains only single words (or tokens), as opposed to expressions or locutions (it includes for instance "en" and "face" but not "en face"). It includes tokens containing an apostrophe (such as "aujourd'hui") or an hyphen ("dix-sept"). The list is stored in csv file with two columns : token and category. It has 903 lines.
- `FRENCH_STOPLOCS` contains adverbial locutions made with stopwords or having the same characteristics as stopwords (weak or ambiguous meaning), such as "à cause de" or "d'une manière ou d'une autre". It is also stored as a csv file with only one colum nammed 'locution'. It has 327 lines.

## Methodology

### Sources

Various sources, including previous lists (as [Lexique](http://www.lexique.org/)), Wikimedia dictionary, websites and ChatGPT have been used to generate lists of stopwords in various domains. These lists have then been carefully curated in order to adapt them for use in NLP tasks.

### Boundaries

`FRENCH_STOPWORDS` includes the following types of tokens :
- Coordination conjunctions ;
- Adverbs (especially space and time adverbs ; manner adverbs have not been included as they very often carry meaning) ;
- Auxiliaries ("être" and "avoir") as well as other verbs often used as auxiliaries ("devoir", "pouvoir", "falloir", "faire", "aller", "dire", "mettre", "passer") ;
- Cardinal numbers (all tokens used to count from zero to 999 999 ; the tokens "million" and "billion" (as well as their plural forms) have not been included because they are foten useful to categorize texts mentioning economic issues) ;
- Ordinal numbers (same limits) ;
- Days of the week ;
- Time units ;
- Months.

`FRENCH_STOPWORDS` does not include the following types of tokens :
- manner adverbs
- Punctuation
- Numbers in digits
- Special characters
- Emojis

`FRENCH_STOPLOCS` is a compilation of frequently employed adverbial phrases in French. However, it is not an exhaustive collection. Its primary objective is to eliminate from a corpus those adverbial phrases consisting of tokens that might convey different meanings when interpreted individually. This is particularly important to prevent potential misinterpretations that could arise if the phrases were not removed prior to tokenization.

### Formats

The following guidelines were adhered to when creating the lists:

- Tokens and phrases are written with accents and special characters.
- All entries are in lowercase.

## How to use the lists

The typical use case for a stopwords list involves removing all stopwords it contains from the analyzed documents. This pre-processing step in an NLP pipeline requires careful consideration.

- `FRENCH_STOPWORDS` should be applied after tokenization. It includes very short tokens, including isolated letters, which should only be removed when encountered as separate tokens in a text. Thus, it is essential to ensure that word boundaries have been correctly interpreted by your tokenization tool before eliminating stopwords with french_stopwords. In tidytext, the recommended approach is to use the list on a tokens column named 'word' with `filter(!word %in% french_stopwords$token)`. Avoid using the list on non-tokenized texts with functions like `stringr::str_replace_all()`.
- `FRENCH_STOPLOCS` should be applied before tokenization since it consists of series of tokens that may not be preserved during tokenization. While it has a limited impact on texts due to the rarity of locutions, it is beneficial to address these expressions before tokenization. This is because the tokens used in each locution can have significantly different meanings when isolated (for example, "tant bien que mal" means "with difficulties" but has no association with "good" and "evil"). Given the length of locutions, there is no risk in using `stringr::str_replace_all()` in this case.

### Extra precautions

- `FRENCH_STOPWORDS` and  `FRENCH_STOPLOCS` are designed for use on clean textual data written in French. They do not encompass common graphical variations of stopwords resulting from spelling errors, OCR issues, etc. It is thus recommended to clean text variable before using them.
- All tokens in both lists include accents when necessary. Therefore, it is important to verify that your corpus also contains accents.
- While French corpora may often include two types of apostrophe ("’"/U+2019 and "'"/U+0027), the lists retains only the "straight" or "vertical" one ("'"). Consequently, ensure that "slanted" ("typographic") apostrophes (which are in fact right single quotation marks) are replaced by straight ones in the corpus before using the lists (e.g., with `dplyr::mutate(text = str_replace_all(text, "’", "'")`).
- The decision to classify a word as a stopword should always align with the research question and the specific corpus in use. Some words may have minimal significance in certain contexts but can be considerably more meaningful in others. Therefore, it is recommended to carefully review and, if necessary, modify the list before applying it.
