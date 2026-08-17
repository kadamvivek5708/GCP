# Pub/Sub Creation Steps

## 1. Create a Pub/Sub Topic

1. Open **Google Cloud Console**.
2. Select your **GCP project**.
3. Go to **Navigation Menu → Pub/Sub**.
4. Click **Topics**.
5. Click **Create Topic**.
6. Enter the topic name:

```text
student-topic
```

7. Keep the default settings.
8. Click **Create**.

---

## 2. Create a Subscription

1. Open the newly created topic **student-topic**.
2. Click **Create Subscription**.
3. Enter the subscription name:

```text
student-sub
```

4. Select the topic:

```text
student-topic
```

5. Keep the default settings.
6. Click **Create**.

---

## 3. Publish a Test Message

1. Open **student-topic**.
2. Go to **Messages**.
3. Click **Publish message**.
4. Enter the sample message:

```text
Student: Rahul

Course: GCP Data Engineering
```

5. Click **Publish**.

---

## 4. Pull the Message from the Subscription

1. Go to **Subscriptions**.
2. Select **student-sub**.
3. Click **Messages**.
4. Click **Pull**.
5. The published message should appear.

---

## 5. Simple Pub/Sub Flow

```text
Publisher
    ↓
  Topic
    ↓
Subscription
    ↓
 Consumer
```

### Example

```text
Publisher
    ↓
student-topic
    ↓
student-sub
    ↓
Consumer
```

---

## 6. Resources Created

| Resource | Name |
|---|---|
| Topic | `student-topic` |
| Subscription | `student-sub` |
| Sample Message | `Student: Rahul` |
| Course | `GCP Data Engineering` |
