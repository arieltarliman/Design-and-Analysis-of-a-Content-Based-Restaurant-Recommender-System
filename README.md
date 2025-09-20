# Restaurant Recommendation System using Content-Based Filtering

## Overview
This project develops a **restaurant recommender system** for a marketplace website.  
The goal is to provide personalized suggestions to users by analyzing restaurant attributes and applying content-based filtering techniques.  

The system was built as part of a machine learning assignment focusing on **recommendation systems (dataset 3B)**.

---

## A. Exploratory Data Analysis (EDA)
- Conducted data inspection to understand the distribution of restaurant attributes such as cuisines, ratings, and locations.  
- Identified and handled anomalies:
  - Missing values in certain restaurant details.
  - Inconsistent entries in cuisine or category fields.  
- Key findings:
  - Certain cuisines dominate the dataset, while others are niche but valuable for personalized recommendations.
  - User ratings provide a useful signal to distinguish between popular and less favored restaurants.

---

## B. Content-Based Recommendation System
- Built a **content-based recommender** that uses restaurant attributes (e.g., cuisines, categories, keywords) to compute similarity.  
- Implemented using **TF-IDF vectorization** and **cosine similarity** to measure how similar restaurants are to each other.  
- Wrapped the system as a **function** that:
  - Takes a string input (e.g., a cuisine or restaurant name).  
  - Returns the **top 5 recommended restaurants** most similar to the input.  

---

## C. Evaluation
- Tested the recommendation function with at least **three different inputs**.  
- Observed that the recommended restaurants aligned well with the given inputs:
  - For cuisine-related queries, results matched similar cuisine categories.  
  - For restaurant-name queries, recommendations were close alternatives offering similar dining styles.  
  - For niche queries, the system successfully surfaced related but less common options.  

**Conclusion**: The content-based recommender demonstrates strong potential for improving user experience on the marketplace platform by delivering relevant and personalized restaurant suggestions.

---

## Requirements
- **Python 3.10**
- **Jupyter Notebook**
- Libraries: `pandas`, `numpy`, `scikit-learn`, `nltk`

---

## How to Run
1. Clone the repository:
   ```bash
   git clone https://github.com/arieltarliman/<your-repo-name>.git
   cd <your-repo-name>
