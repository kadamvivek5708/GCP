# Dataflow Word Count Job

## 1. Create a Cloud Storage Bucket

1. Open **Google Cloud Console**.
2. Go to **Cloud Storage → Buckets**.
3. Click **Create**.
4. Enter a globally unique bucket name.
5. Select the required location and keep the required/default settings.
6. Click **Create**.

---

## 2. Create the Input File

Create a text file named:

```text
input.txt
```

Add some sample text to the file.

Example:

```text
Google Cloud Dataflow is a data processing service.
Dataflow can process data at scale.
Cloud Dataflow makes data processing easier.
```

---

## 3. Upload the Input File

1. Open your Cloud Storage bucket.
2. Go to the **Objects** tab.
3. Click **Upload files**.
4. Select:

```text
input.txt
```

5. Verify that the file has been uploaded successfully.

The input file path will be:

```text
gs://YOUR_BUCKET/input.txt
```

---

## 4. Create the Dataflow Job

1. Open **Google Cloud Console**.
2. Go to **Dataflow**.
3. Click **Create Job from Template**.
4. Select the **Word Count** template.
5. Enter a job name, for example:

```text
word-count-job
```

6. Select the required region.

---

## 5. Configure the Input File

Enter the input file path:

```text
gs://YOUR_BUCKET/input.txt
```

Replace `YOUR_BUCKET` with your actual Cloud Storage bucket name.

Example:

```text
gs://student-data-bucket/input.txt
```

---

## 6. Configure the Output Path

Enter the output path:

```text
gs://YOUR_BUCKET/output/wordcount
```

Example:

```text
gs://student-data-bucket/output/wordcount
```

---

## 7. Run the Dataflow Job

1. Review all the Dataflow settings.
2. Click **Run Job**.
3. Wait for the Dataflow job to complete.

You can monitor the job from the **Dataflow** page.

---

## 8. Check the Output

1. Go to **Cloud Storage**.
2. Open your bucket.
3. Open the output folder:

```text
output/
```

4. Open:

```text
output/wordcount
```

5. The output files will contain each word along with its count.

Example output:

```text
Cloud: 2
Dataflow: 3
Google: 1
data: 2
processing: 2
```

---

# Simple Dataflow Word Count Flow

```text
input.txt
    ↓
Cloud Storage Bucket
    ↓
Dataflow Word Count Job
    ↓
Word Count Processing
    ↓
Cloud Storage
    ↓
output/wordcount
```

---

# Resources Used

| Resource | Example |
|---|---|
| Input File | `input.txt` |
| Dataflow Job | `word-count-job` |
| Input Path | `gs://YOUR_BUCKET/input.txt` |
| Output Path | `gs://YOUR_BUCKET/output/wordcount` |
| Dataflow Template | Word Count |
