# One War, Many Narratives
## A Multi-Layer Text Analytics Study of Media Framing of the Iran-Israel Conflict 2026

**Course:** MBAG-408 — Text & Web Analytics
**Roll Number:** 24030302038
**Institution:** Sri Sathya Sai Institute of Higher Learning
**Submission:** March 2026

---

## Project Overview

This project analyses how the Iran-Israel War (February–March 2026) is framed across three distinct layers of discourse — news articles, editorial opinions, and public YouTube comments — using a comprehensive suite of text analytics techniques.

**Core Research Question:**
> Does the same conflict produce fundamentally different narratives across geopolitical perspectives — and does public discourse echo or diverge from media framing?

**SDG Alignment:**
- **SDG 16** — Peace, Justice and Strong Institutions
- **SDG 10** — Reduced Inequalities
- **SDG 17** — Partnerships for the Goals

---

## Folder Structure

```
24030302038_Master_Project/
│
├── README.md                            ← You are here
│
├── Datasets/
│   ├── Analysis Datasets/               ← Final cleaned datasets used for analysis
│   │   ├── News_Articles/
│   │   │   └── News_Articles.csv        ← 699 merged news articles (final)
│   │   ├── News_Opinion/
│   │   │   └── News_Public_Opinion.csv  ← 232 editorial/op-ed articles (final)
│   │   └── YT_Comments/
│   │       └── Youtube_Comments.csv     ← 1,671 YouTube comments (final)
│   │
│   └── Scraped Datasets/                ← Raw outputs from scrapers
│       ├── Editorial Opinions/
│       │   └── iran_us_public_opinion_20260324_113727.csv
│       ├── News Articles/
│       │   ├── 01_Iran_News_Raw.csv     ← NewsAPI raw collection
│       │   ├── 02_Iran_News_Full.csv    ← NewsAPI with full text extracted
│       │   ├── 03_Iran_News_RSS.csv     ← RSS scraper collection
│       │   ├── 04_news_merge_audit.csv  ← Merge audit trail
│       │   └── 05_news_merged_raw.csv   ← Merged before final cleaning
│       ├── Youtube Comments/
│       │   ├── iran_us_youtube_comments_20260324_140423.csv
│       │   └── iran_us_youtube_videos_20260324_140423.csv
│       └── Output/Visualizations/       ← Saved chart images
│
└── Python Files/
    ├── Analysis Files/
    │   └── 24030302038_Master_Project.ipynb  ← MAIN ANALYSIS — START HERE
    └── Scraper Files/
        ├── 24030302038_News_Scraper.ipynb         ← NewsAPI + RSS news collection
        ├── 24030302038_News_opinion.ipynb         ← Editorial opinion collection
        └── 24030302038_youtube_public_comments.ipynb ← YouTube comments collection
```

---

## How to Run

### Step 1 — Run the Analysis Notebook (no API keys needed)

The analysis notebook loads data directly from the `Datasets/Analysis Datasets/` folder.
All three datasets are pre-collected and ready to use.

```
Open: Python Files/Analysis Files/24030302038_Master_Project.ipynb
Run: All cells top to bottom
```

> **Platform:** Google Colab (recommended) or VS Code with Jupyter extension
> **Runtime:** ~15–20 minutes for full execution

---

### Step 2 — Re-collect Data (optional, requires API keys)

Only needed if you want to re-scrape fresh data.

| Scraper | File | API Key Required |
|---|---|---|
| News Articles (NewsAPI + RSS) | `24030302038_News_Scraper.ipynb` | Yes — NewsAPI key |
| Editorial Opinions (RSS) | `24030302038_News_opinion.ipynb` | No |
| YouTube Comments | `24030302038_youtube_public_comments.ipynb` | Yes — Google Cloud API key |

> **Note:** All scraper notebooks have a freeze mechanism. If the output file already exists, the scraper will skip collection and print a message. Delete the output file to re-scrape.

---

## Datasets

| Dataset | File | Size | Source | Period |
|---|---|---|---|---|
| News Articles | `News_Articles.csv` | 699 articles | NewsAPI + RSS Feeds | Feb 22 – Mar 23, 2026 |
| Editorial Opinions | `News_Public_Opinion.csv` | 232 op-eds | RSS Feeds | Feb 22 – Mar 24, 2026 |
| YouTube Comments | `Youtube_Comments.csv` | 1,671 comments | YouTube Data API v3 | Mar 9 – Mar 24, 2026 |

**News Articles — Perspectives covered:**

| Perspective | Articles | Key Sources |
|---|---|---|
| South Asian | 277 (39.6%) | The Indian Express, Hindustan Times, The Hindu, NDTV |
| Arab / Middle East | 145 (20.7%) | Al Jazeera English, Middle East Eye |
| Western | 143 (20.5%) | NPR, BBC News, The Guardian, Business Insider |
| Russian | 95 (13.6%) | RT, TASS |
| Turkish | 40 (5.7%) | Daily Sabah |
| Israeli | 5 (0.7%) | Times of Israel, Jerusalem Post |

---

## Techniques Applied

| Section | Technique | Applied To |
|---|---|---|
| Phase A2/B2/C2 | Tokenization, Lemmatization, Stopword Removal | All three datasets |
| Phase A3/B3/C3 | Sentiment Analysis (VADER) | All three datasets |
| Phase A4 | Word Clouds | News + Editorial |
| Phase A4 | N-Gram Analysis (Bigrams & Trigrams) | News + Editorial + YouTube |
| Phase A4 | TF-IDF Distinctive Keywords | News + Editorial + YouTube |
| Phase A4 | Keywords in Context (KWIC) | News + YouTube |
| Phase A5/B5/C5 | LDA Topic Modelling | All three datasets |
| Phase A5 | LSA + Cosine Similarity | News Articles |
| Phase A6 | K-Means Clustering (K=10) | News Articles |
| Phase A6 | Hierarchical Clustering | News Articles |
| Phase A7/B6 | Named Entity Recognition (spaCy) | News + Editorial |
| Phase A8/B7 | Text Classification (NB, LR, SVM) | News + Editorial |
| Phase A9 | Extractive Text Summarization | News Articles |

---

## Key Findings

1. **Narratives diverge measurably** — SVM classifier achieves 62.6% (News) and 86.2% (Editorial) accuracy predicting geopolitical perspective from text alone — 3× above random baseline.

2. **The negativity gradient** — News (−0.639) → Editorial (−0.505) → YouTube (−0.132). The public is 4.9× less negative than institutional media about the same conflict.

3. **The peace deficit** — The word "peace" appears 0.5 times per 100 news articles. Diplomacy topics receive 2.0% of news coverage and 0.0% of YouTube coverage.

4. **Six different wars** — South Asian media frames it as an energy crisis; Russian media as US-Israeli aggression; Turkish media as a regional reconfiguration; Arab media as military operations with a Palestinian dimension; Western media as a leadership crisis; YouTube as spiritual warfare.

5. **YouTube introduces unique frames** — Religious framing, conspiratorial cross-referencing, and direct moral accusation appear in YouTube comments but are absent from all 931 institutional documents.

---

## Dependencies

```
pip install pandas numpy matplotlib seaborn wordcloud
pip install nltk scikit-learn gensim spacy
pip install newsapi-python newspaper3k lxml_html_clean feedparser
python -m spacy download en_core_web_sm
```

---

## Notes

- The `~$` prefix files (e.g. `~$030302038_Report.docx`) are temporary Word lock files created when a document is open. They can be safely deleted.
- The `.tmp` file (`~WRL0706.tmp`) is also a Word temporary file — safe to delete.
- JSON files in `Scraped Datasets/` are companion outputs of the CSV scrapers — same data, different format. Not needed for analysis.
