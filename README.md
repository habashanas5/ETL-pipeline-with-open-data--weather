# ETL Pipeline: CSV to PostgreSQL and Google BigQuery

## Project Overview
This project implements an **ETL (Extract, Transform, Load)** pipeline using a publicly available weather dataset. The pipeline extracts data from a CSV file, performs data cleaning and transformation using Python, and loads the cleaned data into:
1. **PostgreSQL** - A relational database for local storage and analysis.
2. **Google BigQuery** - A cloud-based data warehouse for scalable data processing and analysis.

The pipeline demonstrates the use of modern data engineering tools and processes to manage, clean, and store large datasets efficiently.

---

## Tools and Technologies Used
- **Python Libraries**: 
  - `pandas` - For data cleaning and transformation.
  - `psycopg2` - For connecting to and interacting with PostgreSQL.
  - `google-cloud-bigquery` - For interacting with Google BigQuery.
  - `pandas-gbq` - For uploading data to BigQuery.
- **PostgreSQL**: Used as the local relational database.
- **Google BigQuery**: Used for cloud-based data storage and processing.
- **Google Cloud Platform (GCP)**: For BigQuery services.

---

## Pipeline Workflow

### 1. Extract
- **Source**: Weather data is provided in a CSV file named `weather_forecast_data.csv`.
- The CSV file is loaded into a pandas DataFrame for further processing.

### 2. Transform
- **Data Cleaning**:
  - Dropped rows with missing values.
  - Applied transformations, such as rounding numerical values to two decimal places (e.g., Temperature).
  - Checked for and removed any invalid or duplicate entries.
- **Data Inspection**:
  - Verified data types for each column.
  - Generated summary statistics to understand the dataset.
  - Ensured there were no missing or null values.

### 3. Load
#### (a) PostgreSQL
- A connection to a local PostgreSQL database is established using `psycopg2`.
- The cleaned data is inserted into the `weather` table in PostgreSQL.
- Example schema for the `weather` table:
  ```sql
  CREATE TABLE weather (
      id SERIAL PRIMARY KEY,
      temperature FLOAT,
      humidity FLOAT,
      wind_speed FLOAT,
      cloud_cover FLOAT,
      pressure FLOAT,
      rain VARCHAR(50)
  );

####  (b) Google BigQuery
- A connection to Google BigQuery is established using a **Google Cloud service account**.
- The cleaned data is uploaded to a BigQuery table named weather in the dataset weather_data.
- The pandas-gbq library is used to streamline the upload process, enabling efficient batch uploads and schema mapping.
