# 🎵 Spotify Data Pipeline 🚀

## 📖 Overview
This project builds a **data pipeline for Spotify** using `AWS Glue`, `Apache Spark`, `Snowflake`, and `Power BI`. The goal is to extract **music streaming data** from the **Spotify API**, process it, and store it in **AWS S3** before loading it into **Snowflake** for analytics.

---

## 🏗️ Architecture Diagram
```plaintext
Spotify API → Amazon CloudWatch → Python (AWS Lambda) → AWS EMR → AWS S3 → AWS Glue (Apache Spark) → Trigger → S3 (Transformed Data) → Snowpipe → Snowflake → Power BI

```

## Workflow Explanation
- 1️⃣ Extract Data from Spotify API using AWS Lambda (Python script).
- 2️⃣ Schedule Extraction with Amazon CloudWatch (daily trigger).
- 3️⃣ Store Raw Data in Amazon S3 (JSON format).
- 4️⃣ Transform Data using Apache Spark on AWS Glue.
- 5️⃣ Trigger S3 Data Processing when new data arrives.
- 6️⃣ Load Transformed Data into Snowflake via Snowpipe.
- 7️⃣ Analyze Data using Power BI for visualization.

---

## 🎯 Key Features
- ✅ Automated daily data extraction using AWS Lambda & CloudWatch.
- ✅ Scalable ETL Pipeline using Apache Spark on AWS Glue.
- ✅ Data storage in Amazon S3 (Raw + Transformed data).
- ✅ Data Warehouse Integration with Snowflake via Snowpipe.
- ✅ Visualization with Power BI for analytics & insights.

## 🛠️ Technologies Used
- Python (AWS Lambda)
- Apache Spark (PySpark)
- AWS Glue & AWS EMR
- Amazon S3
- Snowflake & Snowpipe
- Power BI

---

## Project Structure

```
spotify-data-pipeline/
│── scripts/
│   ├── extract_spotify_data.py  # Fetches data from Spotify API
│   ├── process_spotify_data.py  # Runs ETL on AWS Glue / EMR
│   ├── config.py                # Stores API keys and AWS credentials
│── data/
│   ├── raw/                     # Raw Spotify data in JSON/CSV format
│   ├── processed/               # Transformed data (Parquet/CSV)
│── notebooks/
│   ├── exploratory_analysis.ipynb  # Jupyter Notebook for analysis
│── README.md                     # Project Documentation
│── requirements.txt               # Python dependencies
│── .gitignore                     # Files to ignore in GitHub repo

```

## 📢 Future Enhancements
- ✅ Integrate real-time streaming with Kafka.
- ✅ Add Airflow for job orchestration.
- ✅ Deploy a dashboard with Power BI / Tableau.
