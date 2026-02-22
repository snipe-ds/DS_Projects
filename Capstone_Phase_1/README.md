### Project Title: Orb Redemption Recommender System

**Author**  
John Eckhardt  

---

#### Executive summary

This project analyzes Discord’s Orb redemption ecosystem and builds a baseline recommender system to predict users’ next redeemed SKU.

Using over 6 million historical redemption events, I conducted exploratory data analysis (EDA) to understand user behavior, SKU concentration, and marketplace structure. A global popularity-based recommender was then implemented and evaluated using a leave-last-interaction-out framework.

Baseline performance:

- **HitRate@1: 0.54**
- **HitRate@3: 0.62**
- **HitRate@5: 0.64**

Results indicate a highly concentrated redemption marketplace, where a small number of SKUs account for the majority of redemptions. This establishes a strong benchmark for future personalization efforts.

---

#### Rationale  
Why should anyone care about this question?

Orb redemptions represent a key engagement mechanism within Discord’s incentive ecosystem. Improving SKU recommendations can:

- Increase redemption frequency  
- Improve perceived reward relevance  
- Drive long-term user engagement  
- Improve discovery of underutilized catalog items  

Before investing in complex personalization systems, it is essential to understand how well simple baseline approaches perform and where they fall short.

---

#### Research Question  
What are you trying to answer?

Given a user’s historical redemption behavior, can we predict the next SKU they are likely to redeem?

---

#### Data Sources  
What data will you use to answer your question?

Data was extracted from Discord DW and consists of completed Orb redemption transactions Jan 1 to Feb 18 2026.

Each record includes:

- `user_id`
- `sku_id`
- `transaction_created_at`
- `product_line_name`
- `orbs_spent`
- `ending_orb_balance`

The dataset contains approximately:

- 6.1 million redemption events  
- 2.0 million multi-redeemer users  
- Hundreds of unique SKUs  

---

#### Methodology  
What methods are you using to answer the question?

1. **Data Cleaning & Preparation**
   - Filtered to completed redemption transactions
   - Verified absence of duplicate transaction groups
   - Removed missing critical identifiers
   - Restricted modeling to users with ≥2 redemptions

2. **Exploratory Data Analysis (EDA)**
   - Analyzed redemption frequency distribution
   - Examined SKU popularity concentration
   - Evaluated Orb spend distribution
   - Identified heavy-tailed marketplace structure

3. **Baseline Recommendation Model**
   - Implemented a global popularity recommender
   - Ranked SKUs by training-set redemption frequency
   - Applied leave-last-interaction-out evaluation
   - Generated Top-K recommendations per user

4. **Evaluation Metrics**
   - **HitRate@K**: Proportion of users whose held-out SKU appears in the Top-K recommendations
---

#### Results  
What did your research find?

Baseline model performance:

- **HitRate@1: 0.54**
- **HitRate@3: 0.62**
- **HitRate@5: 0.64**

Key findings:

- Over half of users redeemed the single most popular SKU.
- Expanding from Top-1 to Top-3 recommendations increases predictive coverage meaningfully.
- Expanding from Top-3 to Top-5 yields diminishing returns.
- SKU popularity is highly concentrated, with approximately 50% of redemptions driven by one dominant item.

These results demonstrate that a non-personalized popularity model performs strongly due to marketplace concentration. Future personalization efforts must demonstrate lift beyond this already high baseline.

---

#### Next steps  
What suggestions do you have for next steps?

**Near-Term Improvements (Capstone Scope)**

- Develop personalized ranking models using historical user behavior  
- Exclude previously redeemed items from recommendation lists  
- Implement collaborative filtering (matrix factorization or embeddings)  
- Measure lift relative to the popularity baseline  
- Evaluate long-tail performance excluding dominant SKUs  

**Long-Term Roadmap (Expanded Data Required)**

- Incorporate Orb earning behavior to support cold-start users  
- Leverage cohort and engagement features  
- Build content-based item similarity models using SKU metadata  
- Introduce diversity-aware ranking to improve catalog exploration  

---

#### Outline of project

- [EDA and Baseline Model Notebook](https://github.com/snipe-ds/DS_Projects/blob/main/Capstone_Phase_1/2026_Capstone_Orb_Recommender_System.ipynb)

---

##### Contact and Further Information

John Eckhardt