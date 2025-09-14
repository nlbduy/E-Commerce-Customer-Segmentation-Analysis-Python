# **E-Commerce Customer RFM Segmentation Analysis with Python**

Author: Nguyen Luu Bao Duy

Tool Used: Python

# **📑** Table of Contents

- [**📌** Project Overview](#-------project-overview)

- [🔎 RFM Methodology](#---rfm-methodology)

- [**📂** Dataset](#-------dataset)

- [**📊 Implementation Steps**](#-----implementation-steps--)
  * [**1️⃣ Data Preparation**](#--1---data-preparation--)

  * [**2️⃣ EDA and Data Reprocessing**](#--2---eda-and-data-reprocessing--)

  * [**3️⃣ Business Overview**](#--3---business-overview--)

  * [4️⃣ RFM Analysis](#4---rfm-analysis)

- [**🚀 Final Conclusions and Recommendations**](#-----final-conclusions-and-recommendations--)

# **📌** Project Overview

## 💼 Business Context

SuperStore is a global retail enterprise with a large scale of operations and a diverse customer base. The company has a strong presence in the European market, particularly in the United Kingdom (UK), serving thousands of customers and processing a high volume of orders.

The Christmas season represents a critical period of the year, when shopping demand peaks and festive campaigns are widely executed. To capitalize on this opportunity, the Marketing department is preparing promotional programs, seasonal gifts, and personalized email campaigns - all to r**eward loyal customers** for their continued support and to **strengthen relationships with potential customers**, with the goal of turning them into long-term loyal buyers.

However, with the customer base expanding significantly this year and transaction data becoming more complex, the Marketing team can no longer rely on manual customer segmentation as in previous years. In addition, the absence of a clear segmentation framework makes it difficult to design effective messages and tailored offers.

To address these challenges, the Marketing department has proposed a collaboration with the Data Analytics team to develop an **automated customer segmentation model**. The chosen approach is the **RFM (Recency - Frequency - Monetary)** framework, which enables the company to identify customer segments systematically and align marketing strategies with each group more efficiently.

## 🎯 Project Objectives

The objective of this analysis is to classify existing customers into distinct behavioural segments using the **RFM (Recency - Frequency - Monetary)** model. This segmentation will enable the Marketing team to design more effective personalized campaigns, enhance customer lifetime value, and optimize acquisition and retention costs.

## 👥 Target audience

- Sales & Marketing Team
- Product Team
- Customer Service Team
- Analytics and Data Team

## **🛰️ Scope of Analysis**

- **Data Source**: Simulated sales transaction dataset of SuperStore (synthetic data).
- **Reference Date for Analysis**: The analysis is assumed to be conducted on **December 31, 2011**.
- **Currency**: All transaction values are assumed to be in **USD**.
- **Unit of Analysis**: The analysis focuses on **actual purchase transactions with an order value greater than zero**. Internal transactions, expense payments, system test records, free gifts, and sample items have been excluded to ensure an accurate reflection of customer purchasing behavior.

# 🔎 RFM Methodology

## **🏗️ What is the RFM Model?**

RFM (Recency – Frequency – Monetary) is a customer segmentation model based on transaction history. It helps assess both the value of customers and their level of engagement with the business. Each customer is scored across three dimensions:

- **Recency (R):** The time elapsed since the customer’s most recent purchase. The shorter the gap, the higher the likelihood of repeat purchases. A longer gap, in contrast, indicates a higher risk of churn.
- **Frequency (F):** The number of transactions made within a defined period. Customers who purchase more frequently tend to have a stronger relationship with the brand and respond more actively to marketing efforts.
- **Monetary (M):** The total amount of money a customer has spent. This reflects their spending capacity and their overall contribution to company revenue.

## **🌱 Why Apply the RFM Model in Customer Segmentation?**

Applying the RFM model provides several advantages:

- Increases the effectiveness of personalized marketing campaigns.
- Improves Customer Lifetime Value.
- Supports segmentation for targeted product launches.
- Strengthens customer loyalty and engagement.
- Reduces churn by identifying at-risk customers.
- Optimizes marketing spend and improves ROI.
- Enhances the performance of remarketing and retargeting campaigns.

## **🛠️ How Are Customer Segments Defined Using RFM?**

Each customer is evaluated using the three RFM dimensions:

- **Recency:** Calculated as the difference between the analysis date and the customer’s last transaction date.
- **Frequency:** Measured by counting the total number of invoices or transactions per customer.
- **Monetary:** Measured by summing the total value of all purchases across the customer’s lifetime.

Once calculated, the values for each dimension are divided into five equal groups (quintiles), with scores assigned from 1 to 5. A score of 1 represents the lowest value, while a score of 5 represents the highest.

The scoring direction differs by dimension:

- **Recency:** Lower values (more recent activity) receive higher scores.
- **Frequency and Monetary:** Higher values receive higher scores.

By combining these three scores, each customer is assigned an **RFM score**, resulting in up to **125 unique combinations**. These combinations are then mapped into well-defined customer segments according to a segmentation framework.

| Segment                   | RFM Scores                                                                                                             | Definition                                                                                                                                                                                                    |
|----------------------------|------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 🏆 **Champions**          | 555, 554, 544, 545, 454, 455, 445                                                                                      | These are the most valuable customers who have purchased recently, buy frequently, and spend the most. They are highly loyal, willing to spend generously, and are very likely to make another purchase soon. |
| 💎 **Loyal Customers**    | 543, 444, 435, 355, 354, 345, 344, 335                                                                                 | These customers spend at a medium to high level and purchase very frequently.                                                                                                                                 |
| 💡 **Potential Loyalists**| 553, 551, 552, 541, 542, 533, 532, 531, 452, 451, 442, 441, 431, 453, 433, 432, 423, 353, 352, 351, 342, 341, 333, 323 | These are relatively new customers who have purchased recently, spend at a moderate level, and have already made more than one purchase.                                                                      |
| ✨ **New Customers**       | 512, 511, 422, 421, 412, 411, 311                                                                                      | These are brand-new customers who made their first purchase recently, with low transaction value and low frequency.                                                                                           |
| 🌱 **Promising**           | 525, 524, 523, 522, 521, 515, 514, 513, 425, 424, 413, 414, 415, 315, 314, 313                                         | These customers purchased recently with relatively high value but have not yet become frequent buyers.                                                                                                        |
| 👀 **Need Attention**      | 535, 534, 443, 434, 343, 334, 325, 324                                                                                 | These customers used to have decent purchase frequency and value but have not bought again recently.                                                                                                          |
| 😴 **About To Sleep**      | 331, 321, 312, 221, 213, 231, 241, 251                                                                                 | These customers have not purchased for quite a while and previously had low frequency and low transaction values.                                                                                             |
| ⚠️ **At Risk**             | 255, 254, 245, 244, 253, 252, 243, 242, 235, 234, 225, 224, 153, 152, 145, 143, 142, 135, 134, 133, 125, 124           | These customers have not purchased for a long time, but they used to buy very frequently with medium to high transaction values.                                                                              |
| 🚨 **Cannot Lose Them**    | 155, 154, 144, 214, 215, 115, 114, 113                                                                                 | These are long-inactive customers who previously purchased often and with high value. Without timely actions to re-engage, the business risks losing them permanently.                                        |
| ❄️ **Hibernating Customers**| 332, 322, 233, 232, 223, 222, 132, 123, 122, 212, 211                                                                 | These customers have been inactive for a long period, with low purchase frequency and low transaction value.                                                                                                  |
| ⛔ **Lost Customers**      | 111, 112, 121, 131, 141, 151                                                                                           | These are customers who have not returned for a very long time, with the lowest purchase frequency and transaction value. They are likely to have stopped using the product or switched to competitors.       |


# **📂** Dataset

## **📝** Data Description

- Dataset: SuperStore dataset
- Format: XLSX
- Components:
    - Sheet **E-Commerce Retail**
        - Size: 541,909 records x 8 columns
        - Contains **detailed e-commerce transactions** at the product level. Each row represents a specific item purchased within an order, including both product information and customer details.
    - Sheet **Segmentation**
        - Size: 11 records x 2 columns
        - Contains segment definitions and their RFM score.

## **⚙️ Data Schemas**

**1️⃣ E-Commerce Retail**

| Column | Description | Data Type |
| --- | --- | --- |
| **InvoiceNo** | Invoice number. Unique identifier for each transaction. Prefix ‘C’ indicates a cancellation. | `object` |
| **StockCode** | Product code. Unique identifier for each product. | `object` |
| **Description** | Product name/description. | `object` |
| **Quantity** | Number of units of the product in the transaction. Negative values may indicate returns. | `int64` |
| **InvoiceDate** | Date and time when the transaction occurred. | `datetime64[ns]` |
| **UnitPrice** | Price per unit of the product. | `float64` |
| **CustomerID** | Unique identifier for each customer. Some missing values exist. | `int64` |
| **Country** | Country where the customer resides. | `object` |

**2️⃣ Segmentation**

| **Column** | **Data Type** | **Description** |
| --- | --- | --- |
| Segment | `object` | Customer group label based on RFM analysis. |
| RFM Score | `object` | Combination of Recency, Frequency, and Monetary scores mapped to each segment. |

## **🗓️** Time Frame

- The dataset includes records spanning from **December 1, 2010** to **December 9, 2011**.
- The analysis is conducted for the same period.

# **📊 Implementation Steps**

## **1️⃣ Data Preparation**

### **1.1. Import packages and modules**

Input:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

### 1.2. Import Dataset

Input:

```python
# Data mounting
from google.colab import drive
drive.mount('/content/drive')
```

```python
# Read files
ecom_df_original = pd.read_excel('/content/drive/MyDrive/Module Projects/Python/ecommerce_retail_data.xlsx', sheet_name='E-Commerce Retail')
segment_def_df_original = pd.read_excel('/content/drive/MyDrive/Module Projects/Python/ecommerce_retail_data.xlsx', sheet_name='Segmentation')
```

```python
# Copy to other dataframes to ensure data integrity
ecom_df = ecom_df_original.copy()
segment_def_df = segment_def_df_original.copy()
```

## **2️⃣ EDA and Data Reprocessing**

### 2.1. **Examine missing data and data types**

Input:

```python
ecom_df.info()
```

Output:

<img width="2000" height="459" alt="Image" src="https://github.com/user-attachments/assets/a4b12a76-7d12-485b-8607-3bfbfedcf1dd" />

👉🏼 Column `Description` and `CustomerID` contain missing values. Data types for each column are reasonable.

<details>
<summary>❓<b>Examine <code>InvoiceNo</code></b>: All invoices that start with a letter are either canceled invoices or bad debt adjustment invoices. Both should be removed.</summary>
    
Input:
    
```python
# Check dtypes in col InvoiceNo
ecom_df['InvoiceNo'].apply(type).value_counts()
```
    
Output: 

<img width="2000" height="292" alt="Image" src="https://github.com/user-attachments/assets/fdde0f94-d1b3-4e32-b666-d339f5b1d6f0" />
    
Input:

```python
## Find canceled trans which starts with 'C'
len(ecom_df[ecom_df['InvoiceNo'].str.startswith('C', na=False)]['InvoiceNo'])
```
    
Output: 9288
  
Input:
  
```python
# Get a look on trans which don't start with 'C'
str_inv = ecom_df[ecom_df['InvoiceNo'].apply(type) == str]
str_inv[~str_inv['InvoiceNo'].str.startswith('C')]
```
    
Output:

<img width="2000" height="316" alt="Image" src="https://github.com/user-attachments/assets/ad3f4d0f-c2df-4906-9677-df32fdf02e30" />

    
👉🏼 The `InvoiceNo` column contains 9,291 string values, of which 9,288 are canceled invoices (starting with 'C') and 3 are bad debt adjustment invoices (starting with 'A'). 

👉🏼 All invoices containing alphabetic characters should be removed.
    
Input:

```python
# Remove all rows that start with a letter
alpha_starting_mask = ecom_df['InvoiceNo'].str[0].str.isalpha()
ecom_df = ecom_df[~alpha_starting_mask.fillna(False)]
# Cast to str type
ecom_df['InvoiceNo'] = ecom_df['InvoiceNo'].astype(str)
```
</details>

<details>
<summary>❓<b>Examine <code>StockCode</code></b>: Some product codes represent non-merchandise codes that serve the service, adjustment, and operational purposes. All should be removed.</summary>

Input:

```python
# Check dtypes in col StockCode
ecom_df['StockCode'].apply(type).value_counts()
```

Output:

<img width="2000" height="295" alt="Image" src="https://github.com/user-attachments/assets/4edf873d-0a84-4364-9701-051dac64be86" />

Input:

```python
## Find trans which are non-merchandise codes (payments, system tests, shipping charges,etc.)
non_trans_mask = ecom_df['StockCode'].astype(str).apply(lambda x: x.strip().replace(' ','').isalpha())
ecom_df[non_trans_mask]['StockCode'].unique()
```

Output: 

<img width="2000" height="89" alt="Image" src="https://github.com/user-attachments/assets/a0272ead-93dd-4f12-ad6a-bf9c4a803b43" />


👉🏼 The `StockCode` column contains some codes that are not actual products. 

👉🏼 All non-merchandise codes should be removed.

Input:

```python
# Remove non-merchandise codes
ecom_df = ecom_df[~non_trans_mask]
# Cast to str type
ecom_df['StockCode'] = ecom_df['StockCode'].astype(str)
```

</details>

<details>

<summary>❓<b>Examine <code>Description</code></b>: Cast Description to <code>str</code> type. </summary>

Input:

```python
# Cast to str
ecom_df['Description'] = ecom_df['Description'].astype(str)
```

</details>

<details>
  
<summary> ❓<b>Examine <code>CustomerID</code></b>: Some customers have made purchases anonymously. They should be labeled as an anonymous customer with the pattern anonymous + <code>InvoiceNo</code>.</summary>

Input:

```python
'''
For NaN values in column CustomerID, 
if a customer with no ID but still finished a transaction, 
they could purchase anonymously (Guest checkout, POS trans).
Fill NaN with the pattern "anonymous_" + that customer’s InvoiceNo
'''

## Create a mask for rows where CustomerID is NaN
cus_na_mask = ecom_df['CustomerID'].isna()

## Replace values in those rows with "anonymous_" + the corresponding InvoiceNo
ecom_df.loc[cus_na_mask, 'CustomerID'] = 'anonymous_' + ecom_df.loc[cus_na_mask, 'InvoiceNo']

# Ensure CustomerID is stored as str type
ecom_df['CustomerID'] = ecom_df['CustomerID'].astype(str)
```

Input:

```python
'''
Verify whether 'anonymous' customers truly represent missing IDs 
by checking if their invoices overlap with identified customers
'''
# Create a list of invoices for anonymous customers
anonymous_inv = ecom_df[ecom_df['CustomerID'].str.startswith('anonymous')]['InvoiceNo'].drop_duplicates()
# Create a list of invoices for identified customers
identified_inv = ecom_df[~ecom_df['CustomerID'].str.startswith('anonymous')]['InvoiceNo'].drop_duplicates()
# Check if any invoices appear in both groups
anonymous_inv.isin(identified_inv).sum()
```

Output: `np.int64(0)`
  
</details>

### 2.2. **Examine summary statistics**

Input:

```python
ecom_df.describe()
```

Output:

<img width="2000" height="495" alt="Image" src="https://github.com/user-attachments/assets/5aa39b9f-47a9-437f-9523-bb9dfd3c187a" />

Invoices with `UnitPrice` = 0 make no contribution to the Monetary metric.

👉🏼 They could be from canceled, returned, or FOC orders and should be removed.

Input:

```python
# Retain only records with UnitPrice > 0
ecom_df = ecom_df[ecom_df['UnitPrice'] > 0]
```

Re-examine summary statistics:

Input:

```python
ecom_df.describe()
```

Output:

<img width="2000" height="500" alt="Image" src="https://github.com/user-attachments/assets/038a0246-0059-4d06-ad83-25f1dc22d0b1" />

👉🏼 Removing records with `UnitPrice` = 0 helps remove negative `Quantity` (which is due to returned or canceled orders)

### 2.3. **Examine duplicates**

Input:

```python
# Check random duplicates
ecom_df[ecom_df.duplicated(keep=False)].sort_values(by=['InvoiceNo', 'StockCode']).query('InvoiceNo == "536409"')
```

Output:

<img width="2000" height="507" alt="Image" src="https://github.com/user-attachments/assets/a22fd339-ca2d-416d-8510-331e48a1cab2" />

After checking random duplicates, some rows appear to be completely identical. However, there is not enough evidence to remove them, as each row could represent a separate invoice line from the same invoice, with the same product and quantity.

👉🏼 **Invoice Line Number** is needed to confirm whether these are true duplicates.

👉🏼 For now, the dataframe will be kept unchanged.

### **2.4. Examine outliers**

Input:

```python
fig, ax = plt.subplots(nrows=1, ncols=2, figsize=(14, 6))
# Boxplot for UnitPrice
sns.boxplot(data = ecom_df, y ='UnitPrice', ax=ax[0])
ax[0].set_title('Boxplot of UnitPrice')
# Boxplot for Quantity
sns.boxplot(data = ecom_df, y = 'Quantity', ax=ax[1])
ax[1].set_title('Boxplot of Quantity')
plt.suptitle('Numeric variables outliers validation')
plt.show()
```

Output:

<img width="2000" height="941" alt="Image" src="https://github.com/user-attachments/assets/50ef8cfc-fe8c-4be1-9c50-6f61f9f45693" />

The variables `UnitPrice` and `Quantity` show clear outliers.

After filtering and reviewing these outliers, no abnormal outliers were found; the data is consistent with the product descriptions. So, there is not enough evidence to remove outliers.

👉🏼 Outliers are retained to accurately reflect customer purchasing behavior.

## **3️⃣ Business Overview**

### 3.1. General Sales Performance

Input:

```python
# Add col Period representing monthly transaction time
ecom_df['Period'] = ecom_df['InvoiceDate'].dt.to_period('M')
# Calculate Total Sales
ecom_df['TotalSales'] = ecom_df['Quantity']*ecom_df['UnitPrice']
# Calculate Number of Customer, Number of Orders, Monthly Sales and AOV
overview_df = (ecom_df.groupby('Period').agg(NumberofCustomers = ('CustomerID', 'nunique'),
                                            NumberofOrders = ('InvoiceNo', 'nunique'),
                                            MonthlySales = ('TotalSales', 'sum'))
                                            .assign(AOV = lambda df: df['MonthlySales']/df['NumberofOrders'])
                                            .reset_index())
```

After calculating the metrics, we visualize them in charts:

<img width="2000" height="429" alt="Image" src="https://github.com/user-attachments/assets/8ab9067a-255a-438b-9762-34f8c49d5697" />

In 2011, SuperStore recorded **significant growth from September to November**, the months leading up to Christmas. Number of Customers, Number of Orders, and Total Sales all peaked in November, confirming this period as the core shopping season and the best window for marketing initiatives.

However, Average Order Value (AOV) declined slightly during this growth phase, indicating that **revenue expansion was primarily driven by more customer acquisition and order volume rather than higher spend per order**. Interestingly, AOV spiked in early December, suggesting that customers might have shifted toward fewer but higher-value purchases during the holiday period.

It is important to note that December’s sharp drop in customer count, orders, and revenue is due to the dataset ending on December 9th, and thus does not represent full-month performance. 

Overall, the analysis highlights a clear seasonality pattern with **Q4** emerging as the strongest growth phase, providing an ideal **opportunity for targeted marketing campaigns**.

Correlation Analysis
To further validate the revenue drivers, a correlation analysis was conducted between **Monthly Sales**, **Number of Orders**, and **Average Order Value (AOV)**.

<img width="2000" height="912" alt="Image" src="https://github.com/user-attachments/assets/9e6ddce5-6da6-4d0c-8bc9-9044fb50cb07" />

The correlation matrix and scatter plots indicate a **very strong linear relationship** between **monthly revenue** and the **number of orders** (correlation coefficient = 0.93). In contrast, the Average Order Value (AOV) shows little to no meaningful correlation with either metric.

This highlights that SuperStore’s revenue growth is primarily driven by **order volume** rather than increases in order value. From a strategic perspective, the focus should be on **encouraging higher purchase frequency and order counts**, especially during peak months, instead of relying solely on selling higher-value products.

In addition, we define the top 10 products with the best performance.

<img width="2000" height="639" alt="Image" src="https://github.com/user-attachments/assets/04272e05-9562-4121-b88e-61ca376154ec" />

## 4️⃣ RFM Analysis

### 4.1. Reform table Segmentation

We may need to convert the original wide nested segmentation table into a long-format table to ensure data standardization and make processing and analysis more efficient.

Input:

```python
rfm_map_df = segment_def_df.copy()
# Split the RFM Score string into a list of integers
rfm_map_df['RFM Score'] = rfm_map_df['RFM Score'].apply(lambda x: [int(score.strip()) for score in x.split(',')])
# Explode each value in the list into a single row
rfm_df_long_2 = rfm_map_df.explode('RFM Score').reset_index(drop=True)
# Rename the column
rfm_df_long_2.rename(columns={'RFM Score': 'RFM_Score'}, inplace=True)
```

Output:

<img width="2000" height="629" alt="Image" src="https://github.com/user-attachments/assets/0e6e08b4-51ce-4791-b15c-21733d0b4c23" />

### 4.2. **Observe customer distribution by Country**

A unique characteristic of this dataset is the customer distribution by country, which is shown in the chart below.

<img width="2000" height="821" alt="Image" src="https://github.com/user-attachments/assets/f6b0ad24-91a5-4c44-a6be-5389146240ed" />

The data reveals that nearly 92% of customers are concentrated in the United Kingdom (UK), creating a significant imbalance in geographic distribution. This substantial disparity may distort insights if the analysis is conducted across the countries as a whole. Therefore, to ensure the analysis accurately reflects customer behavior, this study will separate the UK market from the non-UK market in the subsequent analysis.

### 4.3. **Calculate the metrics - Recency, Frequency, Monetary**

Set the assumed analysis date.

Input:

```python
assumed_analysis_date = pd.to_datetime('2011-12-31')
```

Calculate TotalSales = Quantity*UnitPrice.

Input:

```python
ecom_df['TotalSales'] = ecom_df['Quantity']*ecom_df['UnitPrice']
```

Create RFM table.

Input:

```python
rfm_df = ecom_df.groupby(['CustomerID','Country']).agg(
                                                        Recency = ('InvoiceDate', lambda x: (assumed_analysis_date - x.max()).days),
                                                        Frequency = ('InvoiceNo', 'nunique'),
                                                        Monetary = ('TotalSales', 'sum')
                                                        ).reset_index()
```

### 4.4. Do RFM Segmentation

Input:

```python
# Create a function for calculating rfm score
def rfm_score_calculator(df):
  df = df.copy() # Avoid Warning: SettingWithCopyWarning
  df['R_Score'] = pd.qcut(x=df['Recency'].rank(method='first'), q=5, labels=[5,4,3,2,1])
  df['F_Score'] = pd.qcut(x=df['Frequency'].rank(method='first'), q=5, labels=[1,2,3,4,5])
  df['M_Score'] = pd.qcut(x=df['Monetary'].rank(method='first'), q=5, labels=[1,2,3,4,5])
  df['RFM_Score'] = (df['R_Score'].astype(str) + df['F_Score'].astype(str) + df['M_Score'].astype(str)).astype(int)
  df['Segment'] = df['RFM_Score'].map(rfm_definition_df.set_index('RFM_Score')['Segment'])
  return df
```

Input:

```python
# Calculate rfm score for UK and non-UK market
uk_segmentation_df = rfm_score_calculator(uk_rfm_df)
other_country_segmentation_df = rfm_score_calculator(other_rfm_df)
# Convert to OLAP for visibility
uk_olap_df = uk_segmentation_df.groupby('Segment').agg(NumberofCustomers = ('CustomerID', 'count')).reset_index().sort_values(by='NumberofCustomers', ascending=False)
other_country_olap_df = other_country_segmentation_df.groupby('Segment').agg(NumberofCustomers = ('CustomerID', 'count')).reset_index().sort_values(by='NumberofCustomers', ascending=False)
```

### 4.5. Analyze for each Market

Performance for each market per metric

<img width="2000" height="600" alt="Image" src="https://github.com/user-attachments/assets/0eb85a9a-02a3-4608-a60c-fdf71ae57367" />

**💂‍♀️ UK Market**

- **Number of Customers:** 5,238 customers, accounting for nearly 92% of the total customer base.
- **Revenue:** USD 8,749,427.49, contributing around 85% of total revenue.
- **Number of Orders:** 17,901 orders, representing 91% of total orders.
    
    **Distribution of individual R, F, and M metrics for the UK market**
    
    <img width="2000" height="581" alt="Image" src="https://github.com/user-attachments/assets/78b8aa4e-aff0-434f-a118-24a65bbd5b50" />
    
    **Number of customers by segment for the UK market**
    
    <img width="2000" height="1300" alt="Image" src="https://github.com/user-attachments/assets/4f216a10-350f-4435-91dd-30220de7391a" />
    

**🌍 Non-UK Market**

- **Number of Customers:** 467 customers, accounting for nearly 8% of the total customer base.
- **Revenue:** USD 1,529,447.40, contributing around 15% of total revenue.
- **Number of Orders:** 1,875 orders, representing 9% of total orders.
    
    **Distribution of individual R, F, and M metrics for the non-UK market**
    
    <img width="2000" height="581" alt="Image" src="https://github.com/user-attachments/assets/f4543cb4-7957-45c8-baf2-b80690af6b38" />
    
    **Number of customers by segment for the non-UK market**
    
    <img width="2000" height="1300" alt="Image" src="https://github.com/user-attachments/assets/75d731ae-7198-4f0d-9975-925bf31574ae" />
    

**⚖️ Comparison Between the UK and Non-UK Markets**

The UK market is the core market for SuperStore, concentrating the majority of customers and generating 85% of the company’s revenue. While the Non-UK markets have a relatively small customer base, their revenue contribution is proportionally higher, indicating a higher average spend per customer. This highlights notable growth potential within the Non-UK customer segment.

In terms of the distribution of the R, F, and M metrics, consumer behavior between the UK and Non-UK markets shows no significant differences, despite the large customer base disparity. This suggests that a unified customer segmentation and marketing strategy can be effectively applied across both markets, rather than developing two entirely separate approaches.

Regarding customer distribution across segments, *Champions* represent the largest segment in both markets. This indicates that both the UK and Non-UK markets maintain a loyal and high-value customer group in recent periods. However, due to the difference in market size, the Champions group in the UK far outweighs that of the Non-UK (nearly 1,000 vs. fewer than 100), reflecting the scale gap and frequency of customer interactions.

Additionally, both markets report a significant presence of at-risk segments such as *Hibernating Customers*, *At Risk*, and *Lost Customers*, signaling the continued need for retention and reactivation efforts.

In summary, despite differences in scale, the RFM behavioral patterns across the two markets are largely consistent, reinforcing the view that customer consumption behaviors do not differ substantially by geography.

# **🚀 Final Conclusions and Recommendations**

## 🎯 Campaign Objective

To express gratitude to customers who have supported the company over the past year while strengthening engagement with potential customers and converting them into loyal buyers.

## 🧩 RFM-Based Segmentation Strategy

Based on this objective, RFM segments can be grouped into three levels of priority:

### **👑 Golden Bees - High Priority (Key Focus Segments) 👑**

| Segment                      | Rationale                                                                 | Recommended Strategy                                                                                          |
|------------------------------|---------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| Champions                    | 💡 Most recent, frequent, and high-value buyers <br> 👉🏼 Highly suitable for appreciation campaigns. | ✔️ Send personalized thank-you notes with exclusive perks (VIP sale, early access). <br> ✔️ Recommend new products to sustain purchase frequency. |
| Loyal Customers              | 💡 Consistent purchase history <br> 👉🏼 Retention is crucial to maintain loyalty. | ✔️ Reward points/discounts for next purchase. <br> ✔️ Invite to join loyalty programs. |
| Potential Loyalists          | 💡 Recent buyers with strong potential to become loyal customers. <br> 👉🏼 Nurture their loyalty | ✔️ Send welcome coupons and targeted promotions. <br> ✔️ Recommend products based on past behavior. |
| Promising                    | 💡 First-time recent buyers <br> 👉🏼 Need strong onboarding experience.        | ✔️ Send follow-up “thank you” emails + small incentive for next purchase. <br> ✔️ Provide useful content (tips, product guides). |



### **🌱 Seeds – Medium Priority (Monitor & Nurture) 🌱**

| Segment        | Rationale                                                                 | Recommended Strategy                                                                                          |
|----------------|---------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| Need Attention           | 💡 Valuable but showing lower engagement <br> 👉🏼 Require early reactivation.  | ✔️ Send survey to uncover reasons for inactivity + comeback offers. <br> ✔️ Highlight past benefits/value. |
| New Customers            | 💡 Brand-new with limited history <br> 👉🏼 Potential remains uncertain, needing more attention. | ✔️ Light onboarding with welcome email flows. <br> ✔️ Encourage profile completion and newsletter sign-ups. |


### **🧊 Drifting Icebergs – Low Priority (Deprioritized for Current Campaign) 🧊**

| Segment                  | Rationale                                                                 | Suggested Next Steps                                                                                       |
|---------------------------|---------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------|
| Hibernating <br> At Risk <br> Lost Customers | 💡Inactive for a long time or low spend <br> 👉🏼 Hard to re-engage short term. | ✔️ Include in separate reactivation campaigns. <br> ✔️ Conduct exit surveys to assess churn reasons. |
| About to Sleep <br> Cannot Lose Them         | 💡 Negative purchase patterns or long inactivity <br> 👉🏼 Misaligned with short-term “appreciation” theme. | ✔️ Keep monitoring. <br> ✔️ Exclude from current campaign investments. |


## 🔭 Strategic Focus

- **👑Golden Bees👑**: Primary target. High priority to launch appreciation and engagement initiatives to strengthen loyalty and maximize retention.
- **🌱Seeds🌱**: Observe and nurture selectively, approach only if the budget allows.
- **🧊Drifting Icebergs🧊**: Exclude from the short-term campaign. Plan separate reactivation initiatives.

## 🗺️ Geographic Strategy

- **UK Market**: Large scale, rich data, and clear segmentation → Ideal for implementing detailed RFM-based campaigns.
- **Non-UK Markets**: Smaller scale, less data, and less distinct segmentation  → Focus on general retention or expansion campaigns rather than detailed RFM targeting.

## 🏁 Conclusion

RFM analysis indicates that **SuperStore’s revenue growth is driven primarily by order frequency rather than average order value**. Therefore, strategies that encourage more frequent purchases will be more effective than those focused solely on driving high-value orders.

While the UK dominates in customer base, consumer behavior does not significantly differ from other European markets when viewed through the RFM model.

Alongside the high-value **Champions**, there remains a significant share of **Hibernating, At Risk, and Lost Customers**, requiring dedicated reactivation strategies.

Ultimately, **Champions, Loyal Customers, Potential Loyalists, and Promising segments in the UK market** should be prioritized in the current appreciation and engagement campaign.
