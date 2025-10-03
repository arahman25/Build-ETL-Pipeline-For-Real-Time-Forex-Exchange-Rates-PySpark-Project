### 🌍 **Forex Market Overview**
- **Definition**: The foreign exchange (forex) market is a global marketplace where national currencies are traded against each other.
- **Scale**: It’s the **largest and most liquid** financial market in the world.

---

### 💱 **Currency Conversion Example**
- **USD → EGP → 48.10 EGP**

---

### 🏗️ **AWS Architecture for Forex Data Processing**

| Layer              | Purpose                                                                 |
|--------------------|-------------------------------------------------------------------------|
| **Ingestion Layer** | Fetch real-time forex data from an external API                        |
| **Storage Layer**   | Store raw data in **AWS S3** for scalability and durability            |
| **Processing Layer**| Use **AWS Glue with PySpark** to transform and clean the data          |
| **Query Layer**     | Load structured data into **Amazon Redshift** for efficient querying   |
| **Visualization**   | Use **AWS QuickSight** to generate dashboards and insights             |

---

### 🧠 **Forex Data Pipeline – Layered Architecture Overview**

#### ✅ **1. Ingestion Layer (Completed)**
- **Purpose**: Fetch raw Forex data and store it in S3.
- **Tasks**:
  - Call external API to retrieve exchange rate data.
  - Save raw JSON files into the `S3/raw/` folder.
  - Automate ingestion using **AWS Lambda** and **EventBridge Scheduler**.

---

#### 🔄 **2. Processing Layer (Next Step)**
- **Purpose**: Clean, transform, and enrich the raw data.
- **Tasks**:
  - Use **AWS Glue (PySpark)** to process the JSON files.
  - Convert data into structured format (e.g., **Parquet**).
  - Apply transformations: filtering, aggregations, timestamping.
  - Save processed output into `S3/processed/` folder.

---

#### 📦 **3. Storage Layer**
- **Purpose**: Store structured data for analytics and querying.
- **Tasks**:
  - Load transformed data into **Amazon Redshift** (Data Warehouse).
  - Optimize schema for fast querying and dashboard performance.
  - Ensure consistency and reliability across datasets.

---

### 🔍 **4. Query & Analysis Layer**
- **Purpose**: Enable insights, reporting, and data visualization.
- **Components**:
  - Use **Amazon Redshift** to run SQL queries on structured data.
  - Connect to **BI tools** like **Tableau** and **QuickSight** for visualization.
  - Perform **analytics**, **trend analysis**, and **forecasting**.

---

### 📡 **5. Monitoring & Logging Layer**
- **Purpose**: Track pipeline performance, detect failures, and log events.
- **Components**:
  - Use **AWS CloudWatch** to monitor **Lambda** and **Glue** jobs.
  - Set up **CloudWatch Logs** and **Alarms** for error detection.
  - Implement **SNS notifications** to alert on failures.

---

### 📊 **Summary of Layers & Their Roles – Forex Data Pipeline**

| 🔹 **Layer**             | 🔍 **Purpose**                                | ⚙️ **Technology Used**                          | 📌 **Status**         |
|--------------------------|-----------------------------------------------|--------------------------------------------------|------------------------|
| **Ingestion Layer**      | Fetch & store raw Forex data in S3            | API, AWS Lambda, S3, EventBridge                | ✅ Completed           |
| **Processing Layer**     | Transform & clean data                        | AWS Glue (PySpark)                              | ✅ Completed           |
| **Storage Layer**        | Store structured data for querying            | Amazon Redshift, S3                             | ⏳ Pending             |
| **Query & Analysis Layer**| Analyze, visualize, generate insights         | Amazon Redshift, BI Tools (Tableau)             | ⏳ Pending             |
| **Monitoring Layer**     | Track performance, detect failures            | AWS CloudWatch, SNS                             | ⏳ Pending             |

---

### 🧾 **Indigestion Layer – Completed Setup**

| ✅ **Task**                                                                                   |
|----------------------------------------------------------------------------------------------|
| Created an **S3 Bucket** to store raw Forex data                                             |
| Created an **IAM User** and configured **AWS CLI**                                           |
| Built a **Python script** to fetch Forex data and upload to S3                              |
| Created an **AWS Lambda Function** to automate ingestion                                     |
| Resolved issues: missing libraries, permissions, execution errors                            |
| Successfully executed Lambda manually and verified file upload in S3                         |
| Automated Lambda using **AWS EventBridge Scheduler**                                         |
| Verified scheduled execution every **5 minutes** and confirmed correct data upload           |

---

### 🔄 **Indigestion Layer Purpose**
- **Fetch real-time Forex exchange rates** from an external API.
- **Store raw data** in AWS S3 for downstream processing.

---

### 🔐 **LOGIN TO AWS – Initial Setup Guide**  

#### 🧭 **Step 1.1: Where to Start?**
Before setting up your S3 bucket to store raw Forex data, you need to log in to AWS.

---

### 🖥️ **How to Log In to AWS**
1. Go to the AWS Console: [https://aws.amazon.com/console](https://aws.amazon.com/console)  
2. Click **Sign In**  
3. Enter your AWS account credentials  
   - Or create a new account if you don’t have one  
4. After logging in, you’ll be redirected to the **AWS Management Console**

---

### 🌐 **Forex API Comparison**

| 🔹 **API Name**     | 🆓 **Free Plan** | ⏱️ **Update Frequency** | 📦 **Data Provided**                              |
|---------------------|------------------|--------------------------|---------------------------------------------------|
| **Alpha Vantage**   | Yes              | Every 1 min              | Exchange rates, historical data                   |
| **Currencylayer**   | Yes              | Every 1 hr               | Exchange rates, currency conversions              |
| **ForexDataAPI**    | No               | Real-time                | Forex pairs, historical data                      |
| **X-Rates**         | Yes              | Every 1 hr               | Exchange rates                                    |

---

### ✅ **Recommended Option**
- **Alpha Vantage** is highlighted as the preferred choice:
  - Free and easy to use
  - Provides an **API Key** upon signup
  - Reminder: **Keep your API key safe**

---

### 🔑 **Step 2.1 – Generate & Store Your API Key**

- **Purpose**: To authenticate requests when fetching Forex data from Alpha Vantage.
- **Instructions**:
  - Visit: [https://www.alphavantage.co/support/#api-key](https://www.alphavantage.co/support/#api-key)
  - Sign up or log in to generate your personal **API key**
  - Store the key securely for use in your Python scripts or Lambda functions

---

### 🧪 **Sample API Key Format**
- Example shown: `5KJ6CAN2GNFGA9N**RPGMOWD5SOTTYSCI`  
  *(Note: Only partial key is visible for security)*

---

### 🌐 **Step 2.2 – Constructing an API Request (Alpha Vantage)**

#### 🔗 **Example API Request URL**
```plaintext
https://www.alphavantage.co/query?function=CURRENCY_EXCHANGE_RATE&from_currency=USD&to_currency=EGP&apikey=your_api_key
```
> Replace `your_api_key` with your actual Alpha Vantage key.

---

### 🧩 **API Request Breakdown**

- **API Endpoint**:  
  `https://www.alphavantage.co/query?`  
  *(This is the base URL used to make requests)*

- **API Parameters**:  
  These customize the request and define what data you want.

| 🏷️ **Parameter**     | 🧪 **Value Example**           | 📘 **Description**                                      |
|----------------------|-------------------------------|---------------------------------------------------------|
| `function`           | `CURRENCY_EXCHANGE_RATE`      | Specifies you want real-time forex exchange rates       |
| `from_currency`      | `USD`                         | Base currency                                            |
| `to_currency`        | `EGP`                         | Target currency                                          |
| `apikey`             | `5KCJ6AN2GNFCAGN`             | Your unique Alpha Vantage API key                       |

---

### 📦 **Step 2.3 – Sample API Response (Alpha Vantage)**

When you call the **CURRENCY_EXCHANGE_RATE** endpoint, the API returns a JSON object like this:

```json
{
  "Realtime Currency Exchange Rate": {
    "1. From_Currency Code": "USD",
    "2. From_Currency Name": "United States Dollar",
    "3. To_Currency Code": "EGP",
    "4. To_Currency Name": "Egyptian Pound",
    "5. Exchange Rate": "48.1056",
    "6. Last Refreshed": "2025-09-24 16:00:00",
    "7. Time Zone": "UTC"
  }
}
```

---

### 🔍 **What to Check in the Response**
- ✅ Real-time forex data for **EUR to USD**
- ✅ Key fields:
  - `"Exchange Rate"`
  - `"From_Currency Code"` and `"To_Currency Code"`
  - `"Last Refreshed"` timestamp
- ⚠️ If the response is missing or contains errors:
  - It may be due to **API rate limits**
  - Or an **invalid API key**

---

### ✅ **API Setup Checklist – Completed Tasks**

| 🔹 **Task**                                                                                          |
|------------------------------------------------------------------------------------------------------|
| You’ve generated your **API key** and saved it securely                                              |
| You’ve noted the **API endpoint**, parameters, and key                                               |
| You’ve constructed your API request using: `endpoint + parameters + API key`                         |
| You’ve successfully tested the API in your browser and received a valid response                     |
| Your response includes: `"From Currency Name"`, `"To Currency Name"`, `"Exchange Rate"`, etc.       |
| You understand the **update frequency** (every minute for free tier)                                |
| You’ve checked the **rate limit** (number of free requests per day)                                 |

---

### ❓ **Self-Check Question**

**Q: What is an API Endpoint?**  
**A:** An API endpoint is the **URL you call to request data**.

**Example:**  
For Alpha Vantage’s Forex API, the endpoint is:  
`https://www.alphavantage.co/query`

---

### 🧩 **Understanding API Parameters – Alpha Vantage**

#### 📘 **What Are API Parameters?**
- Parameters help **customize your API request**.
- You need to specify the following:

| 🔹 **Parameter**     | 📌 **Purpose**                                      |
|----------------------|-----------------------------------------------------|
| `function`           | Defines the type of data you want (e.g., exchange rate) |
| `from_currency`      | The base currency (e.g., USD)                       |
| `to_currency`        | The target currency (e.g., EGP)                     |
| `apikey`             | Your unique Alpha Vantage API key                   |

---

### ⏱️ **Data Update Frequency**
- **Alpha Vantage API updates data every minute** for the free tier.
- This ensures near real-time access to currency exchange rates.

---

### 📦 Step 3: Create an S3 Bucket to Store Raw Data

Amazon S3 will serve as the storage layer for raw Forex data before any processing begins.

#### 🔧 How to Create the Bucket
1. **Navigate to AWS Console → S3**  
   [AWS S3 Console](https://s3.console.aws.amazon.com/s3/)
2. **Click**: `Create Bucket`
3. **Fill in the following details**:
   - **Bucket Name**: `forex-data-bucket`
   - **Region**: Choose one close to your users (e.g., `us-east-1`)
4. **Enable Versioning** *(Optional)*  
   - Useful for tracking historical changes to stored data.
5. **Click**: `Create Bucket`

#### 📁 Folder Structure in S3
Organize raw data using a date-based hierarchy:

```
s3://forex-data-bucket/raw/yyyy/MM/dd/
```

**Example for February 7, 2025**:
```
s3://forex-data-bucket/raw/2025/02/07/
```

---

### 🧭 What Are AWS Glue Crawlers Used For?

AWS Glue Crawlers automatically scan and catalog data from various sources into the **AWS Glue Data Catalog**, enabling seamless data discovery and querying.

#### 🔍 Key Uses of AWS Glue Crawlers
1. **Automated Schema Discovery**  
   - Crawlers analyze raw data and infer column names, data types, and structure.
2. **Metadata Extraction**  
   - Extract metadata from sources like S3, Redshift, RDS, DynamoDB, and store it in the Glue Data Catalog.
3. **Incremental Crawls**  
   - Detect and update schema changes incrementally without manual intervention.
4. **Query Enablement for Athena & Redshift Spectrum**  
   - Prepare data for querying without manually defining schemas.

#### 📁 Example Use Case
If you have **CSV files in S3**, a Glue Crawler can scan them and automatically register the schema in the Glue Data Catalog—no manual table definition required.

---

### 🐍 Install Python Dependencies (Local Setup)

**Option 1: Install Python Locally**  
_Recommended for learning and debugging._

#### 🔧 Step 1: Install Python
1. **Download Python** from the official site:  
   [python.org/downloads](https://www.python.org/downloads/)
2. **Mac Users**:
   - Press `Command + Space` and search for **Terminal**
   - Open Terminal and run:
     ```
     python3 --version
     ```
   - If installed correctly, it should return something like:
     ```
     Python 3.x.x
     ```

---

#### ✅ Step 2: Install Required Python Libraries

Install the necessary libraries to fetch Forex data and interact with AWS services:

```bash
python3 -m pip install requests boto3
```

Alternatively, install them individually:

```bash
pip3 install requests     # For making API calls
pip3 install boto3        # For interacting with AWS (e.g., S3)
```

- **`requests`** → Used to fetch Forex data via API calls  
- **`boto3`** → AWS SDK for Python, used to upload data to S3 and other services

---

#### 📝 Step 3: Create a Python Script

Open a text editor and create a new file named:

```
forex_fetch.py
```

This script will contain the logic to retrieve Forex data and push it to AWS.

---

### 🧾 Step 4: Write the Python Script

This script fetches real-time currency exchange data using the **Alpha Vantage API**.

#### 🐍 Python Code Overview

```python
import requests

# API Configuration
API_KEY = "API_KEY"  # Replace with your actual API key
BASE_URL = "https://www.alphavantage.co/query"
CURRENCY_FROM = "USD"
CURRENCY_TO = "EGP"

# Define API Parameters
params = {
    "function": "CURRENCY_EXCHANGE_RATE",
    "from_currency": CURRENCY_FROM,
    "to_currency": CURRENCY_TO,
    "apikey": API_KEY
}

# Fetch Data
response = requests.get(BASE_URL, params=params)
data = response.json()

# Print the Response
print(data)
```

---

