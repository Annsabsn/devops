# 🚀 Secure Static Website Hosting Using Amazon S3 + CloudFront (OAC Method)

---

# ✅ Architecture Flow (Secure Version)

1. User enters CloudFront URL
2. Request goes to nearest **CloudFront Edge Location**
3. CloudFront checks cache
4. If not cached → forwards request to **S3 private bucket (Origin)**
5. CloudFront uses **Origin Access Control (OAC)** to access S3
6. S3 returns content to CloudFront
7. CloudFront caches and serves user

🔐 Bucket is **NOT public**

---

# 🛠️ Step-by-Step Implementation (Your Project – Correct Flow)

---

## Step 1️⃣ – Create S3 Bucket

* Go to S3 → Create bucket
* Keep **Block Public Access = ON**
* Do NOT enable public access
* Upload:

  * index.html
  * error.html
  * CSS
  * JS
  * images

### Why?

S3 is used only as **origin storage**, not for direct public access.

---

## Step 2️⃣ – Do NOT Enable Static Website Hosting (Important)

If using CloudFront + OAC:
👉 Static website hosting is NOT required.

CloudFront uses the **S3 REST endpoint**, not the website endpoint.

---

## Step 3️⃣ – Create CloudFront Distribution

CloudFront → Create Distribution

### Origin Configuration:

* Origin domain: Select S3 bucket
* Origin type: S3
* Enable **Origin Access Control (OAC)**

### Default Root Object:

```
index.html
```

### Viewer Protocol Policy:

* Redirect HTTP to HTTPS

---

## Step 4️⃣ – Allow CloudFront Access to S3

When enabling OAC:
CloudFront automatically generates bucket policy like:

```json
{
  "Effect": "Allow",
  "Principal": {
    "Service": "cloudfront.amazonaws.com"
  },
  "Action": "s3:GetObject",
  "Resource": "arn:aws:s3:::your-bucket-name/*",
  "Condition": {
    "StringEquals": {
      "AWS:SourceArn": "arn:aws:cloudfront::account-id:distribution/distribution-id"
    }
  }
}
```

### Why?

This ensures:
✔ Only this CloudFront distribution can access S3
✔ Direct S3 access is blocked

---

## Step 5️⃣ – Wait for Deployment

Status → Deploying → Enabled
Copy CloudFront domain:

```
d33ccw40kv42w2.cloudfront.net
```

---

# 🎯 Why Static Website Hosting is NOT Needed Here?

| Feature                 | With CloudFront + OAC |
| ----------------------- | --------------------- |
| Public bucket policy    | ❌ Not required        |
| Static website endpoint | ❌ Not required        |
| Secure access           | ✅ Yes                 |
| HTTPS                   | ✅ Yes                 |
| Production ready        | ✅ Yes                 |

---

# 🔥 Professional Interview Explanation

> “I implemented a secure static website hosting solution using Amazon S3 as a private origin and Amazon CloudFront as a CDN. I enabled Origin Access Control to prevent direct S3 access and configured HTTPS redirection for secure content delivery. The architecture ensures high availability, low latency, and improved security.”

---

# 🎤 Interview Questions (Basic)

---

### 1. Why didn’t you enable static website hosting?

Because CloudFront accesses S3 via REST endpoint using OAC. Static website endpoint is only required for direct S3 hosting.

---

### 2. Why keep the bucket private?

To prevent direct public access and ensure content is delivered only through CloudFront.

---

### 3. What is Origin Access Control?

It allows CloudFront to securely access private S3 buckets.

---

### 4. What is Default Root Object?

It defines which file is served when accessing root domain.

---

### 5. What happens if OAC is not configured?

CloudFront will get 403 Access Denied from S3.

---

# 🚀 Intermediate Interview Questions

---

### 6. What is the difference between OAI and OAC?

| OAI           | OAC                    |
| ------------- | ---------------------- |
| Legacy method | New recommended method |
| IAM based     | SigV4 signing          |
| Less flexible | More secure            |

---

### 7. What is TTL in CloudFront?

Time To Live — determines how long content stays cached.

---

### 8. How do you invalidate CloudFront cache?

CloudFront → Invalidations → Create
Example:

```
/*
```

---

### 9. How to implement SPA routing (React app)?

Configure custom error response:
403 → /index.html

---

### 10. What is Edge Location?

CloudFront global data centers that cache content near users.

---

# 🔥 Advanced Interview Questions

---

### 11. How does CloudFront reduce latency?

By serving cached content from nearest edge location instead of origin.

---

### 12. How does CloudFront improve availability?

If one edge fails, request routes to nearest healthy edge.

---

### 13. How would you secure it further?

* Add AWS WAF
* Enable geo restriction
* Use signed URLs
* Enable logging

---

### 14. How to restrict access to specific countries?

Use CloudFront Geo Restriction.

---

### 15. How to serve different content based on device?

Use cache behavior + Lambda@Edge or CloudFront Functions.

---

### 16. How would you optimize cost?

* Use appropriate price class
* Increase cache TTL
* Compress files
* Use HTTP/3

---

### 17. What headers affect caching?

* Cache-Control
* Authorization
* Cookies
* Query strings

---

### 18. What happens if index.html changes?

You must create invalidation to refresh cache.

---

### 19. How does HTTPS work in CloudFront?

CloudFront uses ACM certificate and handles SSL termination at edge.

---

### 20. Can CloudFront connect to multiple origins?

Yes, using multiple behaviors.

---

# 🧠 Advanced Architecture (Production Level)

Production setup would include:

User → Route 53 → CloudFront → WAF → S3 (Private)
CloudWatch → Monitoring
ACM → SSL

---

# 💼 Resume Project Description

> Designed and deployed a secure, globally distributed static website using Amazon S3 and CloudFront. Implemented Origin Access Control to restrict direct S3 access and optimized performance using CDN caching. Configured HTTPS redirection and ensured high availability architecture.

---

# 🎯 Final Outcome of Your Project

✔ Secure (Private bucket)
✔ Scalable
✔ Low latency
✔ Production ready
✔ CDN optimized
✔ HTTPS enabled

creating the s3 bucket
<img width="1905" height="716" alt="Screenshot 2026-02-18 225545" src="https://github.com/user-attachments/assets/17b0c81b-88d2-4f77-a50d-e035b07223c9" />
------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Uploaded the files
<img width="1901" height="721" alt="Screenshot 2026-02-18 225613" src="https://github.com/user-attachments/assets/3aea77a1-713f-4c96-a420-28e0e3900240" />
------------------------------------------------------------------------------------------------------------------------------------------------------------------------
created the cloudfront
<img width="1906" height="721" alt="Screenshot 2026-02-18 230006" src="https://github.com/user-attachments/assets/3de2b8e0-f986-4cd6-9e8f-09f4336fc114" />
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Output
<img width="1903" height="964" alt="Screenshot 2026-02-18 230046" src="https://github.com/user-attachments/assets/328bd8c2-247e-4ba6-b0d4-e03333949d0e" />


