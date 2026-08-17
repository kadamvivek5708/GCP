# Pub/Sub to Cloud Storage using Dataflow

## 1. Create a Cloud Storage Bucket

1. Open **Google Cloud Console**.
2. Go to **Cloud Storage → Buckets**.
3. Click **Create**.
4. Enter the bucket name:

```text
BUCKET_NAME
```

5. Select the required location.
6. Keep the required/default settings.
7. Click **Create**.

---

## 2. Create a Pub/Sub Topic

1. Go to **Pub/Sub → Topics**.
2. Click **Create Topic**.
3. Enter the topic name:

```text
TOPIC_NAME
```

4. Keep the required/default settings.
5. Click **Create**.

---

## 3. Create a Pub/Sub Subscription

1. Open the newly created topic.
2. Click **Create Subscription**.
3. Enter the subscription name:

```text
SUBSCRIPTION_NAME
```

4. Select the topic:

```text
TOPIC_NAME
```

5. Keep the required/default settings.
6. Click **Create**.

---

## 4. Create a Dataflow Job

1. Open **Google Cloud Console**.
2. Go to **Dataflow**.
3. Click **Create Job from Template**.
4. Select the **Pub/Sub to Cloud Storage** template.
5. Enter the Dataflow job name:

```text
DATAFLOW_JOB_NAME
```

6. Select the required region.

---

## 5. Enter the Pub/Sub Subscription

Enter the Pub/Sub subscription in the following format:

```text
projects/PROJECT_ID/subscriptions/SUBSCRIPTION_NAME
```

Example:

```text
projects/my-project/subscriptions/student-sub
```

---

## 6. Enter the Cloud Storage Output Path

Enter the Cloud Storage output path:

```text
gs://BUCKET_NAME/output/
```

Example:

```text
gs://student-data-bucket/output/
```

---

## 7. Configure Dataflow Settings

Configure the following settings as required:

- **Batch/window interval**
- **Worker settings**
- **Number of workers**
- **Machine type**
- **Maximum workers**
- Other required Dataflow options

---

## 8. Run the Dataflow Job

1. Review all the configuration settings.
2. Click **Run Job**.
3. Wait for the Dataflow job to start.

---

## 9. Publish a Test Message

1. Go to **Pub/Sub → Topics**.
2. Open the topic:

```text
TOPIC_NAME
```

3. Go to **Messages**.
4. Click **Publish message**.
5. Enter a test message, for example:

```text
Student: Rahul

Course: GCP Data Engineering
```

6. Click **Publish**.

---

## 10. Verify the Dataflow Job

1. Go to **Dataflow**.
2. Open the Dataflow job:

```text
DATAFLOW_JOB_NAME
```

3. Check the job status.
4. Verify that the message has been processed successfully.

---

## 11. Verify the Cloud Storage Output

1. Go to **Cloud Storage → Buckets**.
2. Open:

```text
BUCKET_NAME
```

3. Open the **output/** folder.
4. Verify that the output file has been created.

---

# Simple Flow

```text
Publisher
    ↓
Pub/Sub Topic
    ↓
Pub/Sub Subscription
    ↓
Dataflow
    ↓
Cloud Storage Bucket
    ↓
output/
```

---

# Resources Used

| Resource | Name |
|---|---|
| Cloud Storage Bucket | `BUCKET_NAME` |
| Pub/Sub Topic | `TOPIC_NAME` |
| Pub/Sub Subscription | `SUBSCRIPTION_NAME` |
| Dataflow Job | `DATAFLOW_JOB_NAME` |
| Output Path | `gs://BUCKET_NAME/output/` |

---

# End-to-End Example

```text
Pub/Sub Topic:
student-topic

Subscription:
student-sub

Dataflow Job:
pubsub-to-gcs-job

Cloud Storage Bucket:
student-data-bucket

Output:
gs://student-data-bucket/output/
```

## End-to-End Flow

```text
Student Message
      ↓
student-topic
      ↓
student-sub
      ↓
Dataflow
      ↓
gs://student-data-bucket/output/
```
