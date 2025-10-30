# 🌐 AWS S3 Static Website Hosting with CORS and Public Access

This project demonstrates how to host a fully functional **static website** using **Amazon S3**, configure **CORS**, and fix the common **403 Access Denied** issue when testing from another S3 bucket.

---

## 🚀 Project Overview

- Hosted using **Amazon S3 static website hosting**
- Two connected HTML pages (`index.html` & `page2.html`)
- Includes an image file (`fish.png`)
- Configured **CORS** for cross-bucket access
- Fixed **403 Forbidden error** caused by missing bucket policy
- Fully tested in **Incognito mode** for clean verification

---

## 🏗️ Tech Stack

- **AWS S3**
- **HTML5**
- **CORS Configuration**
- **Bucket Policies**
- **IAM Permissions**

---

## ⚙️ Project Setup Steps

### 1️⃣ Create Buckets

Create **two S3 buckets**:
- `mohit-html-testing` → main HTML bucket  
- `mohit-storage-testing` → image hosting bucket

Disable:
> Block all public access ✅ OFF

---

### 2️⃣ Upload Files

In **`mohit-html-testing`**, uploaded.


---

### 3️⃣ Enable Static Website Hosting

- Go to **Properties → Static website hosting**
- Enable it
- Index document: `index.html`
- Error document: `index.html`

---

### 4️⃣ Apply CORS Configuration

Add the following **CORS.json** in both buckets:

```json
[
    {
        "AllowedHeaders": ["*"],
        "AllowedMethods": ["GET", "PUT", "POST", "DELETE"],
        "AllowedOrigins": ["*"],
        "ExposeHeaders": ["ETag"]
    }
]
5️⃣ Add Bucket Policy

Use this bucket-policy.json to make objects public:

{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::mohit-html-testing/*"
        }
    ]
}


Common Issue Faced — and Solution
❌ Error:
403 Forbidden
Code: AccessDenied
Message: Access Denied
image: uploaded.

Cause:
Bucket was public, but no bucket policy was attached.

Fix:
✅ Add the above public-read bucket policy
✅ Re-upload HTML file and refresh the website endpoint

After applying the fix, the site loaded perfectly:

http://mohit-html-testing.s3-website.ap-south-1.amazonaws.com

------------------------------------------------------------

🧠 Learning Outcomes

Hosting static websites on Amazon S3

Understanding CORS (Cross-Origin Resource Sharing)

Writing and applying bucket policies

Debugging real AWS 403 Forbidden errors

Testing public website endpoints securely

## 📸 Project Screenshots

### 1️⃣ CORS Configuration
![CORS](screenshots/cors-setup.png)

### 2️⃣ Bucket Policy
![Policy](screenshots/bucket-config.png)

### 3️⃣ Static Website Hosting Enabled
![Static Hosting](screenshots/static-hosting.png)

### 4️⃣ 403 Access Denied Error (Before Fix)
![403 Error](screenshots/403-error.png)

### 5️⃣ Final Working Website
![Website Working](screenshots/website-working(finaloutput).png)


