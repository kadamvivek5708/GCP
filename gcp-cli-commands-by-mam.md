# GCP CLI Commands – Cloud Services

## 1. GCP Authentication and Project

### Authenticate with Google Cloud

```bash
gcloud auth login
```

### List authenticated accounts

```bash
gcloud auth list
```

### List GCP projects

```bash
gcloud projects list
```

### Set the active project

```bash
gcloud config set project PROJECT_ID
```

### View the current gcloud configuration

```bash
gcloud config list
```

---

# 2. Cloud Storage

### List buckets

```bash
gcloud storage buckets list
```

### Create a bucket

```bash
gcloud storage buckets create gs://BUCKET_NAME \
    --location=asia-south1
```

### List objects

```bash
gcloud storage ls gs://BUCKET_NAME
```

### Upload a file

```bash
gcloud storage cp file.txt gs://BUCKET_NAME/
```

### Download a file

```bash
gcloud storage cp gs://BUCKET_NAME/file.txt .
```

### Delete an object

```bash
gcloud storage rm gs://BUCKET_NAME/file.txt
```

### Delete a bucket

```bash
gcloud storage buckets delete gs://BUCKET_NAME
```

---

# 3. Cloud SQL

### List Cloud SQL instances

```bash
gcloud sql instances list
```

### Create a MySQL instance

```bash
gcloud sql instances create my-mysql \
    --database-version=MYSQL_8_0 \
    --tier=db-f1-micro \
    --region=asia-south1
```

### Describe an instance

```bash
gcloud sql instances describe my-mysql
```

### Create a database

```bash
gcloud sql databases create mydb \
    --instance=my-mysql
```

### List databases

```bash
gcloud sql databases list \
    --instance=my-mysql
```

### Create a user

```bash
gcloud sql users create myuser \
    --instance=my-mysql \
    --password=PASSWORD
```

### Connect to MySQL

```bash
gcloud sql connect my-mysql \
    --user=root
```

---

# 4. Cloud Spanner

### List Spanner instances

```bash
gcloud spanner instances list
```

### Create a Spanner instance

```bash
gcloud spanner instances create my-spanner \
    --config=regional-asia-south1 \
    --description="My Spanner" \
    --nodes=1
```

### Describe an instance

```bash
gcloud spanner instances describe my-spanner
```

### Create a database

```bash
gcloud spanner databases create mydb \
    --instance=my-spanner
```

### List databases

```bash
gcloud spanner databases list \
    --instance=my-spanner
```

### Execute SQL

```bash
gcloud spanner databases execute-sql mydb \
    --instance=my-spanner \
    --sql="SELECT * FROM Users"
```

---

# 5. Firestore

### List Firestore databases

```bash
gcloud firestore databases list
```

### Create a Firestore database

```bash
gcloud firestore databases create \
    --location=asia-south1 \
    --type=firestore-native
```

### Describe the default database

```bash
gcloud firestore databases describe \
    --database="(default)"
```

---

# 6. Bigtable

### List Bigtable instances

```bash
gcloud bigtable instances list
```

### Create a Bigtable instance

```bash
gcloud bigtable instances create my-bigtable \
    --cluster=my-cluster \
    --cluster-zone=asia-south1-a \
    --display-name="My Bigtable"
```

### Describe an instance

```bash
gcloud bigtable instances describe my-bigtable
```

### List clusters

```bash
gcloud bigtable clusters list \
    --instances=my-bigtable
```

### Create a table

```bash
gcloud bigtable tables create users \
    --instance=my-bigtable
```

### List tables

```bash
gcloud bigtable tables list \
    --instance=my-bigtable
```

### Create a column family

```bash
gcloud bigtable families create profile \
    --instance=my-bigtable \
    --table=users
```

---

# 7. Pub/Sub

### List topics

```bash
gcloud pubsub topics list
```

### Create a topic

```bash
gcloud pubsub topics create my-topic
```

### Create a subscription

```bash
gcloud pubsub subscriptions create my-sub \
    --topic=my-topic
```

### List subscriptions

```bash
gcloud pubsub subscriptions list
```

### Publish a message

```bash
gcloud pubsub topics publish my-topic \
    --message="Hello Google Cloud"
```

### Pull a message

```bash
gcloud pubsub subscriptions pull my-sub \
    --auto-ack
```

### Delete a topic

```bash
gcloud pubsub topics delete my-topic
```

---

# 8. Dataproc

### List Dataproc clusters

```bash
gcloud dataproc clusters list \
    --region=asia-south1
```

### Create a single-node cluster

```bash
gcloud dataproc clusters create my-cluster \
    --region=asia-south1 \
    --single-node
```

### Describe a cluster

```bash
gcloud dataproc clusters describe my-cluster \
    --region=asia-south1
```

### Submit a PySpark job

```bash
gcloud dataproc jobs submit pyspark gs://BUCKET_NAME/job.py \
    --cluster=my-cluster \
    --region=asia-south1
```

### List jobs

```bash
gcloud dataproc jobs list \
    --region=asia-south1
```

### Delete a cluster

```bash
gcloud dataproc clusters delete my-cluster \
    --region=asia-south1
```

---

# 9. Dataflow

### List Dataflow jobs

```bash
gcloud dataflow jobs list \
    --region=asia-south1
```

### Describe a Dataflow job

```bash
gcloud dataflow jobs describe JOB_ID \
    --region=asia-south1
```

### Cancel a Dataflow job

```bash
gcloud dataflow jobs cancel JOB_ID \
    --region=asia-south1
```

### Drain a Dataflow job

```bash
gcloud dataflow jobs drain JOB_ID \
    --region=asia-south1
```

### Run a Flex Template

```bash
gcloud dataflow flex-template run my-dataflow-job \
    --region=asia-south1 \
    --template-file-gcs-location=gs://BUCKET_NAME/template.json
```

---

# 10. Quick Reference

| Google Cloud Service | CLI Command |
|---|---|
| Cloud Storage | `gcloud storage` |
| Cloud SQL | `gcloud sql` |
| Cloud Spanner | `gcloud spanner` |
| Firestore | `gcloud firestore` |
| Bigtable | `gcloud bigtable` |
| Pub/Sub | `gcloud pubsub` |
| Dataproc | `gcloud dataproc` |
| Dataflow | `gcloud dataflow` |

---

# 11. Common Command Pattern

Most `gcloud` commands follow this general structure:

```bash
gcloud SERVICE RESOURCE ACTION [FLAGS]
```

Examples:

```bash
gcloud storage buckets list
gcloud sql instances list
gcloud spanner instances list
gcloud pubsub topics list
gcloud dataproc clusters list --region=asia-south1
gcloud dataflow jobs list --region=asia-south1
```

---

# 12. Useful Placeholder Values

Replace these placeholders with your actual Google Cloud values:

```text
PROJECT_ID
BUCKET_NAME
PASSWORD
JOB_ID
```

Example:

```bash
gcloud config set project my-gcp-project
```

```bash
gcloud storage ls gs://my-data-bucket
```
