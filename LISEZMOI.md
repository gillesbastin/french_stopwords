# French Stopwords & French_Stoplocs : Deux listes de mots et de locutions pour la préparation de textes en français

[Lisez-moi en français](LISEZMOI.md) • [Read me in English](README.md)

Les logiciels ou bibliothèques standard d'exploration de texte incluent souvent des listes de mots vides par défaut conçues pour le prétraitement des corpus. Cependant, ces listes standard, auxquelles on peut accéder via la [bibliothèque R stopwords](https://github.com/quanteda/stopwords), une dépendance de la solution d'exploration de texte [Quanteda](https://github.com/quanteda/), sont souvent insuffisantes pour les langues autres que l'anglais et manquent de curation cohérente ou d'améliorations continues. Par exemple, la liste [Snowball](https://snowballstem.org/projects.html), une solution largement utilisée en exploration de texte, ne comprend que 164 tokens. Surtout, elle ne prend pas en compte des conjonctions de coordination très courantes et simples en français telles que "ni", "donc" ou "car". Une autre liste fréquemment utilisée, [stopwords-iso](https://github.com/stopwords-iso/stopwords-fr/tree/master), se compose de 691 tokens pour le français, ce qui est substantiel. Cependant, un examen plus attentif révèle des lacunes avec les verbes et les chiffres, ainsi que des problèmes d'accentuation. Parallèlement, la liste inclut également des mots significatifs et non équivoques qui ne sont pas vraiment des mots vides, tels que "nécessaire", "nouveau" ou "valeur". Enfin, la liste utilisée par [Iramuteq](http://www.iramuteq.org/) est également discutable. Composée de 560 tokens, elle contient de très nombreux termes très anciens (tels que "icelles"), de l'argot ("balpeau") ou des interjections ("boudiou") dont l'usage est pourtant très rare. Elle contient aussi des termes qui peuvent avoir un sens intéressant pour l'analyse (comme "attention").

Ce répertoire contient une liste soigneusement élaborée de mots outils pour le prétraitement des textes français, spécifiquement conçue pour les tâches d'exploration de texte ([`FRENCH_STOPWORDS`](french_stopwords.csv)). Cette liste ne prétend pas être exhaustive, mais sa longueur (plus de 1000 tokens) et sa documentation détaillée permettent de surmonter certaines limites des listes précédemment mentionnées. Je l'ai utilisée à plusieurs reprises, principalement pour le prétraitement de corpus d'actualités. Je pense qu'elle est à la fois exhaustive et efficace pour ce type de tâche. Avec son aide, en supprimant simplement les mots de la liste (ainsi que la ponctuation et les chiffres) d'une version tokenisée d'un corpus, la taille d'un document texte standard en français peut être réduite de 50 % sans perte significative de sens.

De plus, le répertoire contient également une liste de locutions adverbiales qui peuvent être utilisées, avec cependant plus de prudence, dans le prétraitement de textes en français ([`FRENCH_STOPLOCS`](french_stoplocs.csv)).

## Objectif

Les mots vides sont généralement considérés comme dénués de sens ou trop ambigus (ou les deux) pour être interprétés dans le contexte de l'exploration de texte. Ils sont généralement retirés d'un corpus avant son traitement avec des méthodes d'exploration de texte telles que l'analyse d'occurrence ou de cooccurrence, la classification, l'analyse en composantes principales, le *topic modeling*, etc. Typiquement, les pronoms, adverbes, auxiliaires, déterminants et conjonctions sont considérés comme des mots vides.

Retirer les mots vides lors du prétraitement du texte est une bonne idée à bien des égards. Parce que les mots vides sont très courants, cela contribue à accélérer le traitement des données textuelles (ce qui peut être très chronophage pour de grands corpus). Parce qu'ils ne contribuent pas significativement au sens d'un document, cela contribue également à augmenter l'importance statistique des mots de contenu ayant une signification sémantique plus grande et les met en avant dans les représentations visuelles du texte. Par conséquent, retirer les mots vides d'un document avant l'analyse textuelle contribue à réduire le bruit dans les données et à améliorer la qualité des résultats.

Bien que l'approche des listes de mots vides soit actuellement contestée par des approches plus statistiques ou basées sur l'IA (par exemple, en supprimant les tokens en fonction de leur fréquence dans un corpus ou en effectuant une étiquetage des parties du discours sur un corpus et en supprimant les tokens en fonction de leur classification grammaticale), de telles listes élaborées restent très utiles pour le traitement du langage naturel (NLP) et sont largement utilisées.

## Contenu du répertoire

- [`FRENCH_STOPWORDS`](french_stopwords.csv) contient uniquement des mots simples (ou tokens), par opposition aux expressions ou locutions (il inclut par exemple "en" et "face" mais pas "en face"). Il comprend des tokens contenant une apostrophe (comme "aujourd'hui") et, dans ce cas, également les parties séparées de tels tokens ("aujourd" et "hui") afin d'éviter les problèmes de mauvaise gestion des apostrophes lors de la tokenisation. La liste inclut également des tokens contenant un tiret ("dix-sept"). Elle est stockée dans un fichier CSV avec deux colonnes : token et catégorie (les tokens sont catégorisés grammaticalement de manière très approximative en raison de leur ambiguïté). Au 10 octobre 2024, la liste compte 1083 entrées.
- [`FRENCH_STOPLOCS`](french_stoplocs.csv) contient des locutions adverbiales composées de mots vides ou ayant les mêmes caractéristiques que les mots vides (sens faible ou ambigu), telles que "à cause de" ou "d'une manière ou d'une autre". Elle est également stockée sous forme de fichier CSV avec une seule colonne nommée 'locution'. Au 10 octobre 2024, la liste compte 373 entrées.

## Méthodologie

### Sources

Diverses sources, dont des listes précédentes (comme [Lexique](http://www.lexique.org/)), le dictionnaire Wikimedia, des sites web et ChatGPT, ont été utilisées pour générer des listes de mots vides dans différents domaines. Ces listes ont ensuite été soigneusement élaborées afin de les adapter à une utilisation dans des tâches de traitement du langage naturel (NLP).

### Limites

[`FRENCH_STOPWORDS`](french_stopwords.csv) comprend les types de tokens suivants :
- Conjonctions de coordination ;
- Conjonctions de subordination ;
- Déterminants ;
- Pronoms (y compris possessifs) ;
- Prépositions ;
- Interjections ;
- Adverbes (en particulier les adverbes de lieu et de temps ; les adverbes de manière n'ont pas été inclus car ils portent très souvent un sens) ;
- Auxiliaires ("être" et "avoir") ainsi que d'autres verbes souvent utilisés comme auxiliaires ("devoir", "pouvoir", "falloir", "faire", "aller", "dire", "mettre", "passer") ;
- Nombres cardinaux (tous les tokens utilisés pour compter de zéro à 999 999 ; les tokens "million" et "milliard" (ainsi que leurs formes plurielles) n'ont pas été inclus car ils sont souvent utiles pour catégoriser les textes mentionnant des sujets économiques) ;
- Nombres ordinaux (mêmes limites) ;
- Jours de la semaine ;
- Unités de temps ;
- Mois (y compris avec "mi-" : "janvier" et "mi-janvier").

[`FRENCH_STOPWORDS`](french_stopwords.csv) n'inclut pas les types de tokens suivants :
- Adverbes de manière ;
- Ponctuation ;
- Nombres en chiffres ;
- Emojis.

[`FRENCH_STOPLOCS`](french_stoplocs.csv) est une compilation de locutions adverbiales fréquemment utilisées en français. Cependant, il ne s'agit pas d'une collection exhaustive. Son objectif principal est de supprimer les locutions adverbiales constituées de tokens qui pourraient avoir des significations différentes lorsqu'elles sont interprétées individuellement. Cela est particulièrement important pour éviter les malentendus potentiels qui pourraient survenir si les locutions n'étaient pas supprimées avant la tokenisation.

## Comment utiliser les listes

Le cas d'utilisation typique d'une liste de mots vides consiste à supprimer tous les mots vides qu'elle contient des documents analysés. Cette étape de prétraitement dans un pipeline NLP nécessite une attention particulière.

- [`FRENCH_STOPWORDS`](french_stopwords.csv) doit être appliqué après la tokenisation. Il inclut des tokens très courts, y compris des lettres isolées, qui ne doivent être supprimés que lorsqu'ils sont rencontrés comme des tokens séparés dans un texte. Il est donc essentiel de s'assurer que les limites des mots ont été correctement interprétées par votre outil de tokenisation avant d'éliminer les mots vides avec [`FRENCH_STOPWORDS`](french_stopwords.csv). Évitez surtout d'utiliser la liste sur des textes non-tokenisés avec des fonctions R telles que `stringr::str_replace_all()`.
- [`FRENCH_STOPLOCS`](french_stoplocs.csv) doit être appliqué avant la tokenisation car il est constitué de séries de tokens séparés par des espaces blancs qui ne seront pas préservés par la tokenisation. Bien que la suppression de [`FRENCH_STOPLOCS`](french_stoplocs.csv) ait un impact limité sur les textes en raison de la rareté des locutions, il est bénéfique de traiter ces expressions avant la tokenisation. Les tokens utilisés dans chaque locution peuvent avoir des significations considérablement différentes lorsqu'ils sont isolés (par exemple, "tant bien que mal" - qui signifie "avec difficultés" - produirait une occurrence de "bien" ("good") et "mal" ("evil") s'il n'était pas supprimé avant la tokenisation. Étant donné la longueur des locutions, il n'y a aucun risque d'utiliser des fonctions telles que `stringr::str_replace_all()` dans ce cas.

### Exemples

La manière dont [`FRENCH_STOPWORDS`](french_stopwords.csv) doit être utilisée dépend en partie de l'outil utilisé pour la tokenisation. Voici deux exemples différents en R avec `tidytext::unnest()` et `udpipde::udpipe_annotate()`. Dans les deux exemples, df est un dataframe avec une colonne de texte nommée Texte.

```R copy
# Approche tidytext avec unnest()
df_tokenized_unnest <- df %>%
  # Étant donné que unnest() gère mal les apostrophes, elles sont remplacées par des espaces
  mutate(Texte = str_replace_all(Texte, "'", " ")) %>%
  # Tokenisation (les tokens sont mis en minuscules et la colonne de texte d'origine est supprimée)
  unnest_tokens(word, Texte, to_lower = TRUE, drop = TRUE) %>%
  # Suppression des mots vides en utilisant french_stopwords
  filter(!word %in% french_stopwords$token) %>%
  # Suppression des chiffres
  filter(!str_detect(word, "[:digit:]"))
```

L'approche tidytext est très simple mais présente quelques problèmes majeurs (la suppression systématique des apostrophes est par exemple une mauvaise solution car elle va impacter aussi les mots pleins). Vous pouvez plutôt utiliser udpipe qui est basé sur un modèle linguistique et fonctionne mieux pour découper les phrases en tokens. Un autre avantage d'udpipe est qu'il vous donne également un lemme pour chaque token. L'inconvénient de l'utilisation d'udpipe est qu'elle peut être assez lente sur de grands corpus et qu'elle nécessite un post-traitement de la colonne tokenisée pour gérer la ponctuation qui n'est pas systématiquement supprimée par l'algorithme.

```R copy
# Installer le modèle français pour udpipe
model <- udpipe_download_model(language = "french")
# Charger le modèle français
ud_model <- udpipe_load_model(model$file_model)
# Tokeniser et étiqueter les parties du discours
df_tokenized_udpipe <- udpipe_annotate(ud_model, x = df$Texte) %>%
  as.data.frame() %>%
      select(-sentence)
# Nettoyer la colonne token
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
  filter(!str_detect(token, "[:digit:]"))
# Remplacer les lemmes manquants par le token d'origine
df_tokenized_udpipe$lemma[is.na(df_tokenized_udpipe$lemma)] <- df_tokenized_udpipe$token
```

Si vous souhaitez utiliser [`FRENCH_STOPLOCS`](french_stoplocs.csv), vous devez exécuter le code R suivant directement sur votre colonne Texte :

```R copy
# Créer une liste de locutions séparées par "|"
loc <- paste(french_stoplocs$locution, collapse = '|')
# Supprimer toutes les locutions dans le texte
df <- df %>% mutate(Texte = str_replace_all(Texte, loc, ""))
```

### Précautions supplémentaires

- [`FRENCH_STOPWORDS`](french_stopwords.csv) et [`FRENCH_STOPLOCS`](french_stoplocs.csv) sont destinés à être utilisés avec des données textuelles propres rédigées en français. Ils ne tiennent pas compte des variations graphiques courantes des mots vides résultant d'erreurs d'orthographe, de problèmes OCR, etc. Il est donc recommandé de prétraiter les variables texte avant d'appliquer ces listes.
- Tous les tokens des deux listes incluent des accents et des caractères spéciaux (comme "œ") lorsque c'est nécessaire. Il est donc important de vérifier que votre corpus contient également des accents.
- Tous les tokens sont en minuscules, et le texte d'origine devrait suivre cette convention.
- Bien que les corpus en français contiennent souvent deux types d'apostrophes ("’"/U+2019 et "'"/U+0027), les listes ne conservent que l'apostrophe "droite" ou "verticale" ("'"). Assurez-vous donc que les apostrophes "inclinées" ("typographiques") (qui sont en fait des apostrophes droites) sont remplacées par des apostrophes droites dans le corpus avant d'utiliser les listes (par exemple, avec dplyr::mutate(text = str_replace_all(text, "’", "'")).
- La décision de classer un mot comme un mot vide doit toujours être en accord avec la question de recherche et le corpus spécifique en cours d'utilisation. Certains mots peuvent avoir une signification minimale dans certains contextes mais peuvent être beaucoup plus significatifs dans d'autres. Il est donc recommandé de revoir attentivement et, si nécessaire, de modifier la liste avant de l'appliquer.
