# ChatGPT App Review Sentiment Analysis

Sentiment analysis of ~194K ChatGPT mobile app reviews using Python, pandas and TextBlob. The project covers data cleaning, rating and sentiment distribution, frequent terms, monthly trends and keyword-based feedback themes.

## Overview

The goal is to understand what users like and dislike about the ChatGPT app by combining star ratings with text sentiment.

**Questions answered**
- How do users rate the app, and how does text sentiment compare with star ratings?
- Which words and phrases show up in positive vs. negative reviews?
- How do review volume and sentiment change over time?
- Which feedback themes (accuracy, usefulness, ease of use, speed, features) draw the most praise and complaints?

## Video Walkthrough

🎥 [Watch the Loom walkthrough](https://www.loom.com/share/cacb47d0d11e4c5ca5bf2f4e9edb4b34) for a step-by-step explanation of the notebook, results and limitations.

## Dataset

- **Source:** [ChatGPT_Reviews_Analysis](https://github.com/Ayush-k-Das/ChatGPT_Reviews_Analysis) (`chatgpt_reviews.csv`)
- **Size:** 196,727 rows, 4 columns
- **Columns:** `Review Id`, `Review`, `Ratings` (1-5), `Review Date`
- **Period:** July 2023 to August 2024
- The notebook loads the CSV directly from GitHub. If the download fails, it asks you to upload the file manually.

## Methodology

1. **Cleaning:** standardized column names, removed 2,511 exact duplicates (194,216 rows remain), parsed dates, and flagged empty reviews.
2. **Exploration:** rating distribution and monthly review volume.
3. **Sentiment scoring:** TextBlob polarity (-1 to 1) and subjectivity (0 to 1) for 194,210 non-empty reviews.
   - Positive: polarity > 0.05
   - Negative: polarity < -0.05
   - Neutral: in between
4. **Rating vs. sentiment:** cross-tab and boxplot of polarity by star rating.
5. **Term analysis:** unigram and bigram counts (CountVectorizer with custom stop words) for positive and negative reviews.
6. **Trend analysis:** monthly review count with mean polarity and mean rating.
7. **Aspect analysis:** keyword matching into five themes, with mean polarity and positive/negative share per theme.

## Key Results

| Metric | Value |
|---|---|
| Reviews analyzed | 194,216 (194,210 scored) |
| Average rating | 4.50 / 5 (median 5) |
| Mean polarity | 0.447 |
| Mean subjectivity | 0.517 |
| Positive / Neutral / Negative | 75.7% / 20.6% / 3.7% |
| Peak review month | May 2024 |

**Rating distribution:** 1★ 11,966 · 2★ 3,346 · 3★ 8,046 · 4★ 22,603 · 5★ 148,255

### Rating vs. sentiment

| Rating | Negative | Neutral | Positive |
|---|---|---|---|
| 1★ | 27.8% | 43.0% | 29.2% |
| 2★ | 18.7% | 34.0% | 47.3% |
| 3★ | 8.7% | 27.3% | 64.0% |
| 4★ | 3.2% | 19.3% | 77.6% |
| 5★ | 1.2% | 18.4% | 80.4% |

### Feedback themes

| Theme | Reviews | Mean polarity | Negative | Positive |
|---|---|---|---|---|
| Usefulness and productivity | 25,716 | 0.326 | 2.7% | 84.9% |
| Accuracy and answer quality | 8,015 | 0.265 | 13.9% | 72.5% |
| Features and access | 7,566 | 0.211 | 12.2% | 61.8% |
| Ease of use and interface | 4,671 | 0.370 | 2.4% | 91.4% |
| Speed and reliability | 3,081 | 0.269 | 11.3% | 78.5% |

### Takeaways

- Users are strongly positive overall. Usefulness and ease of use are the best-received themes.
- Positive reviews use words like *good, best, nice, great, helpful, amazing*.
- Negative reviews use *bad, wrong, answer, worst, useless*, plus *voice, login* and *error*.
- Accuracy, feature access and speed have negative shares well above the 3.7% overall rate, so they are the main areas to improve.
- Review volume rises sharply through 2024 while sentiment stays positive.

## Tech Stack

- Python 3
- pandas, NumPy
- TextBlob
- scikit-learn (CountVectorizer)
- matplotlib, seaborn
- tqdm
- Google Colab / Jupyter Notebook

## How to Run

**Google Colab**
1. Open `Chargeability_Review_Sentiment_Analysis_with_Python.ipynb` in Colab.
2. Run all cells (`Runtime → Run all`). The dataset downloads automatically.

**Locally**
```bash
git clone <your-repo-url>
cd <your-repo-folder>
pip install pandas numpy matplotlib seaborn scikit-learn textblob tqdm jupyter
jupyter notebook
```
Then open the notebook and run all cells. Scoring ~194K reviews with TextBlob takes about a minute.

## Limitations

- TextBlob is lexicon-based and can miss sarcasm, slang and context. For example, some 1-star reviews that say "great app" score as positive.
- Theme detection uses keyword matching, so it is approximate and reviews can fall into several themes.
- Neutral labels include reviews with very short or ambiguous text, such as "ok".
- Only English-style text is handled reliably.

## Future Improvements

- Compare TextBlob with VADER or a transformer model (e.g. BERT).
- Use topic modeling (LDA or BERTopic) instead of fixed keyword themes.
- Look into the mismatch between low ratings and positive text.
- Track theme-level sentiment month by month.

## Project Structure

```
├── Chargeability_Review_Sentiment_Analysis_with_Python.ipynb
└── README.md
```

## Author

Keshav Malviya
(https://www.linkedin.com/in/keshav-malviya-9a59752a5/) · 

## Acknowledgements

Dataset by [Ayush-k-Das](https://github.com/Ayush-k-Das/ChatGPT_Reviews_Analysis).
