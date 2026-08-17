# Cloud Storage Object Versioning and Lifecycle Rules — Version 4

## 1. Create a Cloud Storage Bucket

1. Open **Google Cloud Console**.
2. Go to **Cloud Storage → Buckets**.
3. Click **Create**.
4. Enter a globally unique bucket name, for example:

```text
student-version-demo-123
```

5. Under **Location type**, select:

```text
Region
```

6. Select a region, for example:

```text
asia-south1 (Mumbai)
```

7. Keep the default **Storage class → Standard**.
8. Keep the recommended access and security settings.
9. Click **Create**.

> **Note:** Bucket names are globally unique, so you may need to add numbers or other unique characters to your bucket name.

---

## 2. Enable Object Versioning

1. Open the bucket you just created.
2. Click the **Protection** tab.
3. Find **Object versioning**.
4. Click the current status to change it.
5. Select **Enable**.
6. Click **Confirm**.

### What Object Versioning Does

Once Object Versioning is enabled, when you replace or delete a live object, the previous version is retained as a **noncurrent version**.

---

## 3. Test Object Versioning

Follow these steps to test object versioning:

1. Go to the **Objects** tab.
2. Upload a file called:

```text
student.txt
```

3. Open the file and change its content.
4. Upload the modified file again using the same filename:

```text
student.txt
```

Cloud Storage will now keep both versions:

```text
Current version
    ↓
Latest student.txt

Noncurrent version
    ↓
Previous student.txt
```

You can use the **noncurrent version** to recover the previous content.

---

## 4. Create a Lifecycle Rule

Lifecycle rules automatically perform actions on objects when specified conditions are met.

1. Open your bucket.
2. Click the **Lifecycle** tab.
3. Click **Add a rule**.
4. Select the action:

```text
Delete object
```

5. Click **Continue**.
6. Under **Live state**, select:

```text
Noncurrent
```

7. Specify a condition such as:

```text
Number of newer versions = 2
```

8. Click **Continue**.
9. Review the lifecycle rule.
10. Click **Create**.

---

# Simple Flow

```text
Create Bucket
      ↓
Enable Object Versioning
      ↓
Upload student.txt
      ↓
Modify student.txt
      ↓
Upload student.txt again
      ↓
Current Version + Noncurrent Version
      ↓
Create Lifecycle Rule
      ↓
Delete old noncurrent versions
```

---

# Example Configuration

| Setting | Value |
|---|---|
| Bucket Name | `student-version-demo-123` |
| Location Type | Region |
| Region | `asia-south1 (Mumbai)` |
| Storage Class | Standard |
| Object Versioning | Enabled |
| Test Object | `student.txt` |
| Lifecycle Action | Delete object |
| Live State | Noncurrent |
| Condition | Number of newer versions = 2 |
