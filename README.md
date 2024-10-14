# French Stopwords & French_Stoplocs : Two curated stoplists of words and locutions for preprocessing French texts


[Lisez-moi en français](LISEZMOI.md) • [Read me in English](README.md)

Standard text mining software or libraries often include default stopwords lists designed for pre-processing corpora. However, these standard lists — which can be accessed through the [stopwords R library](https://github.com/quanteda/stopwords) a dependency of [Quanteda](https://github.com/quanteda/) text mining solution — are often insufficient for languages other than English and lack consistent curation or ongoing improvements. For example, the [Snowball](https://snowballstem.org/projects.html) list, a widely utilized solution in text mining, comprises only 164 tokens. Above all, it lacks very common and simple coordinating conjunctions in French such as "ni", "donc" or "car". Another frequently used list, [stopwords-iso](https://github.com/stopwords-iso/stopwords-fr/tree/master), consists of 691 tokens for French, which is substantial. However, a closer inspection reveals weaknesses with verbs and numbers, as well as numerous problems with missing accents. At the same time, the list also includes meaningful and unambiguous words that do not really qualify as stopwords, such as "nécessaire", "nouveau" or "valeur". Another list, from the [University of Neuchâtel](http://members.unine.ch/jacques.savoy/clef/frenchST.txt), is based on tokens frequency and has a very relevant — but in my opinion limited in scope — list of 463 stopwords. Finally, the list used by [Iramuteq](http://www.iramuteq.org/), which contains 560 tokens, is also questionable. It contains a lot of very old terms (such as "icelles"), slang ("balpeau") and interjections ("boudiou") that are very rarely used. It also contains terms that might carry meaning (such as "attention").

This repository contains a carefully curated list of stopwords for preprocessing French texts, specifically designed for text mining tasks ([`FRENCH_STOPWORDS`](french_stopwords.csv)). This list does not claim to be exhaustive, but its length (over 1,000 tokens) and thorough documentation help overcome some limitations of the previously mentioned ones. I have used it on several occasions, mainly for preprocessing news corpora. I believe that it is both comprehensive and effective for this type of task. With its help — typically by simply removing the words in the list (as well as punctuation and numbers) from a tokenized version of a corpus, the size of a standard French text document can be reduced by 50 % without much loss of meaning.

In addition, the repository also contains a list of adverbial locutions which can be used — albeit with more caution — in French text preprocessing ([`FRENCH_STOPLOCS`](french_stoplocs.csv)).

## Aim

Stopwords are words that are generally deemed meaningless or too ambiguous (or both) for interpretation in the context of text mining. They are generally removed from a corpus before its processingh with text mining methods such as occurrence or co-occurrence analysis, classification, principal components analysis, topic modeling, etc. Typically, pronouns, adverbs, auxilliaries, determinants, conjunctions are considered as stopwords.

Removing stopwords in text preprocessing is a good ideas in many respects. Because stopwords are very common, it helps speed up the processing of text data (which can be very time-consuming for large corpora). Because they do not contribute significantly to the meaning of a document, it also helps increase the statistical importance of content words with greater semantic meaning and makes them more prominent in visual representations of the text. Consequently, removing stopwords in a document before text analysis helps reduce noise in the data and increases the quality of the results.

Although the stopwords lists approach for stopwords removal is now being challenged by more statistical or AI-driven approaches (for instance removing tokens based on their frequency in a corpus, or performing Part-of-Speech tagging on a corpus and removing tokens based on their grammatical classification), such curated lists are still very valuable for natural language processing (NLP) and widely used.

## Content of the depository

- [`FRENCH_STOPWORDS`](french_stopwords.csv) contains only single words (or tokens), as opposed to expressions or locutions (it includes for instance "en" and "face" but not "en face"). It includes tokens containing an apostrophe (such as "aujourd'hui") and, in this case, also the separate parts of such tokens ("aujourd" and "hui") in order to prevent issues with poor handling of apostrophes in tokenization. The list also includes tokens containing an hyphen ("dix-sept"). It is stored in csv file with two columns : token and category (tokens are categorized grammatically in a very approximate way due to their ambiguity). **On October 13th, 2024, the list has 1083 entries**.
- [`FRENCH_STOPLOCS`](french_stoplocs.csv) contains adverbial locutions made with stopwords or having the same characteristics as stopwords (weak or ambiguous meaning), such as "à cause de" or "d'une manière ou d'une autre". It is also stored as a csv file with only one colum nammed 'locution'. **On October 14th, 2024, the list has 418 entries**.

## Methodology

### Sources

Various sources, including previous lists (as [Lexique](http://www.lexique.org/)), Wikimedia dictionary, websites and ChatGPT have been used to generate lists of stopwords in various domains. These lists have then been carefully curated in order to adapt them for use in NLP tasks.

### Boundaries

[`FRENCH_STOPWORDS`](french_stopwords.csv) includes the following types of tokens :
- Coordination conjunctions ;
- Subordination conjunctions ;
- Determinants ;
- Pronouns (including possessive ones) ;
- Prepositions ;
- Interjections ;
- Adverbs (especially space and time adverbs ; manner adverbs have not been included as they very often carry meaning) ;
- Auxiliaries ("être" and "avoir") as well as other verbs often used as auxiliaries ("devoir", "pouvoir", "falloir", "faire", "aller", "dire", "mettre", "passer") ;
- Cardinal numbers (all tokens used to count from zero to 999 999 ; the tokens "million" and "billion" (as well as their plural forms) have not been included because they are often useful to categorize texts mentioning economic issues) ;
- Ordinal numbers (same limits) ;
- Days of the week ;
- Time units ;
- Months (including with "mi-" : "janvier" & "mi-janvier").

[`FRENCH_STOPWORDS`](french_stopwords.csv) does not include the following types of tokens :
- manner adverbs
- Punctuation
- Numbers in digits
- Emojis

[`FRENCH_STOPLOCS`](french_stoplocs.csv) is a compilation of frequently employed adverbial phrases in French. However, it is not an exhaustive collection. Its primary objective is to suppress those adverbial phrases consisting of tokens that might convey different meanings when interpreted individually. This is particularly important to prevent potential misinterpretations that could arise if the phrases were not removed prior to tokenization.

## Updates

The initial commit for this project dates back to November 29, 2023. Since then, the lists have been occasionally modified. Starting from October 2024, updates to the lists are documented below:
- October 12, 2024: The lists were shared on the "quanti" mailing list.
- October 13, 2024: Following feedback from the mailing list, a comparison with the Neuchâtel List (Jacques Savoy) was added, and some interjections from this list were incorporated.
- October 14, 2024: The FRENCH_STOPLOCS list was updated with curated locutions from [Wiktionary](https://fr.wiktionary.org/wiki/Cat%C3%A9gorie:Locutions_adverbiales_en_fran%C3%A7ais) (from "et al." to "à flots").

## How to use the lists

The typical use case for a stopwords list involves removing all stopwords it contains from the analyzed documents. This pre-processing step in an NLP pipeline requires careful consideration.

- [`FRENCH_STOPWORDS`](french_stopwords.csv) should be applied after tokenization. It includes very short tokens, including isolated letters, which should only be removed when encountered as separate tokens in a text. Thus, it is essential to ensure that word boundaries have been correctly interpreted by your tokenization tool before eliminating stopwords with [`FRENCH_STOPWORDS`](french_stopwords.csv). Especially avoid using the list on non-tokenized texts with R functions like `stringr::str_replace_all()`.
- [`FRENCH_STOPLOCS`](french_stoplocs.csv) should be applied before tokenization since it consists of series of tokens separated by whitespaces that will not be preserved by tokenization. While removing [`FRENCH_STOPLOCS`](french_stoplocs.csv) has a limited impact on texts due to the rarity of locutions, it is beneficial to address these expressions before tokenization. The tokens used in each locution can have significantly different meanings when isolated (for example, "tant bien que mal" — which means "with difficulties" — would produce an occurrence of "bien" ("good") and "mal" ("evil") if not removed before tokenization. Given the length of locutions, there is no risk in using functions such as `stringr::str_replace_all()` in this case.

### Examples

The way [`FRENCH_STOPWORDS`](french_stopwords.csv) should be used is partly dependent on the tool used for tokenization. Here are two different examples in R with `tidytext::unnest()` and `udpipde::udpipe_annotate()`. In both examples, df is a dataframe with a text column nammed Text

```R copy
# tidytext approach with unnest()
df_tokenized_unnest <- df %>%
  # Since unnest() poorly handles apostrophes, they are replaced by whitespaces
  mutate(Texte = str_replace_all(Texte, "'", " ")) %>%
  # Tokenization (tokens are turned lowercase and the original text column is dropped)
  unnest_tokens(word, Texte, to_lower = TRUE, drop = TRUE) %>%
  # Stopwords removal using french_stopwords
  filter(!word %in% french_stopwords$token) %>%
  # Digits removal
  filter(!str_detect(word,"[:digit:]"))
```
The tidytext approach is very easy but has some major issues (the removal of apostrophes is for instance a bad solution).
Instead you can use udpipe which is based on a language model and performs better at splitting phrases into tokens. Another advantage of udpipe is that it also gives you a lemma for each token. The downside of using udpipe is that it can be quite slow on large corpora and it needs some processing of the tokenized column to deal with punctuation.

```R copy
# Install the French model for udpipe
model <- udpipe_download_model(language = "french")
# Load the French model
ud_model <- udpipe_load_model(model$file_model)
# Tokenize and tag parts of speech
df_tokenized_udpipe <- udpipe_annotate(ud_model, x = df$Texte) %>%
  as.data.frame() %>%
      select(-sentence)
# Clean token column
df_tokenized_udpipe <- df_tokenized_udpipe %>%
  mutate(token = tolower(token)) %>%
  filter(!upos == "PUNCT") %>% # On supprime les lignes de ponctuation
  filter(!upos == "SYM") %>% # On supprime les lignes de ponctuation
  mutate(token = ifelse(str_detect(token, "^-"), str_replace(token, "-", ""), token)) %>% # supprime le - quand le token commence par un tiret
  mutate(token = ifelse(str_detect(token, "^«"), str_replace(token, "«", ""), token)) %>% # supprime le « quand le token commence par un guillemet ouvrant
  mutate(token = ifelse(str_detect(token, "^»"), str_replace(token, "»", ""), token)) %>% # supprime le » quand le token commence par un guillemet fermant
  mutate(token = ifelse(str_detect(token, ".»$"), str_replace(token, "»", ""), token)) %>% # supprime le » quand le token finit par un guillemet fermant
  mutate(token = ifelse(str_detect(token, ".«$"), str_replace(token, "«", ""), token)) %>% # supprime le « quand le token commence par un guillemet ouvrant
  mutate(token = ifelse(str_detect(token, "^,"), str_replace(token, ",", ""), token)) %>% # supprime la virgule quand le token commence par une virgule
  mutate(token = ifelse(str_detect(token, ".'$"), str_replace(token, "'", ""), token)) %>% # supprime l'apostrophe quand le token finit par une apostrophe
  mutate(token = ifelse(str_detect(token, "^\\?"), str_replace(token, "\\?", ""), token)) %>% # supprime le point d'interrogation quand le token finit par un point d'interrogation
  mutate(token = ifelse(str_detect(token, ".\\.$"), str_replace(token, "\\.", ""), token)) %>% # supprime le point quand le token finit par un point
  mutate(token = ifelse(str_detect(token, "^\\.\\.\\."), str_replace(token, "\\.\\.\\.", ""), token)) %>% # supprime les trois points quand le token commence par trois points
  mutate(token = ifelse(str_detect(token, "^\\."), str_replace(token, "\\.", ""), token)) %>% # supprime le point quand le token commence par un point
  filter(!token %in% french_stopwords$token) %>%
  filter(!token %in% c("")) %>%
  filter(!str_detect(token,"[:digit:]"))
# Replace missing lemmas with original token
df_tokenized_udpipe$lemma[is.na(df_tokenized_udpipe$lemma)] <- df_tokenized_udpipe$token
```

If you want to use [`FRENCH_STOPLOCS`](french_stoplocs.csv), you should run the following R code directly on your Text column before tokenizing it :

```R copy
# Create a list of locutions separated by "|"
loc <- paste(french_stoplocs$locution, collapse = '|')
# Remove all locutions in the text
df <- df %>% mutate(Texte = str_replace_all(Texte, loc, ""))
```

### Extra precautions

- [`FRENCH_STOPWORDS`](french_stopwords.csv) and [`FRENCH_STOPLOCS`](french_stoplocs.csv) are intended for use with clean textual data written in French. They do not account for common graphical variations of stopwords resulting from spelling errors, OCR issues, etc. Therefore, it is advisable to preprocess the text variables before applying these lists.
- All tokens in both lists include accents and special characters (such as "œ") when necessary. Therefore, it is important to verify that your corpus also contains accents.
- All tokens are in lowercase, and the original text should follow suit.
- While French corpora may often feature two types of apostrophes ("’"/U+2019 and "'"/U+0027), the lists retain only the "straight" or "vertical" one ("'"). Thus, ensure that "slanted" ("typographic") apostrophes (effectively right single quotation marks) are replaced by straight ones in the corpus before utilizing the lists (e.g., with `dplyr::mutate(text = str_replace_all(text, "’", "'")`).
- The decision to categorize a word as a stopword should always align with the research question and the specific corpus in use. Some words may have minimal significance in certain contexts but can be considerably more meaningful in others. Therefore, it is recommended to carefully review and, if necessary, modify the list before applying it.
