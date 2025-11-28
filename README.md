# English POS Tagger (Brown + UD English EWT, NLTK)

This project implements and compares several **Part-of-Speech (POS) taggers**
in Python using the [NLTK](https://www.nltk.org/) library.

The models are trained and evaluated on **two English corpora**:

1. **Brown Corpus (news category)** – classic POS-tagged corpus.
2. **UD English EWT (Universal Dependencies English Web Treebank)** – a
   more recent web-based corpus in CoNLL-U format, annotated with
   universal POS tags.

The whole project is in a single Jupyter notebook:
`English_POS_Tagger.ipynb`.

---

## 1. Tagging algorithms

Implemented taggers (all from NLTK):

- **DefaultTagger** – assigns the same tag to every word
  (e.g. `NN` or `NOUN`).
- **UnigramTagger** – chooses the most frequent tag for each word based
  only on the word itself.
- **BigramTagger** – considers the previous tag as context, with backoff
  to the unigram tagger.
- **TrigramTagger** – considers the previous two tags, with backoff to
  the bigram tagger.
- **HiddenMarkovModelTagger (HMM)** – sequence model trained
  supervised on labeled sentences.

Each tagger is trained on the training split of a corpus and evaluated on
a held-out test split.

---

## 2. Datasets

### 2.1 Brown Corpus (news)

- Loaded directly from NLTK: `nltk.corpus.brown`.
- We use the **"news"** category.
- Splitting:
  - 80% of sentences for training
  - 20% for testing

### 2.2 UD English EWT

- Downloaded from the Universal Dependencies project
  (files like `en_ewt-ud-train.conllu`, `en_ewt-ud-dev.conllu`,
  `en_ewt-ud-test.conllu`).
- Format: **CoNLL-U** with 10 tab-separated columns.
- We parse the files and keep:
  - column 2: `FORM` (word)
  - column 4: `UPOS` (universal POS tag)
- Splitting:
  - Training: `train + dev` sentences
  - Testing: `test` sentences

Place the EWT files under:

```text
data/
  ud_english_ewt/
    en_ewt-ud-train.conllu
    en_ewt-ud-dev.conllu
    en_ewt-ud-test.conllu
