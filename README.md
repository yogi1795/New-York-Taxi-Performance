# 🚕 End-to-End Microsoft Fabric Project – NYC Taxi Data
This project showcases a complete **data pipeline** built using **Microsoft Fabric**, using open-source **NYC Taxi data**. From ingesting Parquet files to transforming and reporting, everything was executed in an integrated, cloud-native Fabric environment.

### 📦 Data Ingestion and Storage Setup
- Downloaded **12 monthly Parquet files** from the NYC Taxi & Limousine Commission portal.

- Created a **Lakehouse** in Microsoft Fabric.

- Organized the Files section into:

- - One folder for the **Parquet ride data**

- - One folder for **lookup table** data (e.g., zone mappings)

### 🔁 Data Movement Using Pipelines
I created a Data Factory Pipeline to automate the data movement from Lakehouse to Warehouse with the following structure:

- Used a ForEach activity to:

- - Iterate through the list of file names (e.g., yellow_tripdata_2024_01.parquet)

- - Copy each file’s data from the Lakehouse to a **staging schema** in the **Fabric Warehouse**

- - Automatically **create tables dynamically** during each iteration

- Inside the loop:

- - Included a **SQL Script activity to filter each table based** on the inferred month from the filename (ensuring data consistency)

- Outside the loop:

- - Added a **SQL Script activity** to **UNION all staging tables** into a single **master fact table**

### 🧹 Data Cleaning and Standardization
- Created a **Dataflow Gen2** to:

- - Clean and standardize the combined dataset

- - Merge it with the lookup tables to enrich pickup/drop-off location data

- - Cast all fields to correct data types (dates, floats, integers)

### 📊 Reporting with Power BI
- Built a Power BI report directly on top of the cleaned and enriched data from the Warehouse

- The report includes:

- - Trends in trip count over months

- - Revenue distribution by vendor

- - Payment method patterns across locations

- - Average distance, fare amount, and passenger counts

### 🧠 Key Learnings and Observations
- **Fabric Pipelines do not support dynamic table names inside Stored Procedures**

- I **overcame this by using Script Activities with parameters**, enabling a dynamic yet controlled workflow

- This approach maintains modularity and avoids manual table handling

### 💡 Skills Demonstrated
✅ Lakehouse architecture and file organization
✅ Pipelines with parameterized ForEach loops
✅ Dynamic SQL scripting and table handling
✅ Data cleansing and enrichment via Dataflows
✅ Seamless integration with Power BI for reporting
