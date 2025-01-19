# AWS Cloud ETL Architecture for Spotify API Data Pipeline

## **Overview**
This architecture extracts, transforms, and loads (ETL) data from the **Spotify API** into AWS, enabling SQL-based analytics using **Amazon Athena**. It automates data ingestion and transformation using **AWS Lambda, S3, Glue, and CloudWatch**.

---

## **Step-by-Step ETL Process**

### **1. Extraction Phase**
- **Spotify API**: The pipeline fetches raw music data (e.g., track details, artist info) from the **Spotify API**.
- **AWS Lambda (Data Extraction)**: 
  - A Python-based AWS Lambda function extracts data from the API.
  - It runs on a **daily schedule** triggered by **Amazon CloudWatch**.
- **Amazon S3 (Raw Data Storage)**:
  - The extracted raw data is stored in an **Amazon S3 bucket** for further processing.

---

### **2. Transformation Phase**
- **AWS Lambda (Data Transformation)**:
  - Another Lambda function processes the raw data, **cleaning and transforming** it into a structured format (e.g., JSON, Parquet).
- **Amazon S3 (Transformed Data Storage)**:
  - The transformed data is then stored in a **separate S3 bucket**.
- **Trigger (Object Put Event)**:
  - A trigger is set up to **automatically process new files** uploaded to the raw S3 bucket.

---

### **3. Load Phase**
- **AWS Glue Crawler**:
  - This service scans the transformed data in S3 and **infers the schema**.
  - It updates the metadata catalog, making data easily accessible for queries.
- **AWS Glue Data Catalog**:
  - Stores metadata and **schema definitions** for structured access.
- **Amazon Athena (Analytics)**:
  - A **serverless query engine** that enables SQL-based analysis of the processed data.

---

## **AWS Services Used**
| Service | Purpose |
|---------|---------|
| **Spotify API** | External data source |
| **AWS Lambda** | Data extraction and transformation |
| **Amazon CloudWatch** | Triggers scheduled Lambda execution |
| **Amazon S3** | Raw and transformed data storage |
| **AWS Glue Crawler** | Infers schema from transformed data |
| **AWS Glue Data Catalog** | Stores metadata for structured queries |
| **Amazon Athena** | Enables SQL-based analytics on transformed data |

---

## **Architecture Diagram**
Below is the architecture diagram representing the ETL workflow:

![AWS ETL Architecture](sandbox:/mnt/data/hd_image.png)

---

## **Conclusion**
This architecture automates the entire ETL process using **AWS serverless services**. It provides a **scalable, cost-efficient, and easily maintainable** solution for ingesting, transforming, and analyzing Spotify API data.

