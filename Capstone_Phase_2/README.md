### Project Title: Reward Marketplace Optimization- Predicting Orb Redemption Behavior

**Author**  
John Eckhardt  

---

#### Executive Summary

Business Problem

Discord’s Orb reward ecosystem contains hundreds of redeemable items, but redemption activity is highly concentrated among a small number of SKUs. This limits discovery of new items and reduces the effectiveness of reward incentives.

The objective of this analysis is to evaluate whether recommendation models can improve the relevance of reward suggestions and increase redemption engagement.

Potential Business Impact
If deployed within the Orb reward system, improved recommendations could:
• Increase redemption conversion rate
• Increase total Orb sink volume
• Improve reward discovery
• Improve long-term engagement with reward campaigns
Even a 1–2% improvement in redemption rate could materially increase reward engagement across millions of users.

Results Summary
Four models were evaluated using a leave-last-interaction-out framework and the **HitRate@3** evaluation metric:

Model | HitRate@3
--- | ---
Global Popularity Baseline | **0.62**
Personalized History Model | 0.48
Collaborative Filtering (Matrix Factorization) | 0.50
Segmented Recommender | **0.60**

The results show that redemption activity is **extremely concentrated**, with a small number of SKUs accounting for the majority of redemptions. Because of this structure, the global popularity baseline performs very strongly.

However, the **segmented recommender approach performed closest to the baseline while introducing personalization**, making it the most promising direction for future optimization. This model applies different recommendation strategies depending on user behavior patterns, allowing more sophisticated models to be applied where they add value while retaining strong baseline recommendations for highly concentrated user segments.

These findings highlight that future improvements will require richer behavioral signals and longer historical windows to meaningfully outperform the popularity benchmark.

---

#### Rationale  
Why should anyone care about this question?

Orb redemptions represent a key engagement mechanism within Discord’s incentive ecosystem. Improving SKU recommendations can:

- Increase redemption frequency  
- Improve perceived reward relevance  
- Drive long-term user engagement  
- Improve discovery of underutilized catalog items  

Recommendation systems are widely used in digital marketplaces to guide user behavior and improve product discovery. Before investing in complex personalization systems, it is important to understand how well simple baseline approaches perform and where they fall short.

---

#### Research Question  
What are you trying to answer?

Given a user’s historical redemption behavior, can we predict the next SKU they are likely to redeem?

Additional supporting questions include:

- How well does a simple popularity-based recommender perform?
- Do personalized recommendation approaches outperform the baseline?
- Can different user behaviors benefit from different recommendation strategies?

---

#### Data Sources  
What data will you use to answer your question?

Data was extracted from the Discord data warehouse and consists of completed Orb redemption transactions between **January 1 and February 18, 2026**.

Each record includes:

- `user_id`
- `sku_id`
- `transaction_created_at`
- `product_line_name`
- `orbs_spent`
- `ending_orb_balance`

The dataset contains approximately:

- **6.1 million redemption events**
- **2.0 million multi-redeemer users**
- **Hundreds of unique SKUs**

For modeling purposes, the dataset was restricted to users with **two or more redemption events**, allowing the final redemption per user to be used as test data.

---

#### Methodology  
What methods are you using to answer the question?

1. **Data Cleaning & Preparation**

- Filtered to completed redemption transactions  
- Verified absence of duplicate transaction groups  
- Removed missing critical identifiers  
- Restricted modeling to users with **two or more redemptions**

---

2. **Exploratory Data Analysis (EDA)**

EDA focused on understanding marketplace dynamics:

- Redemption frequency distribution across users  
- SKU popularity concentration  
- Orb spend distribution  
- Identification of heavy-tailed marketplace behavior  

The analysis revealed strong concentration of redemptions among a small number of SKUs.

---

3. **Train/Test Evaluation Framework**

A **leave-last-interaction-out** approach was used:

- Each user’s final redemption is held out as the test observation  
- Remaining interactions form the training dataset  
- The model attempts to predict the held-out SKU

---

4. **Recommendation Models**

Several models were evaluated:

**Model 1 – Global Popularity Baseline**

- Ranks SKUs by overall redemption frequency  
- Recommends the same Top-K items to every user

**Model 2 – Personalized History Model**

- Recommends SKUs a user has historically redeemed most frequently

**Model 3 – Collaborative Filtering**

- Uses matrix factorization (TruncatedSVD) to learn latent relationships between users and SKUs

**Model 4 – Segmented Recommender**

Users were segmented based on redemption behavior:

- Sparse users (1 event)
- Repeat users (2+ events, same SKU) 
- Exploratory users (2+ events, not same SKU) 

Different recommendation strategies were applied to each segment.

---

5. **Evaluation Metrics**
Model performance was measured using **HitRate@K**.
HitRate@K measures the proportion of users whose actual held-out SKU appears in the Top-K recommendations generated by the model.

---

#### Results  
What did your research find?

Model performance was evaluated using **HitRate@3**, which measures whether the true held-out SKU appears within the top three recommendations generated by the model.

| Model | HitRate@3 |
|------|------|
| Global Popularity Baseline | 0.62 |
| Personalized History Model | 0.48 |
| Collaborative Filtering (Matrix Factorization) | 0.50 |
| **Segmented Recommender** | **0.60 – Selected to move forward and further optimize** |

**Key findings:**
- The global popularity baseline performed extremely strongly, correctly predicting the next redeemed SKU for approximately 62% of users.
- The personalized history model underperformed the baseline, indicating that many users repeatedly redeem the same dominant items rather than exhibiting diverse preferences.
- The collaborative filtering model improved slightly over simple personalization, but still did not outperform the baseline due to extreme SKU popularity concentration.
- The segmented recommender performed closest to the baseline, applying different recommendation strategies depending on user behavior patterns.

These findings demonstrate that marketplace concentration strongly favors popularity-based recommendations, and that future personalization improvements will require richer behavioral signals or expanded data sources.

#### Next steps  

**Long-Term Roadmap**
- Develop improved personalized ranking models using more historical user behavior  
- Implement collaborative filtering improvements  
- Incorporate Orb earning behavior to support cold-start users  
- Leverage cohort and other engagement features  
- Build content-based item similarity models using SKU metadata (eg. Categories vs. SKUs)  

---

#### Outline of project

- [Phase 1 Notebook - EDA and Baseline Model Notebook](https://github.com/snipe-ds/DS_Projects/blob/main/Capstone_Phase_1/2026_Capstone_Orb_Recommender_System.ipynb)
- [Phase 2 Notebook - Optimized Models & Comparison Notebook](https://github.com/snipe-ds/DS_Projects/blob/main/Capstone_Phase_2/2026_Capstone_Orb_Recommender_System_PHASE_2.ipynb)


---

##### Contact and Further Information

John Eckhardt