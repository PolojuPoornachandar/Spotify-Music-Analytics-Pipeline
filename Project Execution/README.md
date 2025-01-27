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

----

## AWS Boto3 Package and Its Importance

## What is Boto3?
Boto3 is the AWS SDK for Python, which allows developers to interact with AWS services programmatically. It is essential for working with AWS resources such as S3, Lambda, EC2, and more. In our case, we use Boto3 to extract data from the Spotify API and dump it into an S3 bucket using AWS Lambda.

## Why Do We Need to Create Layers in AWS Lambda?
AWS Lambda has a size limit for deployment packages, and including additional dependencies like Boto3 can increase the package size significantly. Creating layers helps in:
- **Reducing redundancy:** Reusable libraries like Boto3 can be shared across multiple Lambda functions.
- **Optimizing function performance:** Layers keep the function package lightweight, leading to faster deployment and execution.
- **Easy dependency management:** Updating the Boto3 package separately without modifying the entire Lambda function.

## Dumping Data to S3 Using Boto3
To store data in an S3 bucket from AWS Lambda, we use the Boto3 client to interact with S3. Below is an example of how to dump Spotify API data into an S3 bucket:

```python
import boto3
import json

# Initialize S3 client
client = boto3.client("s3")

# Define bucket and data
bucket_name = "your-bucket-name"
file_path = "path/to/store/data.json"
spotify_data = {"example": "data from Spotify API"}

# Upload data to S3
client.put_object(
    Bucket=bucket_name,
    Key=file_path,
    Body=json.dumps(spotify_data)
)
```

## Why Do We Need IAM Roles for AWS Services?
When two AWS services need to communicate (e.g., Lambda storing data in S3), we must assign proper permissions using IAM roles. IAM roles allow Lambda to have:
- **Read/write access to S3 buckets**
- **Permissions to trigger events using CloudWatch**
- **Secure access management without embedding credentials in the code**

To create an IAM role:
1. Navigate to AWS IAM Console.
2. Create a new role with the **AWS Lambda** trusted entity.
3. Attach an S3 policy allowing write access to the desired bucket.
4. Attach the IAM role to the Lambda function.

## Automating Data Extraction Using CloudWatch Triggers
To ensure the data is continuously pulled from Spotify API to S3, we can set up an AWS CloudWatch event trigger:
- **Step 1:** Go to AWS Lambda Console.
- **Step 2:** Select the Lambda function.
- **Step 3:** Click on "Add Trigger" and choose "CloudWatch Events."
- **Step 4:** Define a schedule expression (e.g., `rate(5 minutes)`) to trigger Lambda every 5 minutes.
- **Step 5:** Save the configuration and deploy.

This setup ensures the Lambda function extracts data from Spotify API and dumps it into S3 at regular intervals.

