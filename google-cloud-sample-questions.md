# Google Cloud Sample Questions

## 1. Cloud Storage Backup Files

**Your company uses Cloud Storage to store application backup files for disaster recovery purposes. You want to follow Google's recommended practices. Which storage option should you use?**

**A.** Multi-Regional Storage  
**B.** Regional Storage  
**C.** Nearline Storage  
**D.** Coldline Storage

---

## 2. BigQuery Query Cost Estimation

**You need to run an important query in BigQuery but expect it to return a lot of records. You want to find out how much it will cost to run the query. You are using on-demand pricing. What should you do?**

**A.** Arrange to switch to Flat-Rate pricing for this query, then move back to on-demand.

**B.** Use the command line to run a dry run query to estimate the number of bytes read. Then convert that bytes estimate to dollars using the Pricing Calculator.

**C.** Use the command line to run a dry run query to estimate the number of bytes returned. Then convert that bytes estimate to dollars using the Pricing Calculator.

**D.** Run a `SELECT COUNT(*)` to get an idea of how many records your query will look through. Then convert that number of rows to dollars using the Pricing Calculator.

---

## 3. Globally Scalable Relational Database

**You are building an application that stores relational data from users. Users across the globe will use this application. Your CTO is concerned about the scaling requirements because the size of the user base is unknown. You need to implement a database solution that can scale with your user growth with minimum configuration changes. Which storage solution should you use?

**A.** Cloud SQL  
**B.** Cloud Spanner  
**C.** Cloud Firestore  
**D.** Cloud Datastore

---

## 4. Time-Series Data Pipeline

**You are building a pipeline to process time-series data. Which Google Cloud Platform services should you put in boxes 1, 2, 3, and 4?**

**A.** Cloud Pub/Sub, Cloud Dataflow, Cloud Datastore, BigQuery

**B.** Firebase Messages, Cloud Pub/Sub, Cloud Spanner, BigQuery

**C.** Cloud Pub/Sub, Cloud Storage, BigQuery, Cloud Bigtable

**D.** Cloud Pub/Sub, Cloud Dataflow, Cloud Bigtable, BigQuery

---

## 5. Archival Storage for Quarterly Access

**You are building an archival solution for your data warehouse and have selected Cloud Storage to archive your data. Your users need to be able to access this archived data once a quarter for some regulatory requirements. You want to select a cost-efficient option. Which storage option should you use?**

**A.** Coldline Storage  
**B.** Nearline Storage  
**C.** Regional Storage  
**D.** Multi-Regional Storage

---

## 6. ETL Processing of Unstructured Data

**Your company has a large quantity of unstructured data in different file formats. You want to perform ETL transformations on the data. You need to make the data accessible on Google Cloud so it can be processed by a Dataflow job. What should you do?**

**A.** Upload the data to BigQuery using the `bq` command line tool.

**B.** Upload the data to Cloud Storage using the `gsutil` command line tool.

**C.** Upload the data into Cloud SQL using the import function in the console.

**D.** Upload the data into Cloud Spanner using the import function in the console.

---

## 7. Bigtable Row Key Design

**Your company is streaming real-time sensor data from their factory floor into Bigtable and they have noticed extremely poor performance. How should the row key be redesigned to improve Bigtable performance on queries that populate real-time dashboards?**

**A.** Use a row key of the form `<timestamp>`.

**B.** Use a row key of the form `<sensorid>`.

**C.** Use a row key of the form `<timestamp>#<sensorid>`.

**D.** Use a row key of the form `>#<sensorid>#<timestamp>`.

---

## 8. Financial Time-Series Data and Hadoop

**Your financial services company is moving to cloud technology and wants to store 50 TB of financial time-series data in the cloud. This data is updated frequently and new data will be streaming in all the time. Your company also wants to move their existing Apache Hadoop jobs to the cloud to get insights into this data. Which product should they use to store the data?**

**A.** Cloud Bigtable

**B.** Google BigQuery

**C.** Google Cloud Storage

**D.** Google Cloud Datastore

---

## 9. Migrating a 2 TB Relational Database

**You need to migrate a 2 TB relational database to Google Cloud Platform. You do not have the resources to significantly refactor the application that uses this database and cost to operate is of primary concern. Which service do you select for storing and serving your data?**

**A.** Cloud Spanner

**B.** Cloud Bigtable

**C.** Cloud Firestore

**D.** Cloud SQL

---

## 10. Minimum Storage Duration for Archive Storage

**What is the minimum storage duration for the Archive storage class?**

**A.** 180 days  
**B.** 200 days  
**C.** 365 days  
**D.** 60 days

---

## 11. Bigtable NoSQL Type

**Google Bigtable in GCP supports which type of NoSQL?**

**A.** Document databases.

**B.** Key-value stores.

**C.** Column-oriented databases.

**D.** Graph databases.

---

## 12. Data Analysis Without a Database Administrator

**Which of the following services in GCP is used for analyzing the data to find meaningful results without the need for any database administrator?**

**A.** Google Bigtable

**B.** Cloud SQL

**C.** BigQuery

**D.** Google Cloud Datastore

**E.** Cloud Dataflow

---

## 14. Apache Hadoop and Spark

**Which service in GCP is used as the service for running Apache Hadoop and Spark jobs?**

**A.** Google Cloud Datastore

**B.** Google Cloud SQL

**C.** Google BigQuery

**D.** Google Dataproc

---

## 15. Centralized Monitoring and Alerts

**Which of the following GCP services provides you the ability to rapidly view alerts, logs, and metrics from GCP resources on your cloud? This service is also known as the centralized method of receiving signals.**

**A.** Google Monitoring Service

**B.** Google Stackdriver

**C.** Cloud Armor

**D.** Cloud Security Scanner

---

## 16. SQL Join Matching Records

**Which of the following joins returns the records that match the values for the join columns from both tables?**

Choose the correct option:

**A.** Right outer join

**B.** Inner joins

**C.** Left outer join

**D.** Full outer join

---

## 17. Logical Collection of Tables

**A logical collection of tables is known as _______.**

Choose the correct option:

**A.** Datasets

**B.** Collection

**C.** Jobs

**D.** Schema

---

## 18. BigQuery Implementation

**Google BigQuery is the public implementation of ______.**

Choose the correct option:

**A.** Dremel

**B.** Percolator

**C.** Pregel

**D.** None of the options

---

## 19. Dataflow Triggers

**What Dataflow concept determines when a Window's contents should be output based on certain criteria being met?**

**A.** Sessions

**B.** OutputCriteria

**C.** Windows

**D.** Triggers

---

## 20. Dataflow Processing Component

**You are developing a software application using Google's Dataflow SDK, and want to use conditional statements, `for` loops, and other complex programming structures to create a branching pipeline. Which component will be used for the data processing operation?**

**A.** PCollection

**B.** Transform

**C.** Pipeline

**D.** Sink API
