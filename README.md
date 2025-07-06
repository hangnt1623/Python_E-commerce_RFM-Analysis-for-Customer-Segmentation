# RFM Analysis for Customer Segmentation in E-commerce using Python
Use Python for Customer Segmentation

![KPMG Transaction Analysis](https://github.com/Dorothy-Ho-Vy/Sample_SQL_Python_template/blob/4dee6ff56077b90b1aea82e8517136f7185a77a3/Blue%20White%20Modern%20Payment%20Gateway%20Service%20Twitter%20Post.png.crdownload)

- Author: Nguyen Thuy Hang  
- Date: 2025-06-22
- Tools Used: Python  

---

## 📑 Table of Contents  
1. [📌 Background & Overview](#-background--overview)  
2. [📂 Dataset Description & Data Structure](#-dataset-description--data-structure)  
3. [🔎 Final Conclusion & Recommendations](#-final-conclusion--recommendations)

---

## 📌 Background & Overview  

### Objective:
### 📖 What is this project about? What Business Question will it solve?

**SuperStore**, a global retail company, needs to **segment its large and growing customer base** to run **effective, personalized marketing campaigns** during the **Christmas and New Year holidays**. Due to the **scale of customer data**, traditional manual segmentation (e.g., Excel) is no longer practical. The **Marketing department** requests an **automated solution using Python** to implement the **RFM (Recency, Frequency, Monetary)** model for **scalable, accurate customer segmentation**.


This project uses **Python** to analyze **SuperStore’s large-scale customer transaction data** to:

✔️ **Segment customers using the RFM model** to identify groups like loyal, inactive, and high-value customers

✔️ **Automate segmentation** to handle large datasets, replacing manual Excel methods

✔️ **Deliver insights** to help **Marketing & Sales** run **targeted, effective holiday campaigns**

 

### 👤 Who is this project for?  

✔️ **Marketing Teams** – to identify and target customer segments with **personalized holiday campaigns**

✔️ **Sales Teams** – to focus efforts on **high-value and frequent buyers** for **upselling and retention**

✔️ **Data Analytics Teams** – to **automate and scale customer segmentation** using **Python**

✔️ **Business Leaders** – to make **data-driven decisions** that boost **customer lifetime value** and **revenue**


### RFM Analysis Overview
#### 🔹 What is RFM?

RFM stands for:

| Metric    | Description                                  |
|-----------|----------------------------------------------|
| Recency   | How recently a customer made a purchase      |
| Frequency | How often the customer purchases             |
| Monetary  | How much money the customer has spent        |

🔗 *Customers with high scores across all three dimensions are considered **the most valuable***.

#### 🧠 Why Use RFM?

- Behavior-based segmentation (data-driven)
- Easy to implement and scale
- Improves marketing ROI by targeting the right segments
- Prioritizes customer retention and engagement efforts
  
---

## 📂 Dataset Description & Data Structure  

### 📌 Data Source  
- Source: The dataset is obtained from Kaggle
- Size: 541909 rows, 8 columns
- Format: .xlsx  

### 📊 Data Structure & Relationships  

#### 1️⃣ Tables Used:  
There is a table in the dataset called 'ecommerce_retail'. 

#### 2️⃣ Table Schema 

**Table: ecommerce_retail**
<details>
  <summary>📊 <strong>Table schema</strong></summary>

| Column Name | Data Type | Description |  
|-------------|----------|-------------|  
| InvoiceNo  |  object   | Invoice number |  
| StockCode  |  object     | Product (item) code |  
| Description    | object     | Product (item) name |  
| Quantity    | int64   | The quantities of each product (item) per transaction |  
| InvoiceDate    | datetime64[ns]  | Invoice Date and time |  
| UnitPrice    | float64   | Unit price |  
| CustomerID    | float64    | Customer number |  
| Country    | object   | Country name |  
</details>


## ⚒️ Main Process

1️⃣ **Data gathering**: Import datasets & libraries

2️⃣ **Exploratory Data Analysis (EDA):** 

<details>
  <summary>🧩 <strong>Step 1: Understand dataset</strong></summary>
****

(1) Use "df.shape"  to immediately know the number of transactions (rows) and types of information (columns) you're dealing with.
```python
ecommerce_retail.shape
```
*Result*: (541909, 8) -> you have over half a million transactions with 8 different attributes each

(2) Use "df.info()" to provides a quick summary of the structure and quality of ecommerce_retail
```python
ecommerce_retail.info()
```
*Result*:
- The DataFrame has 541,909 rows and 8 columns.
- The columns Description (missing 1,554 values) and CustomerID (missing 135,080 values) have missing data.
- The data types of the columns (e.g. InvoiceDate is datetime64[ns] which is fine, but CustomerID is float64 even though it is an ID).
- The total amount of memory the DataFrame taking up is 33.1+ MB

(3) Use "df.head(10)" to visually inspect the actual data for the first 10 transactions
```python
ecommerce_retail.head(10)
```

(4) Use "df.describe()" to get a quick statistical summary of numerical columns like Quantity and UnitPrice
```python
ecommerce_retail.describe()
```
</details>


<details>
  <summary>🧩 <strong>Step 2: Inspect & valid dataset</strong></summary>
****

- First of all, use ProfileReport to  generate automated Exploratory Data Analysis (EDA) reports for ecommerce_retail, this provide a quick overview of data quality, missing values, and variable distribution, helping you understand your ecommerce_retail data immediately
```python
profile = ProfileReport(ecommerce_retail, title="EDA Report", explorative=True)
profile.to_notebook_iframe()
```

***(1) Data type*** 

Checking data types identifies data's nature and initial quality issues, while changing them ensures correct operations, optimized performance, and compatibility for analysis.

- Change datatype of "InvoiceID" & "StockCode" & "CustomerID" to STRING because InvoiceID usually includes numbers & letters
- "Description", "Country" -> description / country name -> change datatype of these 2 columns to STRING

*Before & After*

<img width="163" alt="{0CFCB0C3-A158-4523-941B-02580D70A53E}" src="https://github.com/user-attachments/assets/541113a9-b9ca-4d03-ae8b-e6bdc8df1d15" />
<img width="160" alt="{7414B09B-650A-4AA0-9C7B-663D335BAF30}" src="https://github.com/user-attachments/assets/86910594-b746-4fe1-becf-a880a1cab78d" />

***(2) Missing Value***

Checking missing values helps identify data quality issues and incompleteness. Handling them prevents analysis errors, ensures accurate results, and improves model performance by providing complete data.

"Description", "CustomerID" -> Next step:
- Remove lines without Description information because Unit Price = 0 and no Customer ID information
- Remove lines without CustomerID information because it will not be possible to identify the customer segment

*Before & After*

<img width="129" alt="{E86A6975-448B-4685-8C86-443125EA59FF}" src="https://github.com/user-attachments/assets/5e82199c-9c3f-43a9-bd75-0f0c02c3d11d" />
<img width="99" alt="{7D4F5A14-D448-4E0D-8B8C-468E36A7AD4E}" src="https://github.com/user-attachments/assets/f2fd9ae8-4a15-4af8-8f54-35043917ef6d" />


***(3) Unique Value***

- Understand Categorical Variables: See distinct categories and their counts for analysis
- Verify Identifier Columns: Confirm uniqueness of IDs and spot duplicates
- Aid Data Cleaning & Preprocessing: Identify inconsistencies or values needing standardization

<img width="128" alt="{89F9632E-0C0E-4A91-9EC7-59A9DC7A9C60}" src="https://github.com/user-attachments/assets/81b297c3-ece0-4c20-87f4-149a122e44b6" />


***(4) Duplicate Value***

Checking duplicates is to find redundant or erroneous entries, while removing them is to ensure accurate analysis, prevent bias, and maintain data integrity.

Duplicates: 5225 rows -> Next step: Delete rows

***(5) Outliers***

Check outliers is to find unusual or extreme data points that can skew results, while dealing with them is to prevent data distortion, ensure accurate analysis, and improve model performance.

Result: 25616 rows × 12 columns 
-> Next step: no action because some customers buy small quantities, some customers buy large quantities

***(6) Valid Value***

Checking valid values is to find data outside expected logical or business ranges, while dealing with them is to prevent errors, ensure data integrity, and derive reliable insights.

- Quantity < 0: Return transaction, not actual sale -> Remove these rows
- Unit Price < 0: Data error or invalid value -> Remove these rows

***(7) Distribution***

Checking distribution is to understand how data values are spread and concentrated, detect outliers, guide data transformations, and inform model selection for better analysis.

In this case, use logarithm is to make highly skewed data distributions more symmetrical and easier to visualize, compressing wide value ranges and highlighting patterns.

<img width="433" alt="{DB8D25CB-1A07-4CCC-AA7B-1BC8D6FFE70C}" src="https://github.com/user-attachments/assets/19085132-dd69-4ce8-8b32-62c0d24e1694" />

<img width="487" alt="{A115DE8D-1F29-483A-B540-CA85ED359F48}" src="https://github.com/user-attachments/assets/ae737372-b36f-45d0-9f44-fd1c74dcd27a" />

-> Both Quantity and TotalPrice are strongly skewed towards small values. The logarithmic plot shows that Quantity has specific common purchase levels, while TotalPrice after the logarithm transformation becomes more concentrated and symmetrical, indicating that the majority of transactions have total values ​​within a certain range.
</details>



3️⃣ **Data processing:** 

<details>
  <summary>🧩 <strong>Step 1: Prepare the data</strong></summary>

 - Calculate TotalPrice for each transaction by multiplying quantity × unit price.
- Set a reference date (Dec 31, 2011) to measure recency from.
</details>


<details>
  <summary>🧩 <strong>Step 2: Calculate R, F, M values per customer</strong></summary>
#### 
- Recency: Days since the customer’s last purchase (difference between reference date and last purchase date).
- Frequency: Count of unique purchase invoices (how often the customer bought).
- Monetary: Total money spent by the customer.
</details>

<details>
  <summary>🧩 <strong>Step 3: Convert R, F, M values to scores (1 to 5)</strong></summary>
- For Recency, lower days mean higher score (5 = most recent buyers).
- For Frequency and Monetary, higher values get higher scores (5 = most frequent/spending customers).

-> This is done by splitting customers into 5 groups (quintiles) based on each metric.
</details>

<details>
  <summary>🧩 <strong>Step 4: Combine the scores into a 3-digit RFM Score</strong></summary>

 -> Concatenate the R, F, and M scores into a single string, e.g., "545".
</details>

<details>
  <summary>🧩 <strong>Step 5: Segment customers by matching their RFM Score to predefined groups</strong></summary>

 - Use the mapping table of RFM Score patterns (like "555", "544", etc.) to assign customers into segments such as Champions, Loyal, At Risk, Lost, etc.
- This allows tailoring marketing strategies to each customer group.

<details>
  <summary>🧩 <strong>Click here to see RFM Segments</strong></summary>

| Segment               | RFM Score Patterns |
|-----------------------|-------------------|
| **Champions**         | 555, 554, 544, 545, 454, 455, 445 |
| **Loyal**             | 543, 444, 435, 355, 354, 345, 344, 335 |
| **Potential Loyalist**| 553, 551, 552, 541, 542, 533, 532, 531, 452, 451, 442, 441, 431, 453, 433, 432, 423, 353, 352, 351, 342, 341, 333, 323 |
| **New Customers**     | 512, 511, 422, 421, 412, 411, 311 |
| **Promising**         | 525, 524, 523, 522, 521, 515, 514, 513, 425, 424, 413, 414, 415, 315, 314, 313 |
| **Need Attention**    | 535, 534, 443, 434, 343, 334, 325, 324 |
| **About To Sleep**    | 331, 321, 312, 221, 213, 231, 241, 251 |
| **At Risk**           | 255, 254, 245, 244, 253, 252, 243, 242, 235, 234, 225, 224, 153, 152, 145, 143, 142, 135, 134, 133, 125, 124 |
| **Cannot Lose Them**  | 155, 154, 144, 214, 215, 115, 114, 113 |
| **Hibernating**       | 332, 322, 233, 232, 223, 222, 132, 123, 122, 212, 211 |
| **Lost**              | 111, 112, 121, 131, 141, 151 |

> Use RFM segmentation to tailor marketing strategies, target reactivation campaigns, and maximize lifetime value.
</details>
</details>

4️⃣ **Data visualization & Analysis** 

<details>
  <summary> 🧩 <strong>(1) Relationship between indicators: R, F, M</strong></summary>
 
While the main analysis uses **RFM model** to segment customers for strategic actions,  this section dives deeper into the **interplay between Recency, Frequency, and Monetary**.  It helps uncover **specific customer behaviors** inside and across segments,  revealing *hidden value, churn risk, and growth potential*.

![image](https://github.com/user-attachments/assets/bd683818-74db-4d78-9356-cbbbf60d4e15)

![image](https://github.com/user-attachments/assets/9e7ffde6-5730-463d-a7e4-b2fdcdb1dc49)

*Observations:*

- From Correlation Matrix:
  + Frequency (F) and Monetary (M) have a strong positive correlation (0.55). This is the most crucial finding: higher frequency directly leads to higher spending. Prioritize strategies to increase purchase frequency.
  + Recency (R) and Frequency (F) show a moderate negative correlation (-0.26). Recent buyers tend to be more frequent. This aligns with RFM logic.
- From Heatmaps of R, F, M Scores:
 + F_score vs M_score (Right Heatmap) is key. This heatmap visually confirms the strong F-M relationship: high concentration of customers with both high F and high M scores (e.g., F=5, M=5). These are your "Champions" – prioritize retention and growth strategies for them.
 + R_score vs F_score (Left Heatmap):
   ++ Significant clusters of high R, low F customers (e.g., R=5, F=1) indicate "New Customers" or "One-Time Buyers" needing nurturing to become frequent.
   ++ Clusters of low R, high F customers (e.g., R=1, F=5) represent "Lapsed Loyalists" who need re-engagement.
   
*Recommendations*
- Reward Champions (High F/M): Offer exclusive loyalty perks to your most frequent and high-spending customers.
- Convert New Customers (High R/Low F): Launch immediate follow-up campaigns to drive their second purchase.
- Win Back Lapsed Loyalists (Low R/High F): Send targeted re-engagement offers to reignite their activity.

</details>

<details>
  <summary>🧩  <strong>(2) Distribution of Recency, Frequency, Monetary</strong></summary>

To support segmentation logic, this section visualizes the **distribution of Recency, Frequency, and Monetary** across all customers.  
It helps assess the **shape of the customer base** - e.g., how active, how loyal, how valuable they are - and informs whether the segmentation is well-balanced or skewed.
 
***Distribution (remove outliers)***

![image](https://github.com/user-attachments/assets/fd742b3c-62d3-408d-8c83-61022952a79e)

-> *Observation*
- Overall
 + Heavily Skewed Data: All three charts (Recency, Frequency, Monetary) are strongly skewed right, showing most customers are in the lower ranges of buying frequency and total spend.
 + "Long-Tail" Customer Presence: Despite the concentration at lower values, each distribution has a long tail, indicating a smaller but significant group of highly engaged and valuable customers.
 + Conversion Opportunity: The combined view suggests a customer base where initial purchases are common, but transforming these into consistent, high-value engagement is a major challenge and primary growth area.
- Detail
  + "New & At-Risk": Customers who recently bought (high Recency) but show low Frequency/Monetary. Focus: Immediate engagement to prevent churn.
  + "Lapsed Loyalists": Customers with low Recency, but historically high Frequency/Monetary. Focus: Targeted win-back campaigns to reactivate past value.
  + "High-Value Champions": Customers consistently high in both Frequency and Monetary. Focus: Retention, rewards, and fostering advocacy.

***Distributions (for outliers -> high spending)***

|  | Recency | Frequency | Monetary | F_score | M_score | RFM_Score |
| --- | --- | --- | --- | --- | --- | --- |
| count | 104.000.000 | 104.000.000 | 104.000.000 | 104.000.000 | 104.0 | 104.000.000 |
| mean | 39.528.846 | 30.596.154 | 35.097.018.942 | 3.807.692 | 5.0 | 492.115.385 |
| std | 44.219.654 | 33.106.336 | 46.617.847.042 | 608.626 | 0.0 | 98.006.073 |
| min | 21.000.000 | 1.000.000 | 10.196.570.000 | 1.000.000 | 5.0 | 115.000.000 |
| 25% | 22.750.000 | 12.000.000 | 12.334.922.500 | 4.000.000 | 5.0 | 445.000.000 |
| 50% | 25.500.000 | 22.000.000 | 17.189.940.000 | 4.000.000 | 5.0 | 545.000.000 |
| 75% | 36.250.000 | 33.250.000 | 35.295.950.000 | 4.000.000 | 5.0 | 545.000.000 |
| max | 346.000.000 | 209.000.000 | 280.206.020.000 | 4.000.000 | 5.0 | 545.000.000 |

![image](https://github.com/user-attachments/assets/c238e6d7-22ee-4089-ba8c-73807abe7945)

-> *Observation*
- This chart reveals a heavily right-skewed distribution even among top spenders (>\$10,000). The majority of these high-value customers cluster just above the \$10,000 mark.
- There's an extreme rarity of "ultra-high" spenders (e.g., above \$50,000-\$75,000). This identifies a very small, elite segment of "Monetary Elites" or "Whales" whose individual contribution to revenue is disproportionately large.

***Compare outliers vs total RFM average***

|  | All_Customers | Outliers_Only |
| --- | --- | --- |
| Recency | 113.1 | 39.5 |
| Frequency | 4.3 | 30.6 |
| Monetary | 2048.7 | 35097.0 |


*Observations*
- Elite (Champion, Loyalist, ..)  Performance Gap: Our top-tier outliers purchase ~8x more frequently and spend ~17x more per customer than the average, while being ~3x more recently active. This isn't just better; it reveals an entirely different dimension of customer engagement.
- CLTV Chasm: This extreme disparity underscores a massive Customer Lifetime Value (CLTV) chasm between the bulk of our customers and this elite group. The real challenge is unlocking similar value from the broader base, or at least understanding what makes this small segment so incredibly lucrative.
- Strategic Focus Imperative: The data screams: these outliers aren't just good, they're a business-defining force. Ignoring their unique behavior and contribution means missing critical insights into maximizing enterprise value.

***Recommendations***
- Tailored Elite Programs: Develop exclusive, high-touch programs (e.g., dedicated account managers, early access to products, bespoke offers) for the "Monetary Elites" and "High-Value Champions."
- Segmented Re-engagement Funnels: Implement specific re-engagement strategies for "New & At-Risk" (e.g., welcome series with immediate value propositions) and "Lapsed Loyalists" (e.g., win-back campaigns highlighting new offerings or personalized incentives).
- Upskill Broad Base: Analyze the purchasing patterns and product preferences of "High-Value Champions" and "Monetary Elites." Use these insights to create targeted upsell/cross-sell campaigns and educational content for the broader customer base, aiming to migrate more customers towards higher frequency and monetary value.
</details>


<details>
  <summary>🧩 <strong>(3) Customer segment structure</strong></summary>
****
→ Analyze the size of each customer group to understand dominant segments and prioritize strategies.

***Total numbers of customers & revenue by segment***

| Segment | Num_Customers | Total_Revenue | %_Customers | %_Revenue |
| --- | --- | --- | --- | --- |
| Champions | 534 | 4.877.732.290 | 12.31 | 54.88 |
| Loyal | 236 | 884.850.540 | 5.44 | 9.96 |
| Need Attention | 422 | 732.141.920 | 9.73 | 8.24 |
| Promising | 485 | 697.531.710 | 11.18 | 7.85 |
| At Risk | 240 | 574.017.240 | 5.53 | 6.46 |
| Cannot Lose Them | 228 | 354.187.691 | 5.26 | 3.99 |
| Potential Loyalist | 245 | 171.490.251 | 5.65 | 1.93 |
| Hibernating customers | 491 | 169.985.642 | 11.32 | 1.91 |
| About To Sleep | 328 | 161.623.840 | 7.56 | 1.82 |
| Lost customers | 620 | 143.382.810 | 14.29 | 1.61 |
| New Customers | 509 | 120.264.960 | 11.73 | 1.35 |


![image](https://github.com/user-attachments/assets/02d7e8dd-6eb9-4545-9543-10cd51272d3a)

![image](https://github.com/user-attachments/assets/5c485388-cb36-4d40-8d15-bce0f4bbb422)

*Observations*

- Champions: Your Revenue Fortress (and Fragility Point)
  + Champions are absolutely mind-blowing, representing a staggering 54.88% of your total revenue with only 12.31% of your customer base. This isn't just impressive; it means for every dollar you make, over half comes from just over one-tenth of your customers! This segment isn't just your best customers; they are your business.
  + -> This extreme concentration is a superpower and a critical vulnerability. Losing even a few Champions means massive revenue hits. Prioritize hyper-personalized retention; they're not just customers, they're your core asset.
- Lost Customers: A Bigger Opportunity Than New Acquisition
  + Lost Customers are the largest segment by count (14.29%), still out-earning entire New Customers segment (1.61% vs. 1.35% of revenue).
  + -> Forget chasing all new leads. Your biggest immediate win might be reactivating this massive pool of already-converted customers. A smart win-back strategy here could yield significantly higher ROI than typical acquisition efforts.
- Hibernating Customers: The Unwoken Giants
  + Hibernating Customers are a huge segment (11.32%) and contribute more revenue than "About To Sleep" customers (1.91% vs. 1.82%).
  + -> Don't just focus on preventing future churn. These "sleeping giants" represent a vast, untapped resource. Targeted re-engagement to awaken even a small portion of them could drive substantial, efficient revenue growth.

*Recommendations*
- Launch a "Champion Circle" Exclusive Program:
 + Action: Create an invitation-only loyalty tier for your Champions, offering dedicated support, early product access, and direct input into your offerings.
 -> This deepens loyalty, mitigates revenue concentration risk, and secures your most vital customers.
- Execute a "Welcome Back, Valued Customer" Win-Back:
  + Action: Deploy personalized, multi-channel campaigns to Lost Customers with compelling offers based on their purchase history.
  -> Reactivating past customers is often cheaper and yields higher ROI than new acquisition, tapping into a proven revenue pool.
- Implement a "Re-Spark Interest" Nurturing Track:
  + Action: Set up automated, value-driven content series (e.g., tips, new arrivals) for Hibernating Customers, avoiding immediate sales pushes.
  -> This scalable approach gently re-engages a large, dormant segment, converting latent potential into active revenue.
  
</details>


5️⃣ **Insights & Recommendations**

**(1) Conclusion on the status of SuperStore & Suggestions for Marketing team**

***SuperStore Status***

- **Heavy Reliance on Champions**: Over 50% revenue comes from ~12% loyal customers, posing a high risk if this group churns.  
- **Low Repeat Purchases**: Most customers are one-time or low-frequency buyers, indicating a need to boost engagement and average revenue per user (ARPU).  
- **At-Risk High-Value Customers**: A segment of high-spending customers is showing signs of disengagement, threatening significant revenue loss.  
- **Untapped Potential**: New and promising customers exist but haven't been effectively converted into loyal, high-value buyers.  
- **Dormant/Lost Segments**: A large portion of customers are inactive or lost, currently offering minimal value.  


***Suggestions for Marketing team***

- **Retention Focus:** Implement VIP programs for Champions/Loyal and personalized re-engagement for At-Risk/Cannot Lose Them customers.  
- **Nurturing Strategy:** Develop targeted onboarding and repeat-purchase campaigns for New and Promising customers.  
- **Reactivation Campaigns:** Launch flash sales and emotional messaging to re-engage Hibernating/About to Sleep customers.  
- **Resource Optimization:** Reduce broad marketing spend on Lost Customers; use selective A/B testing for re-engagement or delist.  


**(2) Suggestions for Marketing and Sales team with the retail model of Superstore company, which of the 3 indexes R, F, M should be most concerned about?**

***Marketing Team***

- **Prioritize:** Recency (R)  
- **Reasons**  
   + Customer "Hotness": R indicates recent activity; recent buyers are more receptive to marketing  
   + Conversion & Efficiency: Higher conversion rates for retargeting, optimizing ad spend (avoids "cold" customers)  
   + Lifecycle Segmentation: Essential for tailoring messages across customer journey stages (e.g., active, warm, cold, lost).
     
***Sales Team***

- **Prioritize:** Frequency (F)  
- **Reasons**  
  + **True Engagement:** F reflects actual loyalty and trust (repeat purchases)  
  + **Lower Selling Costs:** Frequent buyers are easier to upsell/cross-sell; they require less effort to close deals  
  + **Sustainable Revenue:** F identifies reliable, long-term revenue sources  
  + **Upsell/Cross-sell Opportunities:** Consistent purchase habits create clear paths for higher-value sales  
  

## 🔎 Final Conclusion & Recommendations  

**1. Based on the insights and findings, we would recommend the Marketing team to consider the following:** 

📌 Key Takeaways:  

✔️ Retention Strategy - Champions & Loyal; At Risk & Cannot Lose Them

✔️ Nurturing Strategy - Promising, Potential Loyalist, New Customers 

✔️ Reactivation Strategy - Hibernating, About to Sleep, Need Attention

✔️ Resource Optimization Strategy - Lost Customers

**2. Each team should prioritize each RFM metric**

- Marketing team should prioritize Recency
  
- Sales team should prioritize Frequency
