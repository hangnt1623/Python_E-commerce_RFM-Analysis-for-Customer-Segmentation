# RFM-Analysis
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

✔️ Segment customers using the RFM model to identify groups like loyal, inactive, and high-value customers.

✔️ Automate segmentation to handle large datasets, replacing manual Excel methods.

✔️ Deliver insights to help Marketing & Sales run targeted, effective holiday campaigns.
 


### 👤 Who is this project for?  

✔️ Marketing Teams – to identify and target customer segments with personalized holiday campaigns.

✔️ Sales Teams – to focus efforts on high-value and frequent buyers for upselling and retention.

✔️ Data Analytics Teams – to automate and scale customer segmentation using Python.

✔️ Business Leaders – to make data-driven decisions that boost customer lifetime value and revenue.





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

- Understand dataset

- Clean dataset

- Inspect & valid dataset

3️⃣ **Data processing:** Segment customers from RFM score

4️⃣ **Data visualization & Analysis** 

- Distribution of R, F, M

- Customer segment structure

- Group Value Analysis

- Relationship between indicators: R, F, M 

5️⃣ **Insights & Recommendations**

- Conclusion on the current status of SuperStore & Suggestions for Marketing team

- Suggestions for Marketing and Sales team with the retail model of Superstore company, which of the 3 indexes R, F, M should be most concerned about?


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
