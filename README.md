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

