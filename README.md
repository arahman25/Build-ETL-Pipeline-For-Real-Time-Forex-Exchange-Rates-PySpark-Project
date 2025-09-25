### 🌍 **Forex Market Overview**
- **Definition**: The foreign exchange (forex) market is a global marketplace where national currencies are traded against each other.
- **Scale**: It’s the **largest and most liquid** financial market in the world.

---

### 💱 **Currency Conversion Example**
- **1 RS = 300.0 DONG**
- **USD → EUR → 1.17 USD**

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

