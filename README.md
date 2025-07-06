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
This project uses Python to analyze SuperStore’s large-scale customer transaction data to:

✔️ Segment customers using the RFM model to identify groups like loyal, inactive, and high-value customers

✔️ Automate segmentation to handle large datasets, replacing manual Excel methods

✔️ Deliver insights to help Marketing & Sales run targeted, effective holiday campaigns
 


### 👤 Who is this project for?  

✔️ Marketing Teams – to identify and target customer segments with personalized holiday campaigns

✔️ Sales Teams – to focus efforts on high-value and frequent buyers for upselling and retention

✔️ Data Analytics Teams – to automate and scale customer segmentation using Python

✔️ Business Leaders – to make data-driven decisions that boost customer lifetime value and revenue





---

## 📂 Dataset Description & Data Structure  

### 📌 Data Source  
- Source: The dataset is obtained from Kaggle
- Size: 541909 rows, 8 columns
- Format: .xlsx  

### 📊 Data Structure & Relationships  

#### 1️⃣ Tables Used:  
There is a table in the dataset called 'ecommerce_retail'. 

#### 2️⃣ Table Schema & Data Snapshot  

**Table: ecommerce_retail**

*Table schema*

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

*Data snapshot*

<img width="758" alt="{4BD60805-AC96-4709-ACB1-976B55F6B92D}" src="https://github.com/user-attachments/assets/8d796929-f5b2-4e3f-9ead-396bb2007bde" />





## ⚒️ Main Process

1️⃣ **Define problem, metric & Data gathering**

**Define problem, metric**

SuperStore, a global retail company, needs to segment its large and growing customer base to run effective, personalized marketing campaigns during the Christmas and New Year holidays. Due to the scale of customer data, traditional manual segmentation (Excel) is no longer practical. The Marketing department requests an automated solution using Python to implement the RFM (Recency, Frequency, Monetary) model for scalable, accurate customer segmentation.

**Data gathering**: Import datasets & libraries

2️⃣ **Exploratory Data Analysis (EDA):** 

**Step 1: Understand dataset**

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



**Step 2: Inspect & valid dataset**

- First of all, use ProfileReport to  generate automated Exploratory Data Analysis (EDA) reports for ecommerce_retail, this provide a quick overview of data quality, missing values, and variable distribution, helping you understand your ecommerce_retail data immediately
```python
profile = ProfileReport(ecommerce_retail, title="EDA Report", explorative=True)
profile.to_notebook_iframe()
```

***(1) Data type*** 

Checking data types identifies data's nature and initial quality issues, while changing them ensures correct operations, optimized performance, and compatibility for analysis.

- Change datatype of "InvoiceID" & "StockCode" & "CustomerID" to STRING because InvoiceID usually includes numbers & letters
- "Description", "Country" -> description / country name -> change datatype of these 2 columns to STRING

*Before

<img width="163" alt="{0CFCB0C3-A158-4523-941B-02580D70A53E}" src="https://github.com/user-attachments/assets/541113a9-b9ca-4d03-ae8b-e6bdc8df1d15" />

*After 

<img width="160" alt="{7414B09B-650A-4AA0-9C7B-663D335BAF30}" src="https://github.com/user-attachments/assets/86910594-b746-4fe1-becf-a880a1cab78d" />

***(2) Missing Value***

Checking missing values helps identify data quality issues and incompleteness. Handling them prevents analysis errors, ensures accurate results, and improves model performance by providing complete data.

"Description", "CustomerID" -> Next step:
- Remove lines without Description information because Unit Price = 0 and no Customer ID information
- Remove lines without CustomerID information because it will not be possible to identify the customer segment

*Before

<img width="129" alt="{E86A6975-448B-4685-8C86-443125EA59FF}" src="https://github.com/user-attachments/assets/5e82199c-9c3f-43a9-bd75-0f0c02c3d11d" />

*After

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



3️⃣ **Data processing:** 

Calculate RFM (Recency, Frequency, Monetary) scores and combine them into an aggregate RFM score to segment customers.


4️⃣ **Data visualization & Analysis** 

**(1) Distribution of Recency, Frequency, Monetary**

→ Understand the overview of customer behavior in each dimension: recent, frequent, monetary

***Distribution (remove outliers)***

![image](https://github.com/user-attachments/assets/fd742b3c-62d3-408d-8c83-61022952a79e)


***Distributions (for outliers -> high spending)***

![image](https://github.com/user-attachments/assets/c238e6d7-22ee-4089-ba8c-73807abe7945)

***Compare outliers vs total RFM average***

<img width="244" alt="{E8DED7DD-310C-4D61-974C-C4EED177D915}" src="https://github.com/user-attachments/assets/9d0d99d4-661a-452a-80ca-46a33e802b04" />

*Observations*

- Recency: Customer base is largely active (many recent buyers), though a small segment is at risk (inactive for 150+ days).
- Frequency: The majority are low-frequency buyers (1-3 purchases), indicating low repeat purchase rates.
- Monetary: Most customers are low-spenders, but a small, high-value segment (outliers) exists.
- High-Value Customers: This small group of "Champions" exhibits very active, frequent, and recent purchasing behavior, driving significant value.

-> SuperStore has an active customer base but struggles with repeat purchases. A critical, high-value customer segment requires dedicated engagement.

*Recommendations*

- Implement retargeting for inactive/low-frequency customers
- Develop a "VIP" program for high-spenders
- Utilize customer segmentation for personalized marketing strategies



**(2) Customer segment structure**

→ Analyze the size of each customer group to understand dominant segments and prioritize strategies.

***Total numbers of customers & revenue by segment***

<img width="440" alt="{2179BD22-7200-4FB0-A2CE-0EC09FAB2010}" src="https://github.com/user-attachments/assets/6ea52092-120a-4575-a5fb-f1133e4e795e" />

![image](https://github.com/user-attachments/assets/02d7e8dd-6eb9-4545-9543-10cd51272d3a)

![image](https://github.com/user-attachments/assets/5c485388-cb36-4d40-8d15-bce0f4bbb422)

*Observations*

- High Value Concentrated: A small group of Champions (12% customers) drives over half (55%) of the total revenue. Loyal customers also contribute significantly with potential to grow.
- Large Potential Base: New and Promising customers form a large group with low current revenue, representing future growth.
- Significant Churn Risk: At-Risk and Cannot Lose Them segments show declining interaction but still hold substantial value, indicating potential revenue loss if unaddressed.
- Low Value, High Volume: Lost Customers are the largest group by count but contribute very little revenue.

*Recommendations*

- Prioritize Core: Implement VIP programs for Champions and growth incentives for Loyal customers to ensure retention and progression.
- Nurture & Convert: Develop robust onboarding and personalized engagement for New and Promising customers to foster loyalty.
- Re-engage Proactively: Launch targeted, personalized reactivation campaigns for At-Risk and Cannot Lose Them segments to prevent churn.
- Optimize Spend: Reduce broad marketing efforts on Lost Customers, focusing instead on highly selective re-engagement or reallocating resources to higher-potential segments.


**(3) Group Value Analysis**

→ Understand each customer segment according to the value it brings

<img width="544" alt="{39F271BC-DFD2-4B3E-94F6-AF7DCBC631A0}" src="https://github.com/user-attachments/assets/8ec85f68-f54e-4ea6-905f-d3f53bbb26f5" />

*Observations*

- Core Value Drivers: Champions (12% of customers) generate over half (55%) of all revenue with high average spend and frequency. Loyal customers also contribute significantly, showing strong engagement.
- High-Risk, High-Value: Segments like At Risk and Cannot Lose Them still hold substantial revenue, but are showing clear signs of declining engagement (e.g., high Recency for "Cannot Lose Them"), posing a significant threat of loss.
- Growth Potential: New, Promising, and Potential Loyalist customers are a large group with good Recency but low current frequency and spend, representing future growth opportunities.
- Dormant Segments: Hibernating, About To Sleep, and Need Attention customers are increasingly inactive, with some (Need Attention) having decent past spend, indicating a need for urgent reactivation.
- Lost Group: Lost Customers form a large segment with minimal current value or engagement.

*Recommendations*

- Prioritize Core: Implement VIP programs & personalized care for Champions & Loyal.
- Proactive Re-engagement: Use targeted campaigns for At-Risk and Cannot Lose Them.
- Nurture Growth: Establish onboarding & personalized engagement for New/Potential customers.
- Reactivate Dormant: Employ flash sales & targeted outreach for Hibernating/About To Sleep.
- Optimize Spend: Reduce broad marketing for Lost Customers, focus on selective re-marketing.

**(4) Relationship between indicators: R, F, M** 

→ Understand customer purchasing behavior and identify potential or unusual customer groups for tailored strategies

![image](https://github.com/user-attachments/assets/bd683818-74db-4d78-9356-cbbbf60d4e15)

![image](https://github.com/user-attachments/assets/9e7ffde6-5730-463d-a7e4-b2fdcdb1dc49)

*Observations:*

- Emerging High-Value Customers: A significant group (R=5, F=3-4, M=4-5) are recent, moderately frequent, and high-spending – a promising core for future Champions.
- High-Value Churn Risk: Customers with low Recency (R=1) but high past Monetary (M=4-5) are valuable but at high risk of churn.
Frequent Low-Value Buyers: A segment with high Frequency (F=4) but low Monetary (M=1-2) indicates loyal but low-spending customers.
- Newly Re-engaged, Low Value: Customers with high Recency (R=5) but low Frequency/Monetary (F=1, M=1) are recently reactivated but not yet valuable.

*Recommendations*

- Nurture Emerging VIPs: Offer early VIP benefits, exclusive experiences, and tailored loyalty programs to develop the R5F3-4M4-5 group.
- Win Back High-Value Churners: Deploy personalized re-engagement emails and exclusive "welcome back" vouchers for R1M4-5 customers.
- Increase ARPU for Loyal Low-Spenders: Promote product bundles, tiered discounts, and value-added services (e.g., free shipping thresholds) for F4M1-2 customers.
- Convert New Re-engagers: Offer incentives for a second purchase and provide a superior onboarding experience for R5F1M1 customers.


5️⃣ **Insights & Recommendations**

**(1) Conclusion on the status of SuperStore & Suggestions for Marketing team**

***SuperStore Status***

- Heavy Reliance on Champions: Over 50% revenue comes from ~12% loyal customers, posing a high risk if this group churns.
- Low Repeat Purchases: Most customers are one-time or low-frequency buyers, indicating a need to boost engagement and average revenue per user (ARPU).
- At-Risk High-Value Customers: A segment of high-spending customers is showing signs of disengagement, threatening significant revenue loss.
- Untapped Potential: New and promising customers exist but haven't been effectively converted into loyal, high-value buyers.
- Dormant/Lost Segments: A large portion of customers are inactive or lost, currently offering minimal value.

***Suggestions for Marketing team***

- Retention Focus: Implement VIP programs for Champions/Loyal and personalized re-engagement for At-Risk/Cannot Lose Them customers.
- Nurturing Strategy: Develop targeted onboarding and repeat-purchase campaigns for New and Promising customers.
- Reactivation Campaigns: Launch flash sales and emotional messaging to re-engage Hibernating/About to Sleep customers.
- Resource Optimization: Reduce broad marketing spend on Lost Customers; use selective A/B testing for re-engagement or delist.


**(2) Suggestions for Marketing and Sales team with the retail model of Superstore company, which of the 3 indexes R, F, M should be most concerned about?**

***Marketing Team***

- Prioritize: Recency (R)
- Reasons
   + Customer "Hotness": R indicates recent activity; recent buyers are more receptive to marketing
   + Conversion & Efficiency: Higher conversion rates for retargeting, optimizing ad spend (avoids "cold" customers)
   + Lifecycle Segmentation: Essential for tailoring messages across customer journey stages (e.g., active, warm, cold, lost).
     
***Sales Team***

- Prioritize: Frequency (F)
- Reasons
  + True Engagement: F reflects actual loyalty and trust (repeat purchases)
  + Lower Selling Costs: Frequent buyers are easier to upsell/cross-sell; they require less effort to close deals
  + Sustainable Revenue: F identifies reliable, long-term revenue sources
  + Upsell/Cross-sell Opportunities: Consistent purchase habits create clear paths for higher-value sales
  

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
