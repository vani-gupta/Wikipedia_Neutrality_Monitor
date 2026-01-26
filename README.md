# Wikipedia_Neutrality_Monitor
## Multilingual Sentiment and Bias Analysis of Wikipedia Articles

This repository presents the core analytical components of a research-driven project developed in collaboration with **Wikimedia** and **IBM**, focusing on the **measurement of sentiment and neutrality across multiple language editions of Wikipedia**.

The project investigates how **sentiment signals and potential bias patterns vary cross-lingually**, even when articles describe the same entities or topics. Such variations raise important questions for knowledge equity, neutrality, and responsible AI in multilingual information systems.

Only the **two central analytical notebooks** are included in this repository.

## Research Context and Motivation

Wikipedia aspires to a *Neutral Point of View (NPOV)*; however, neutrality is not only a function of factual accuracy but also of **linguistic framing, sentiment, and implicit bias**, which may differ across languages due to cultural, social, or political contexts.

This work addresses the following research questions:

- How does **sentiment polarity** vary across languages for the same Wikipedia entities?
- Can **lexicon-based methods**, when adapted per language, provide reliable sentiment signals for encyclopedic text?
- To what extent can **zero-shot large language models** detect bias patterns without task-specific training data?

## Data Description

- **Languages:** English (EN), German (DE), Spanish (ES), Hindi (HI), Chinese (ZH)
- **Scale:**
  - ~1,000 entities
  - ~5,000 Wikipedia articles
  - Diverse topical categories
- **Data sources:** Wikipedia dumps and Wikipedia API
- **Preprocessing steps:**
  - Removal of references and markup
  - Extraction of clean article text for analysis

<img width="851" height="219" alt="image" src="https://github.com/user-attachments/assets/096af453-341a-426a-9557-fac759786487" />


## Notebook 1: Language-Specific Lexicon-Based Sentiment Labelling

**File:** `language_specific_labelling.ipynb`

### Objective

To estimate **continuous sentiment scores** for Wikipedia articles using **language-appropriate sentiment lexicons**, avoiding English-centric bias common in multilingual sentiment analysis.

### Methodological Approach

This notebook implements a **lexicon-based sentiment analysis framework**, combining:

1. **VADER** as a reference baseline (primarily for English)
2. **Language-specific sentiment lexicons**, selected based on:
   - Linguistic specificity
   - Contextual suitability for formal, encyclopedic text
   - Availability of real-valued sentiment scores

| Language | Lexicon | Approx. Vocabulary Size |
|--------|--------|--------------------------|
| English | NRC Emotion | ~14,000 |
| German | SentimentWS | ~34,000 |
| Spanish | NRC Community | ~15,000 |
| Hindi | AffectiveSpace | ~40,000 |
| Chinese | NTUSD | ~11,000 |

Each article is mapped to:
- A **normalized sentiment score**
- Associated **semantic or emotional labels** (where available)

### Findings

- Sentiment distributions differ substantially across languages for identical entities.
- Language-specific lexicons yield **more stable and interpretable sentiment estimates** for formal text domains such as Wikipedia.
  
<img width="953" height="524" alt="Screenshot 2026-01-26 at 10 00 16 PM" src="https://github.com/user-attachments/assets/025e8ffb-ece7-4707-87a7-bf52690f49fa" />

---

## Notebook 2: Zero-Shot Bias Detection Using BART

**File:** `bart_modelling.ipynb`

### Objective

To detect **latent bias signals** in Wikipedia articles using **zero-shot natural language inference models**, without requiring manually labeled bias datasets.

### Bias Taxonomy

The analysis operationalizes bias across the following categories:

- **Social Bias** (e.g., gender, race, age)
- **Political Bias**
- **Media Bias** (framing, omission, coverage)
- **Cultural Bias**

### Model Choice and Rationale

- **BART-MNLI** is used for zero-shot classification due to:
  - Strong semantic reasoning capabilities
  - Flexibility in defining bias hypotheses
  - Multilingual generalization potential
- Comparative experiments were conducted using **XLM-R** for performance validation

Zero-shot classification was selected to:
- Avoid costly annotation processes
- Enable rapid iteration across bias definitions
- Support multilingual scalability

<img width="748" height="411" alt="Screenshot 2026-01-26 at 10 01 05 PM" src="https://github.com/user-attachments/assets/337a65a5-85c4-4a34-94b5-57e14a2e08d7" />

### Results

- Bias-related signals were identified in approximately **13% of articles (639 / 5000)**.
- The strongest and most consistent signals were observed for:
  - **Social bias**
  - **Cultural bias**
- Political bias detection was limited by **low class support** in the dataset.

<img width="546" height="213" alt="Screenshot 2026-01-26 at 10 02 11 PM" src="https://github.com/user-attachments/assets/38da1405-0540-4377-a3de-7f6b67b28782" />
<img width="618" height="222" alt="Screenshot 2026-01-26 at 10 02 33 PM" src="https://github.com/user-attachments/assets/cecd5531-e9fc-4765-a26f-4487a16377eb" />
<img width="1173" height="302" alt="Screenshot 2026-01-26 at 10 02 46 PM" src="https://github.com/user-attachments/assets/3a6e8651-c052-4df0-b4d8-546f098a6c99" />

## Discussion and Implications

Key observations from this study include:

- Neutrality is **not uniform across language editions** of Wikipedia.
- Lexicon-based sentiment analysis remains effective when **linguistically grounded**.
- Zero-shot LLMs offer a viable pathway for **scalable bias detection** in low-resource or unlabeled settings.
- Combining **symbolic (lexicon-based)** and **neural (LLM-based)** methods provides complementary analytical perspectives.

## Limitations and Future Work

- Expansion of bias taxonomies and explainability methods
- Human-in-the-loop validation of detected bias signals
- Finer-grained article section analysis
- Longitudinal neutrality tracking across Wikipedia revisions

