# spaCy Symspell: Spelling correction implementation in spaCy via Symspell

This package is a [spaCy 2.0 extension](https://spacy.io/usage/processing-pipelines#section-extensions) that adds sentnece/spelling corrections via Symspell to spaCy's text processing pipeline.

## Installation

`pip install spacy_symspell`

## Usage

Adding the component to the processing pipeline is relatively simple:

```
import spacy
from spacy_symspell import SpellingCorrector

nlp = spacy.load('en')
corrector = SpellingCorrector()
nlp.add_pipe(corrector)
doc = nlp('What doyuoknowabout antyhing.')

doc.suggestions  #list
doc.segmentation  #what do you know about anything?
```

spaCy_symspell operates on `Doc` and `Span` spaCy objects. When called on a `Doc` or `Span`, the object is given two attributes: `suggestions` (a list of all found spelling suggestions) and `segmentation` (a corrected sentence in the case of ommitted spaces).

## Under the hood
spacy_symspell is a wrapper of the [python port](https://github.com/mammothb/symspellpy) for [Symspell](https://github.com/wolfgarbe/SymSpell). For additional details, see the linked project pages.