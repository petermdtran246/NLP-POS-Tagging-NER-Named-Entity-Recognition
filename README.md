#  NLP Pipeline Project — POS Tagging & Named Entity Recognition (NER)

This project demonstrates the full Natural Language Processing (NLP) pipeline used to analyze real-world tech news headlines.  
It covers text preprocessing, tokenization, lemmatization, POS tagging, and named entity recognition using **NLTK** and **spaCy**.

The dataset used in this project is:

tech_startup_news.csv


which contains 1,000 AI & Tech startup headlines generated for learning and experimentation.

---

## **Project Objectives**

This project showcases how to:

- Clean and preprocess raw text  
- Tokenize and normalize words  
- Remove stopwords and punctuation  
- Lemmatize tokens  
- Apply POS tagging to understand grammatical structure  
- Apply NER to detect entities (PERSON, ORG, DATE, MONEY, etc.)  
- Analyze frequency distributions for POS and Entities  

This is similar to real-world NLP pipelines used in search engines, chatbots, recommendation systems, and analytics dashboards.

---

## **Technologies Used**

| Library | Purpose |
|--------|----------|
| **NLTK** | Tokenization, stopwords, lemmatization |
| **spaCy** | POS tagging and NER |
| **pandas** | Data manipulation |
| **matplotlib** | Visualization |
| **re (regex)** | Text cleaning |

---

## **Project Structure**
├── tech_startup_news.csv # Dataset used in this project
├── nlp_pos_ner_project.ipynb # Full notebook code
└── README.md # Documentation (this file)

Also ensure NLTK datasets are downloaded:

nltk.download('punkt')
nltk.download('stopwords')
nltk.download('wordnet')


1. Text Preprocessing Pipeline

The project begins by loading the dataset and preprocessing the title column.

Steps performed:

• Lowercasing

• Removing stopwords

• Removing punctuation

• Tokenization (raw & cleaned)

• Lemmatization

• Flattening token lists

Example:

titles['lowercase'] = titles['title'].str.lower()

titles['no_stopwords'] = titles['lowercase'].apply(
    lambda x: " ".join(w for w in x.split() if w not in en_stopwords)
)

titles['no_stopwords_no_punct'] = titles['no_stopwords'].str.replace(
    r"[^\w\s]", " ", regex=True
)

titles['tokens_clean'] = titles['no_stopwords_no_punct'].map(word_tokenize)


2. Flattening the Token Lists

To analyze word frequency across the entire dataset, we flatten all token lists using three approaches:
tokens_raw_list = list(chain.from_iterable(titles['token_raw']))
tokens_clean_list = list(chain.from_iterable(titles['tokens_clean_lemmatized']))

3. POS Tagging with spaCy

The cleaned raw text is joined into a single string and processed through spaCy:
spacy_doc = nlp(" ".join(tokens_raw_list))

We then convert each token into a pandas DataFrame:
pos_df = pd.DataFrame({
    "token": [t.text for t in spacy_doc],
    "pos":   [t.pos_ for t in spacy_doc],
    "tag":   [t.tag_ for t in spacy_doc]
})

Example POS output:
| token    | pos   | tag |
| -------- | ----- | --- |
| Apple    | PROPN | NNP |
| launches | VERB  | VBZ |
| new      | ADJ   | JJ  |

Top 10 Most Frequent Nouns:

top_nouns = pos_df_counts[pos_df_counts['pos'] == 'NOUN'].head(10)

Similar logic is used to extract the top verbs and adjectives.

4. Named Entity Recognition (NER)

Entities are extracted directly from the processed spaCy document:

ner_df = pd.DataFrame({
    "entity":  [ent.text for ent in spacy_doc.ents],
    "ner_tag": [ent.label_ for ent in spacy_doc.ents]
})

Example NER output:

| entity     | tag  |
| ---------- | ---- |
| Apple      | ORG  |
| 2025       | DATE |
| California | GPE  |


Entity Frequency Analysis

ner_df_counts = (
    ner_df
    .value_counts(["entity", "ner_tag"])
    .reset_index(name="counts")
    .sort_values(by="counts", ascending=False)
)


## Key Learnings

This project demonstrates:

• How preprocessing dramatically affects model output

• How POS tagging helps understand grammatical structure

• How NER identifies real-world concepts from text

• How to convert NLP outputs into analyzable DataFrames













