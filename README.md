# AWS Athena Data Analytics Lab

![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Amazon S3](https://img.shields.io/badge/Amazon%20S3-569A31?style=for-the-badge&logo=amazon-s3&logoColor=white)
![Amazon Athena](https://img.shields.io/badge/Amazon%20Athena-FF9900?style=for-the-badge&logo=amazon-aws&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=for-the-badge&logo=amazon-dynamodb&logoColor=white)

A hands-on data engineering project demonstrating serverless data analytics using Amazon Athena and S3. This lab showcases the implementation of a cost-effective, scalable data warehouse solution for querying structured data directly from S3 storage using SQL.

## Objective

Build and configure a serverless data analytics pipeline on AWS to query CSV data stored in Amazon S3 using Amazon Athena's Trino SQL engine. This project demonstrates proficiency in cloud-based data engineering, serverless architectures, and SQL-based data analysis without the overhead of managing database infrastructure.

## Real-World Business Use Case

### Hypothetical Scenario: Digital Library Analytics Platform

**Business Context:**  
A growing digital publishing company manages a catalog of thousands of books across multiple authors and publication years. The marketing and acquisitions teams need to analyze inventory trends, identify popular authors, and make data-driven decisions about which genres and time periods to prioritize for new acquisitions.

**Challenge:**  
Traditional database solutions require significant infrastructure investment, ongoing maintenance, and capacity planning. The company needs a cost-effective solution that:
- Scales automatically with query volume
- Charges only for queries executed (pay-per-query model)
- Allows business analysts to run ad-hoc SQL queries without database administration overhead
- Integrates seamlessly with existing S3 data lake storage

**Solution:**  
Implement Amazon Athena as a serverless query engine to analyze book catalog data stored in S3. This approach eliminates database servers, reduces operational costs by up to 70%, and enables analysts to extract insights using familiar SQL syntax within seconds.

## Key Features

### Infrastructure & Architecture
- **Serverless Query Engine**: Zero infrastructure management using Amazon Athena
- **S3-Based Data Lake**: Decoupled storage and compute for cost optimization
- **Schema-on-Read**: Flexible data modeling without upfront transformations
- **Query Result Management**: Dedicated S3 bucket for result caching and reuse

### Data Operations
- **CSV Data Ingestion**: Upload and query structured data from CSV files
- **Hive-Compatible Metadata**: Apache Hive table definitions for broad compatibility
- **SQL Query Interface**: Standard ANSI SQL queries via Trino engine
- **Security Best Practices**: S3 bucket public access blocking enabled by default

### Analytics Capabilities
- **Filtering & Aggregation**: WHERE clauses for targeted data retrieval
- **Sorting & Ordering**: ASC/DESC sorting on timestamp and text fields
- **Distinct Value Analysis**: Identify unique authors and categories
- **Date Range Queries**: Filter publications by year ranges

## Technology Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Cloud Provider** | Amazon Web Services (AWS) | Cloud infrastructure platform |
| **Object Storage** | Amazon S3 | Raw data storage and query result storage |
| **Query Engine** | Amazon Athena (Trino) | Serverless SQL query execution |
| **Data Format** | CSV | Structured data file format |
| **Table Metadata** | Apache Hive | Schema definition and data cataloging |
| **Query Language** | SQL (ANSI Standard) | Data analysis and manipulation |


## Implementation Summary

### Workflow

#### 1. Data Acquisition
- Downloaded `libros_laboratorio.csv` dataset containing book catalog information
- Dataset schema: `autor` (string), `libro` (string), `year` (integer)

#### 2. S3 Storage Configuration
**Data Bucket Creation:**
- Created S3 bucket for raw data storage with globally unique name
- Enabled default encryption and versioning
- Blocked all public access for security compliance
- Uploaded CSV file via AWS Console

**Results Bucket Creation:**
- Created dedicated S3 bucket for Athena query output
- Configured as Athena query result location
- Enables query result caching and historical analysis

#### 3. Athena Configuration
- Opened Athena Query Editor with Trino engine
- Configured query result location pointing to results bucket
- Selected default database for table creation

#### 4. Table Schema Definition
**DDL Implementation:**
CREATE EXTERNAL TABLE IF NOT EXISTS tablalibros (
    autor STRING,
    libro STRING,
    year INT
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION 's3://your-data-bucket-name/'
TBLPROPERTIES ('skip.header.line.count'='1');

**Configuration Details:**
- Table Type: Apache Hive (for broad tool compatibility)
- File Format: CSV with comma delimiter
- Storage Location: S3 data bucket path
- Header Handling: Skip first row (column names)

#### 5. Data Validation & Analysis
Executed comprehensive SQL queries to validate data integrity and extract business insights (see Validation SQL Queries section below).

## Validation SQL Queries

### 1. Complete Dataset Retrieval
```sql
SELECT * FROM tablalibros;
```
**Purpose:** Verify successful table creation and data loading. Returns all records with all columns.

### 2. Author-Specific Filtering
```sql
SELECT * FROM tablalibros 
WHERE autor = 'Dean Koontz';
```
**Purpose:** Demonstrate WHERE clause filtering. Retrieves all books by specific author for targeted catalog analysis.

### 3. Publication Date Range Filter
```sql
SELECT * FROM tablalibros 
WHERE year > 2000;
```
**Purpose:** Filter modern publications. Useful for identifying recent acquisitions and trending authors.


## Key Learnings

### Technical Skills Acquired

#### 1. Serverless Data Architecture
- Designed and implemented a serverless analytics pipeline eliminating database management overhead
- Understood the separation of storage (S3) and compute (Athena) for cost optimization
- Learned pay-per-query pricing model vs. traditional always-on database costs

#### 2. Amazon S3 Best Practices
- Created and configured S3 buckets with security-first approach (public access blocking)
- Implemented bucket naming conventions for globally unique identifiers
- Organized data lake structure with separate buckets for raw data and query results
- Uploaded and managed structured data files in cloud object storage

#### 3. Amazon Athena Query Engine
- Configured Athena with Trino SQL engine for serverless query execution
- Set up query result locations for output persistence and caching
- Created external tables using Hive metastore for schema-on-read operations
- Executed ANSI SQL queries against S3-stored data without data movement

## Acknowledgments

Special thanks to **Workshop M&O** for providing comprehensive hands-on AWS training materials and guided laboratory environment.

---

*This project is for educational purposes.*
