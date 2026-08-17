# Firestore Database Creation Steps

## 1. Open Google Cloud Console

1. Open **Google Cloud Console**.
2. Select your **Google Cloud Project**.

---

## 2. Open Firestore

1. In the search bar, type:

```text
Firestore
```

2. Click **Firestore**.

---

## 3. Create a Firestore Database

1. Click **Create Database**.
2. Select:

```text
Firestore in Native Mode
```

3. Choose a **database location**.
4. For a demo, select a suitable region close to your users.
5. Select the **security rules**.
6. For a beginner demo, choose:

```text
Restrictive
```

7. Configure the rules later as required.
8. Click **Create Database**.

---

## 4. Create a Collection

Once the database has been created:

1. Go to **Firestore → Data**.
2. Click **Start collection**.
3. Enter a **collection name**.

Example:

```text
students
```

---

## 5. Create a Document

1. Create a new document.
2. Add the required fields.

Example:

| Field | Type | Value |
|---|---|---|
| name | string | Rahul |
| course | string | GCP Data Engineering |
| age | number | 25 |

3. Click **Save**.

---

# Simple Firestore Flow

```text
Google Cloud Console
        ↓
     Firestore
        ↓
 Create Database
        ↓
Firestore Native Mode
        ↓
   Choose Location
        ↓
   Security Rules
        ↓
    Create Database
        ↓
   Firestore → Data
        ↓
   Start Collection
        ↓
    Create Document
        ↓
      Add Fields
        ↓
        Save
```

---

# Example Structure

```text
Firestore Database
└── students
    └── document-1
        ├── name: Rahul
        ├── course: GCP Data Engineering
        └── age: 25
```
