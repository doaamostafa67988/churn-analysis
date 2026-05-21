# 📊 Combating Subscriber Churn with Predictive Modeling & Customer Segmentation

An end-to-end data science project designed to mitigate subscriber loss (churn) and maximize platform revenue. By combining predictive classification algorithms with unsupervised clustering techniques, this system accurately identifies at-risk subscribers and categorizes users into distinct engagement profiles, making marketing strategies **27% more efficient**.

---

## 🎯 Business Objective
* **Churn Prevention:** Pinpoint high-risk subscribers before they cancel to enable timely, automated retention interventions.
* **Targeted Marketing:** Group active subscribers into behavior-based categories to run personalized campaigns, optimizing customer lifetime value (LTV).

---

## 🧠 Approach & Methodology

### 1. Churn Prediction (Classification)
We implemented and compared three classification models using an **80/20 train-test split** to evaluate churn risk based on user demographics and platform behavior:
* **Logistic Regression:** Serves as a strong statistical baseline.
* **Decision Tree Classifier (`max_depth=3`):** Provides a highly interpretable, rule-based approach.
* **Random Forest Ensemble (`n_estimators=10, max_depth=3`):** Combines multiple decision trees to minimize overfitting.

### 2. Subscriber Segmentation (Clustering)
To uncover latent user patterns, **K-Means Clustering** was performed strictly on scaled engagement metrics:
* **The Elbow Method** was used to find the optimal variance-reduction inflection point.
* **Silhouette Analysis** validated the cluster quality to arrive at an optimal cluster size of **$k=3$**.

---

## 📋 Dataset Description
The model trains on the `AZWatch_subscribers.csv` dataset, which includes the following features:
* `subscriber_id`: Unique key identifier for each subscriber.
* `age_group`: Demographic bracket (e.g., `18-24`, `25-34`, `45+`).
* `engagement_time`: Total duration spent interacting with the platform.
* `engagement_frequency`: Number of individual platform interactions within a set timeframe.
* `subscription_status` (**Target variable**): Account state (`Active`, `Canceled`, `Expired`, `Trial`).

---

## 🛠️ Data Preprocessing Pipeline
1. **Feature Dropping:** Excluded unique primary identifiers (`subscriber_id`) to prevent data leakage.
2. **Categorical Encoding:** Transformed the `age_group` column using **One-Hot Encoding** (`pd.get_dummies`) consistently across both train and test splits.
3. **Feature Scaling:** Applied a standard normalization routine (`StandardScaler`) to smooth out variations in scale between engagement time and interaction frequencies.

---

## 📈 Model Performance Matrix

| Classification Model | Evaluation Metric (Accuracy) |
| :--- | :--- |
| **Logistic Regression** | **92.5%** |
| **Decision Tree** | 92.0% |
| **Random Forest Ensemble** | 91.5% |

*The Logistic Regression baseline demonstrated top performance, achieving an optimal accuracy score of 92.5% on the unseen test matrix.*

---

## 👥 Customer Segmentation Insights

By analyzing feature averages across the $k=3$ clusters, we mapped out three well-defined customer profiles:

| Cluster ID | Avg Session Time | Session Interactions | Persona Profile |
| :---: | :---: | :---: | :--- |
| **Cluster 0** | 4 minutes | 5 | 📉 **Light Users** (At-Risk Segment) |
| **Cluster 2** | 9 minutes | 9 | 🔄 **Moderate Users** (Steady Segment) |
| **Cluster 1** | 7 minutes | 18 | 🔥 **High-Frequency Users** (Power Segment) |

---

## 🚀 Strategic Recommendations

Based on the subscriber segmentation profiles, the following tailored marketing actions are suggested:

* **Light Users (Cluster 0):** Engage with free premium content trials, customized re-engagement push notifications, and personalized content recommendations to build consistent habits.
* **Moderate Users (Cluster 2):** Introduce gamified milestones, user challenges, and curated course/content bundles to drive their metrics upward.
* **High-Frequency Users (Cluster 1):** Capitalize on high engagement by cross-selling premium subscription upgrades, creating customer ambassador/referral programs, and giving them early access to exclusive features.

---

## 🔮 Future Enhancements
1. Integrate additional behavioral tracks (such as feature clickstreams and payment histories).
2. Set up automated A/B testing infrastructure to measure the conversion rates of cluster-specific campaigns.
3. Build and package a real-time churn prediction endpoint using a FastAPI application loop.
4. Experiment with deep sequential neural network structures (RNNs/LSTMs) to capture shifting time-series behaviors.
