# Instagram Post Engagement Rate Analysis

## Overview
Content creators and businesses rely on Instagram engagement to grow their audience and reach potential customers. A common belief is that posting time affects how users interact with content. This project investigates whether posting in the **morning (6–10 AM)** versus the **evening (6–10 PM)** has a statistically significant effect on Instagram post engagement rate.

Using a dataset of 30,000+ Instagram posts, a two-sample t-test was conducted to compare mean engagement rates between the two time groups. Results indicate **no statistically significant difference**, a finding that held consistently across stratified analyses by content category and follower count.

---

## Dataset
- **Source:** [Instagram Analytics Dataset](https://www.kaggle.com/datasets/kundanbedmutha/instagram-analytics-dataset) (Kaggle)
- **Size:** ~30,000 Instagram posts; filtered to **12,500 posts** (morning and evening only)
- **No missing values** were present in the dataset
- Accounts were binned into four follower tiers for stratified analysis:
  - ≤ 5,000 followers
  - 5,000–10,000 followers
  - 10,001–20,000 followers
  - \> 20,000 followers

---

## Methods

### Dependent Variable
Engagement rate = total interactions (likes, comments, shares, saves) ÷ impressions

### Primary Analysis
A **two-sample independent t-test** was used to compare mean engagement rates between morning and evening posts.

Statistical assumptions were assessed before testing:
- **Normality:** Data is right-skewed, but with ~6,200 posts per group, the Central Limit Theorem ensures approximate normality
- **Equal variance:** Confirmed visually via boxplots and formally via **Levene's test** (p = 0.70); Student's t-test used with `equal_var=True`
- **Independence:** Each observation is a unique post; morning and evening periods do not overlap

A log transformation was tested to address skewness but did not meaningfully improve normality and was not applied.

### Stratified Analysis
To control for potential confounders, analyses were stratified across:
- **10 content categories** (Technology, Fitness, Beauty, Music, Photography, Food, Lifestyle, Travel, Fashion, Comedy) — Bonferroni-corrected threshold: α = 0.005
- **4 follower tiers** — Bonferroni-corrected threshold: α = 0.0125
- **40 combined subgroups** (content × follower) — Bonferroni-corrected threshold: α = 0.00125

---

## Results

| Analysis | Result |
|---|---|
| Primary t-test | t = -0.27, p = 0.79 — fail to reject null hypothesis |
| By content category (10 groups) | No significant results after Bonferroni correction |
| By follower tier (4 groups) | No significant results; lowest p = 0.21 |
| Combined subgroups (40 groups) | 2 nominally significant results; neither survived Bonferroni correction |

**Conclusion:** Posting time (morning vs. evening) has no statistically significant effect on Instagram engagement rate.

---

## Limitations
- The dataset may not equally represent all Instagram account types
- Potential presence of bot activity could introduce noise and distort true engagement patterns
- Future work could focus on verified organic engagement metrics and explore other posting-time windows

---

## Tools & Libraries
- **Python** (pandas, scipy, matplotlib, seaborn)
- **Jupyter Notebook**

---

## Files
| File | Description |
|---|---|
| `InstagramPostEngagementRate_Analysis.ipynb` | Full analysis notebook with code and visualizations |
