# Gendered Words Dataset

This dataset tags English words with the [natural gender](#natural-gender-definition) of the person or type of person the word refers to.

# License
The dataset is licensed under [Creative Commons Attribution 3.0](https://creativecommons.org/licenses/by/3.0/us/), and WordNet content is licensed under the [WordNet License](https://wordnet.princeton.edu/license-and-commercial-use).

# Contents and Format

The dataset is a JSON file, containing a single list of JSON objects, one per word-sense, that is, a word and its definition. Thus, a single word with multiple definitions could appear multiple times in the dataset. To disambiguate words, each JSON object contains a [WordNet](https://wordnet.princeton.edu/) sense number and definition (definitions are also mostly from WordNet).

### JSON format

* `word` is the word itself.
* `wordnet_senseno` is the sense number in WordNet, and may be used to look up the word in WordNet, for example to find synonyms and related words.
* `gender` is the gender of the person or people the word refers to, and currently has one of the values gender-neutral (`n`), male or masculine (`m`), female or feminine (`f`) or other (`o`).
* `gender_map` contains mappings to words for other genders, if they exist. 
	* Currently contains mappings for `f` (female/feminine), `m` (male/masculine), `n` (gender-neutral). Other genders may be added in the future or by pull request.
	* `parts_of_speech` is either `*` for all parts of speech, or one of the [Penn Treebank POS tagset](https://www.cis.uni-muenchen.de/~schmid/tools/TreeTagger/) which is common to Python NLTK and many other NLP libraries. Examples are `NN` (noun) and `NNP` (proper noun).

### Example
```json
[
	{
		"word":"artilleryman", 
		"wordnet_senseno": "artilleryman.n.01", 
		"gender": "m", 
		"gender_map": {
				"f": [{"parts_of_speech": "*", "word": "artillerywoman"}],
				"n": [{"parts_of_speech": "*", "word": "artilleryperson"}]
			}
		}
	},
	...
]
```

# Contributing

1. [Fork](https://guides.github.com/activities/forking/) the [master repo](https://github.com/ecmonsen/gendered_words) and clone your fork.
1. Using your favorite editor or IDE, make your changes.
  1. Do not reformat the JSON. Preserve the format of one word per line. 
  1. Add new words at the **end** of the file. 
1. Commit and push changes to your fork.
1. Create a [pull request](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-requests).
1. Maintainers of the master repo will review the pull request and accept or request changes.

# How the dataset was created

This dataset was initially created by dumping all of the hyponyms of the WordNet synset for "person". Each word was manually tagged as gender-neutral (`n`), male or masculine (`m`), female or feminine (`f`) or other (`o`) (only a few words such as "hermaphrodite" are tagged as "other").

A few additional words that are not WordNet hyponyms of "person" were manually added, including personal (`he`, `she`, `him`, `her`) and possessive (`his`, `hers`, `her`) pronouns, and a few adjectives like `male` and `female`.

The dataset will be occasionally updated, and pull requests are welcome.

# Natural Gender Definition

According to [Wikipedia](https://en.wikipedia.org/wiki/Grammatical_gender#Grammatical_vs._natural_gender) (as of 2019-10-31), "The natural gender of a noun, pronoun or noun phrase is a gender to which it would be expected to belong based on relevant attributes of its referent. This usually means masculine or feminine, depending on the referent's sex (or gender in the sociological sense)." 


