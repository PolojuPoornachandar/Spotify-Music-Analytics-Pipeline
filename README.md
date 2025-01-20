# **Spotify ETL Data Pipeline - AWS Cloud Implementation**

## **Project Overview**
Our client is passionate about the **music industry** and wants to analyze **music trends** using data from **Spotify**. The client aims to collect **weekly top global songs** from **Spotify Billboard** to understand:
- Trending songs
- Popular artists and composers
- Trending albums
- Music patterns over time

### **Business Problem**
The **Spotify Billboard** updates weekly, and our client wants to build a **large dataset over a year or two**. By analyzing this data, he can discover **patterns, trends, and insights** to create new music. 

To achieve this, we are developing an **ETL (Extract, Transform, Load) pipeline** to automate weekly data collection, processing, and storage.

---

## **Proposed AWS ETL Architecture**
We designed the following **AWS-based ETL pipeline** to automate data extraction, transformation, and storage.

### **ETL Process Steps**
1. **Extract:**
   - Extract **top global songs** from **Spotify API** using **AWS Lambda (Data Extraction)**.
   - Use **Amazon CloudWatch** to trigger the Lambda function **weekly**.
   - Store raw data in **Amazon S3 (Raw Data Storage)**.

2. **Transform:**
   - A trigger (**Object Put Event**) activates **AWS Lambda (Data Transformation)**.
   - Transform raw data into structured format (e.g., **JSON, Parquet**).
   - Store transformed data in **Amazon S3 (Transformed Data Storage)**.

3. **Load:**
   - **AWS Glue Crawler** scans transformed data and infers the schema.
   - **AWS Glue Data Catalog** stores metadata (column names, data types).
   - Use **Amazon Athena** to run **SQL queries** for data analysis.

### **Architecture Diagram**
![AWS ETL Architecture](sandbox:/mnt/data/hd_image.png)

---

## **AWS Resources Used**
### **1. AWS Lambda (Serverless Compute)**
- Used for **data extraction** and **data transformation**.
- Runs Python scripts for **API calls, data processing, and transformation**.

### **2. Amazon S3 (Simple Storage Service)**
- Stores **raw** and **transformed data**.
- Acts as a **data lake** to hold structured and unstructured data.

### **3. Amazon CloudWatch**
- Triggers AWS Lambda on a **weekly schedule** to fetch data.
- Monitors execution logs for debugging.

### **4. AWS Glue Crawler**
- Scans S3 **transformed data** and **infers schema** (columns, data types).
- Generates metadata for querying.

### **5. AWS Glue Data Catalog**
- Stores metadata about the dataset.
- Helps in structuring and organizing large datasets.

### **6. Amazon Athena (SQL-Based Analytics)**
- A **serverless SQL query service** to analyze data stored in S3.
- Enables **trend analysis** and **data insights** without database setup.

---

## **Spotify API Data Extraction**
Spotify API provides:
- **Artists** (e.g., Ed Sheeran, Drake)
- **Albums** (e.g., latest album releases)
- **Tracks** (e.g., top weekly tracks)

Our **Python app** connects to the **Spotify API** to **fetch data** and process it in **AWS Cloud**.

---

## **Future Improvements**
- **Data Visualization** using **Amazon QuickSight**.
- **Machine Learning Analysis** for trend prediction.
- **Automate data quality checks** using AWS Lambda.
- **Enhance metadata tracking** with AWS Glue.



---

## **Architecture Diagram**
Below is the architecture diagram representing the ETL workflow:

![hd_image](https://github.com/user-attachments/assets/51e03c64-5d6d-4713-98c2-4846afca0e5f)

---

## **Conclusion**
This architecture automates the entire ETL process using **AWS serverless services**. It provides a **scalable, cost-efficient, and easily maintainable** solution for ingesting, transforming, and analyzing Spotify API data.

