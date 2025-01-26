# AWS CloudWatch, S3 Bucket Setup, and AWS Lambda Function with Environment Variables

## **Step 1: Setting a Budget Alarm in AWS CloudWatch**
To ensure you don’t exceed your AWS budget, follow these steps:

1. **Go to AWS Billing Dashboard**:
   - Sign in to **AWS Management Console**.
   - Navigate to **Billing** > **Budgets**.

2. **Create a New Budget**:
   - Click on **Create a budget**.
   - Select **Cost budget**.
   - Set the **monthly budget limit**.

3. **Set Up Alerts**:
   - Define the **threshold percentage** (e.g., **80% of the budget**).
   - Choose an **email recipient** or an **SNS topic** to receive notifications.

4. **Enable CloudWatch Alarms**:
   - Under **Notifications**, enable **CloudWatch Alarms**.
   - AWS will notify you when your spending approaches the defined limit.

---

## **Step 2: Setting Up an S3 Bucket for Data Storage**
1. **Create an S3 Bucket**:
   - Navigate to **AWS S3**.
   - Click on **Create Bucket**.
   - Enter a **unique bucket name** (e.g., `spotify-data-bucket`).
   - Choose a region (e.g., `us-east-1`).
   - Click **Create**.

2. **Create Folder Structure Inside the S3 Bucket**:
   - **Raw Data Folder** (`raw/`):
     - `raw/processed/`
     - `raw/to_process/`
   - **Transformed Data Folder** (`transformed/`):
     - `transformed/album_data/`
     - `transformed/artists_data/`
     - `transformed/songs_data/`

📌 *This structure helps organize data at different pipeline stages (raw vs transformed).*

---

## **Step 3: Creating AWS Lambda Function for Spotify API Extraction**
### **1. Create an AWS Lambda Function**
1. Go to **AWS Lambda** in the AWS Console.
2. Click **Create Function**.
3. Choose **Author from Scratch**.
4. Enter a **Function Name** (e.g., `spotify_data_extractor`).
5. Choose **Python (latest version)** as the runtime.
6. Set **Permissions**:
   - Attach a role that allows **S3 write access**.

---

### **2. Store Spotify API Credentials in Environment Variables**
Instead of hardcoding **API keys** in the Python script, we store them securely in AWS Lambda’s **Environment Variables**.

#### **How to Add Environment Variables in Lambda:**
1. In the **Lambda function console**, go to the **Configuration** tab.
2. Click on **Environment Variables**.
3. Click **Edit** and add the following key-value pairs:
   - `SPOTIFY_CLIENT_ID = your_client_id`
   - `SPOTIFY_CLIENT_SECRET = your_client_secret`
4. Click **Save**.

Now, you can access these values in your Python script using:
```python
import os

SPOTIFY_CLIENT_ID = os.getenv("SPOTIFY_CLIENT_ID")
SPOTIFY_CLIENT_SECRET = os.getenv("SPOTIFY_CLIENT_SECRET")

```

5. 📌 This ensures security and prevents API keys from being hardcoded into the script.
