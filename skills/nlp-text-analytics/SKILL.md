---
name: nlp-text-analytics
description: Use when the user works with text data and needs help with text preprocessing, sentiment analysis, topic modeling, text classification, NER, embeddings, transformers, LLM fine-tuning, RAG pipelines, or any natural language processing task.
---

# NLP & Text Analytics

Process and analyze text data systematically. Choose the simplest method that answers the question before reaching for deep learning.

## 1. Text preprocessing

- **Inspection first**: examine raw text samples, encoding issues, HTML artifacts, special characters, and language mix before applying any cleaning.
- **Cleaning pipeline** (apply only what is necessary for the task):
  * Lowercasing (skip for NER, cased models, and acronym-sensitive tasks).
  * HTML/URL/email removal.
  * Unicode normalization (NFKD) and encoding fixes.
  * Punctuation and special character handling (preserve meaningful punctuation for sentiment).
  * Tokenization: use a tokenizer appropriate to the language and task (NLTK, spaCy, or model-specific tokenizers).
  * Stopword removal: only when bag-of-words methods are used. Never remove stopwords when using contextual embeddings or transformers.
  * Stemming vs Lemmatization: prefer lemmatization (spaCy, WordNet) over stemming for interpretability.
- **Do not over-clean**: aggressive preprocessing destroys signal. Justify every preprocessing step.

## 2. Text representation

| Method | When to Use |
|---|---|
| Bag-of-Words / TF-IDF | Baselines, small datasets, interpretable models |
| Word2Vec / GloVe / FastText | When pre-trained static embeddings suffice; OOV handling with FastText |
| Sentence embeddings (Sentence-BERT) | Semantic similarity, clustering, search |
| Transformer tokenizers (BERT, RoBERTa) | Fine-tuning for classification, NER, QA |
| LLM APIs (Gemini, GPT, Claude) | Zero/few-shot when labeled data is scarce; RAG pipelines |

Fit TF-IDF vocabulary on training data only. When using pre-trained embeddings, verify vocabulary coverage and handle out-of-vocabulary words explicitly.

## 3. Common NLP tasks

### Text Classification
- Start with TF-IDF + LogisticRegression / Naive Bayes baseline.
- Progress to fine-tuned transformers only when baseline is insufficient and labeled data is adequate (typically 1000+ examples per class).
- Evaluate with appropriate metrics: macro/weighted F1 for multi-class, PR-AUC for imbalanced classes.

### Sentiment Analysis
- For quick analysis: use pre-trained models (VADER for rule-based, pre-trained transformers for neural).
- For domain-specific sentiment: fine-tune on domain-labeled data. General-purpose sentiment models often fail on domain-specific language.
- Report the positive class definition and handle neutral/mixed sentiment explicitly.

### Named Entity Recognition (NER)
- Use spaCy NER or Hugging Face token classification pipelines.
- For custom entities: fine-tune on IOB/BIO-tagged data. Minimum ~200 annotated examples per entity type.
- Evaluate with entity-level F1 (strict and partial matching).

### Topic Modeling
- LDA (Latent Dirichlet Allocation): set number of topics, evaluate coherence scores, inspect top words per topic.
- BERTopic: for transformer-based topic discovery with better semantic coherence.
- Always show representative documents per topic for human validation.

### Text Similarity & Search
- Cosine similarity on TF-IDF vectors for keyword-level similarity.
- Sentence-BERT / embedding models for semantic similarity.
- For search: use FAISS or similar vector stores for efficient nearest-neighbor retrieval.

## 4. Transformer & LLM workflows

- **Fine-tuning**: use Hugging Face Trainer or equivalent. Monitor validation loss for early stopping. Freeze lower layers for small datasets.
- **Few-shot / zero-shot**: use prompt engineering with clear task instructions, examples, and output format specifications.
- **RAG (Retrieval-Augmented Generation)**: chunk documents appropriately (typically 256–512 tokens with overlap), embed with a suitable model, store in a vector database, retrieve top-k relevant chunks, and pass to the LLM with context.
- **Evaluation**: BLEU/ROUGE for generation, exact match / F1 for QA, human evaluation for open-ended tasks. Always establish baselines.

## 5. Multilingual considerations

- Identify the language(s) present in the dataset before choosing models.
- Use multilingual models (mBERT, XLM-R) for non-English or mixed-language data.
- Language detection: use `langdetect` or `fasttext` language identification.
- Tokenization: some languages (Chinese, Japanese, Thai) require specialized tokenizers.

## 6. Deliverable

Provide reproducible code with: text preprocessing pipeline, representation choice with justification, model training with proper text-aware train/test split, evaluation metrics appropriate for the task, and example predictions with confidence scores. Keep text in its original form alongside processed versions for debugging.
