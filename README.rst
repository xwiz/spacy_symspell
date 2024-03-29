
spaCy Symspell
==============

Spelling correction implementation in spaCy via Symspell
--------------------------------------------------------

This package is a `spaCy 2.0 extension <https://spacy.io/usage/processing-pipelines#section-extensions>`_ that adds sentnece/spelling corrections via Symspell to spaCy's text processing pipeline.

Installation
------------

``pip install spacy_symspell``

Notes
-----

This package is still in Alpha and there may be unforeseen errors. Dictionary loading time is also significant, can take up to 30 seconds on slow machines.

Usage
-----

Adding the component to the processing pipeline is relatively simple:

.. code-block::

   import spacy
   from spacy_symspell import SpellingCorrector

   nlp = spacy.load('en_core_web_sm')
   corrector = SpellingCorrector()
   nlp.add_pipe(corrector)
   doc = nlp('What doyuoknowabout antyhing')

   for s in doc._.suggestions:#iterable
       print(s) #What doyon about anything

   doc._.segmentation  #::segmented_string - What doyouk now about antyhing ::corrected_string - that dook now about anything


spaCy_symspell operates on ``Doc`` and ``Span`` spaCy objects. When called on a ``Doc`` or ``Span``\ , the object is given two attributes: ``suggestions`` (a list of all found spelling suggestions) and ``segmentation`` (a corrected sentence in the case of ommitted spaces).

Todo
----

Symspell accuracy can be improved with the help of spaCy by extracting and analyzing resulting n-grams and cross-referencing with possible n-grams deductible from the character groups in the symspell result. For example the correction 'that dook now' leaves us with a verbless sentence, and on closer analysis will reveal that the character group 'now' is related with the verb 'know', and the verb know is associated with the n-gram 'you know'.

Under the hood
--------------

`spacy_symspell <https://github.com/xwiz/spacy_symspell>`_ is currently a wrapper of the `python port <https://github.com/mammothb/symspellpy>`_ for `Symspell <https://github.com/wolfgarbe/SymSpell>`_. For additional details, see the linked project pages.
