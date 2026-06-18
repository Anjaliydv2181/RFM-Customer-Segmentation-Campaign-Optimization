# RFM Customer Segmentation using PCA and K-Means Clustering

## Author
**Anjali Yadav**  
Indian Institute of Technology (IIT) Madras

## Introduction 
RFM segmentation is a marketing analysis method that involves analyzing customer behavior based on three key factors: recency, frequency, and monetary value. It helps businesses group customers into segments, enabling targeted and personalized marketing strategies. 

Recency indicates how recently a customer has made a purchase, while Frequency measures how often they make purchases, and Monetary represents the amount of money a customer spends on purchases.

This project applies RFM analysis to a UK-based online retail dataset spanning December 2010 to December 2011, containing transactions from 4,165 customers. Using PCA-enhanced K-Means clustering, customers are grouped into five actionable segments that inform targeted marketing campaigns.

## Data Collection 
The data is available on [Kaggle](https://www.kaggle.com/datasets/ersany/online-retail-dataset) with an Open Database License (ODbL).

This is a transnational dataset that contains all the transactions occurring between 01/12/2010 and 09/12/2011 for a UK-based and registered non-store online retail. The company mainly sells unique all-occasion gifts. Many customers of the company are wholesalers.

## Data Preparation 
- Calculate Recency, Frequency, and Monetary value for each customer. 
- Perform data cleaning by checking for duplicates, missing values, and dealing with outliers.
- Standardize the data to make it suitable for the machine learning model.
- Apply IQR-based outlier removal (5th–95th percentile) across all three RFM dimensions, reducing the dataset from 4,281 to 4,165 customers.

## Data Modeling
- **Principal component analysis (PCA)** is a linear dimensionality reduction technique used to reduce the number of variables of a data set, while preserving as much information as possible. It makes analyzing data points much easier and faster for machine learning algorithms. In this project, we used PCA with 2 dimensions to enhance the effectiveness of our K-Means clustering algorithm, enabling more accurate and efficient segmentation of our customer data. PCA was applied after StandardScaler normalization; the two principal components capture the dominant variance across the three correlated RFM dimensions, enabling cleaner cluster separation.
  
- **K-Means Clustering** is an Unsupervised Learning algorithm, which groups the unlabeled dataset into k-number clusters. It allows us to cluster the data into different groups and a convenient way to discover the categories of groups in the unlabeled dataset on its own without the need for any training.
  
  We first used The **Elbow Method**, which is a graphical method for finding the optimal K value.
  ![Elbow](https://github.com/maissaladjimi/RFM_Customer_Segmentation/assets/94018321/e7f5f120-944d-488e-8515-d6aad646fb8f)
  
  It revealed that the optimal K=5. After running the model, the following clusters were revealed
  
  ![PCA_KMeans](https://github.com/maissaladjimi/RFM_Customer_Segmentation/assets/94018321/a059ef81-4c32-4e7a-bbc7-8fb77794bb57)

## Cluster Interpretation 
In order to understand the characteristics of each cluster and identify the segment properties, we calculated the mean values for Recency, Frequency, and Monetary for each cluster. Additionally, for more visual interpretation, we visualized the distribution of clusters against each variable. 

![Means](https://github.com/maissaladjimi/RFM_Customer_Segmentation/assets/94018321/80b8bb61-27ba-4a21-ba17-d19ccff6658c)

![catplots](https://github.com/maissaladjimi/RFM_Customer_Segmentation/assets/94018321/62d7dc41-494d-4571-9811-f9ab7d869efe)

- **Cluster 0 — Inactive Shoppers** | Recency: 253.20 days | Frequency: 1.47 | Monetary: $49.19  
  Customers who haven't been active for an extended period, with no recent purchases.

- **Cluster 1 — Occasional Shoppers** | Recency: 54.58 days | Frequency: 2.04 | Monetary: $39.59  
  Customers with recent but infrequent purchases and low spending.

- **Cluster 2 — Frequent Spenders** | Recency: 30.66 days | Frequency: 10.41 | Monetary: $406.19  
  Customers who shop frequently with moderate to high spending. They engage often and spend moderately.

- **Cluster 3 — High-Value Loyal Shoppers** | Recency: 19.74 days | Frequency: 16.10 | Monetary: $913.78  
  VIP customers who shop very often and spend significantly. They engage frequently and spend generously.

- **Cluster 4 — Regular Shoppers** | Recency: 29.88 days | Frequency: 5.72 | Monetary: $149.89  
  Customers who shop regularly, with recent purchases. Moderate frequency and moderate spending.

## Customer Segments
After identifying the clusters, each customer was assigned its respective segment. These segments are essential for more effective and targeted marketing strategies tailored to their specific engagement and spending patterns. 

<div align="center">
  <img src="https://github.com/maissaladjimi/RFM_Customer_Segmentation/assets/94018321/65bce3e4-75d6-49b4-978b-414888d1ade0" alt="Customer Segments">
</div>

## Key Insights & Business Findings

### Revenue Concentration
The top 9.7% of customers (Frequent Spenders + High-Value Loyal Shoppers) generate **46.1% of total revenue** (~$216,482 of ~$469,790). This highlights extreme revenue concentration and the critical importance of retention campaigns for high-value segments.

### Segment Summary

| Segment | Customers | Share | Avg Recency | Avg Frequency | Avg Monetary | Revenue Share |
|---|---|---|---|---|---|---|
| Occasional Shoppers | 1,931 | 46.4% | 54.6 days | 2.0 orders | $39.59 | 16.3% |
| Inactive Shoppers | 969 | 23.3% | 253.2 days | 1.5 orders | $49.19 | 10.1% |
| Regular Shoppers | 862 | 20.7% | 29.9 days | 5.7 orders | $149.89 | 27.5% |
| Frequent Spenders | 299 | 7.2% | 30.7 days | 10.4 orders | $406.19 | 25.9% |
| High-Value Loyal Shoppers | 104 | 2.5% | 19.7 days | 16.1 orders | $913.78 | 20.2% |

### Behavioral Patterns
- **Recency gradient**: A clear separation exists between active customers (Clusters 2, 3, 4 with <31 days average recency) and lapsed customers (Cluster 1 at 55 days, Cluster 0 at 253 days).
- **Frequency-Monetary correlation**: The jump from Regular Shoppers (5.7 orders, $150 AOV) to Frequent Spenders (10.4 orders, $406 AOV) shows a ~2× frequency increase yields ~2.7× monetary increase, indicating disproportionate value from high-engagement customers.
- **Wholesale customer profile**: High monetary values (up to $1,696 for top loyal customers) reflect the business's predominantly wholesale customer base making repeat bulk orders.

## Campaign Optimization Strategies

RFM segmentation enables distinct marketing strategies for each customer group:

| Segment | Primary Goal | Key Tactic | Channel |
|---|---|---|---|
| Inactive Shoppers | Win-back | "We miss you" — 15–20% discount drip | Email, SMS |
| Occasional Shoppers | Frequency lift | Bundle offers, loyalty program enrollment | Email, retargeting |
| Regular Shoppers | Spend increase | Volume discounts, cross-sell recommendations | Email, on-site |
| Frequent Spenders | Retention + upgrade | Early access, VIP tier invitation | Email, personal outreach |
| High-Value Loyal Shoppers | Maximize LTV | Dedicated account manager, exclusive perks | Direct, phone |

For detailed campaign specifications, KPIs, budget allocation, and a 12-month implementation roadmap, see [Campaign Optimization Report](campaign_optimization_report.md).

## Repository Structure

```
RFM-Customer-Segmentation/
├── RFM_Segmentation.ipynb           # Full analysis notebook
├── rfm_segmentation.py              # Standalone Python script
├── customer_segments.csv            # Output: 4,165 customers with segment labels
├── campaign_optimization_report.md  # Campaign strategy and ROI analysis
└── README.md                        # Project documentation
```

## Usage
1. Download the dataset from [Kaggle](https://www.kaggle.com/datasets/ersany/online-retail-dataset) and save as `data.csv`.
2. Run the Jupyter notebook `RFM_Segmentation.ipynb` for the full interactive analysis.
3. Alternatively, run the standalone script: `python rfm_segmentation.py`
4. Output will be saved to `customer_segments.csv`.

**Dependencies**: `numpy`, `pandas`, `matplotlib`, `seaborn`, `scikit-learn`

## License
The dataset is made available under the [Open Database License (ODbL)](https://opendatacommons.org/licenses/odbl/1-0/).
