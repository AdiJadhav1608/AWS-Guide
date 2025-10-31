# 🚀 AWS CloudFront (Content Delivery Network)

## 📘 Introduction
**Amazon CloudFront** is a **Content Delivery Network (CDN)** service that securely delivers data, videos, applications, and APIs to users globally with **low latency** and **high transfer speeds**.

It uses a network of **edge locations** distributed around the world to cache and serve content closer to the users, improving website and application performance.

---

## 🎯 Key Features

| Feature | Description |
|----------|--------------|
| **Global Edge Network** | Uses AWS edge locations worldwide for fast content delivery. |
| **Caching** | Stores frequently accessed content near users to reduce latency. |
| **Integration** | Works with AWS S3, EC2, Elastic Load Balancer, and Route 53. |
| **Security** | Integrated with AWS Shield, WAF, and SSL/TLS for DDoS protection and encryption. |
| **Customizable** | Supports dynamic content, Lambda@Edge, and custom error pages. |
| **Real-time Metrics** | Provides detailed monitoring through Amazon CloudWatch. |

---

## 🧩 Core Components

| Component | Description |
|------------|--------------|
| **Distribution** | The main CloudFront configuration that defines how and where content is delivered. |
| **Origin** | The location of your content (e.g., S3 bucket, EC2 instance, ALB, or on-prem server). |
| **Edge Location** | AWS data centers that cache content close to users. |
| **Cache Behavior** | Rules that control how CloudFront responds to requests (e.g., caching duration, headers). |
| **Invalidation** | Mechanism to remove cached content before its expiration. |
| **Viewer Protocol Policy** | Defines HTTP/HTTPS behavior for viewer connections. |

---

## ⚙️ How CloudFront Works

```
[ User Request ]
       ↓
[ Nearest Edge Location ]
       ↓
[ Cache Hit → Serve Content ]
[ Cache Miss → Fetch from Origin ]
       ↓
[ Response Cached and Sent Back to User ]
```

1. The user requests content (like an image or web page).  
2. CloudFront routes the request to the nearest **edge location**.  
3. If cached, content is served immediately. Otherwise, CloudFront fetches it from the **origin server**.  
4. The content is cached at the edge for future requests.

---

## 🧱 Types of Content Delivered

| Type | Example |
|-------|----------|
| **Static Content** | HTML, CSS, JS, images, videos. |
| **Dynamic Content** | Personalized or API-driven responses. |
| **Streaming Media** | Live or on-demand video streaming. |
| **Software Downloads** | Games, patches, updates. |

---

## 🧰 Common Use Cases

- 🌎 **Website Acceleration** — Faster load times for websites and web apps.  
- 🎬 **Video Streaming** — Deliver videos on demand or live.  
- 🧾 **API Acceleration** — Distribute APIs closer to users.  
- 🔒 **Security** — Encrypted connections and DDoS protection.  
- 💡 **Cost Optimization** — Reduced data transfer from origins due to caching.  

---

## 🧩 CloudFront Integration with AWS Services

| Service | Integration |
|----------|--------------|
| **S3** | Deliver static websites or media files directly from S3 using CloudFront. |
| **EC2 / ALB** | Deliver dynamic content through instances or load balancers. |
| **Route 53** | Use DNS routing to connect your domain to the CloudFront distribution. |
| **AWS WAF** | Protect your applications from common web exploits. |
| **AWS Shield** | Defend against DDoS attacks. |
| **CloudWatch** | Monitor performance metrics and logs. |
| **Lambda@Edge** | Customize content delivery logic closer to users. |

---

## 🧩 Creating a CloudFront Distribution

### 🪶 Step 1: Create a Distribution via AWS Console or CLI

#### AWS CLI Example
```bash
aws cloudfront create-distribution \
  --origin-domain-name mybucket.s3.amazonaws.com \
  --default-root-object index.html
```

---

### 🪶 Step 2: Configure Cache Behavior
- Set cache duration (TTL)
- Choose allowed HTTP methods
- Configure viewer protocol policy (Redirect HTTP to HTTPS)

---

### 🪶 Step 3: Associate SSL Certificate
- Use **AWS Certificate Manager (ACM)** for custom domain SSL.
- Attach the certificate to your CloudFront distribution.

---

### 🪶 Step 4: Connect with Route 53
- Create an **Alias record** in Route 53 pointing to the CloudFront domain.

```bash
aws route53 change-resource-record-sets \
  --hosted-zone-id Z123456ABCDEFG \
  --change-batch file://alias.json
```

**alias.json**
```json
{
  "Changes": [
    {
      "Action": "CREATE",
      "ResourceRecordSet": {
        "Name": "cdn.example.com",
        "Type": "A",
        "AliasTarget": {
          "HostedZoneId": "Z2FDTNDATAQYW2",
          "DNSName": "d123abcd.cloudfront.net",
          "EvaluateTargetHealth": false
        }
      }
    }
  ]
}
```

---

## 🧱 Caching and Invalidation

| Action | Description |
|----------|--------------|
| **Cache Duration (TTL)** | Control how long content stays cached at edge locations. |
| **Invalidation** | Remove outdated or incorrect cached files manually. |
| **Cache Control Headers** | Define caching behavior directly from origin headers. |

### Example: Invalidate Cached Content
```bash
aws cloudfront create-invalidation \
  --distribution-id E123456ABCDEFG \
  --paths "/index.html" "/images/*"
```

---

## 🔐 Security Features

| Feature | Description |
|----------|--------------|
| **HTTPS Support** | Encrypt content between viewers and CloudFront. |
| **AWS WAF Integration** | Protect against SQL injection, XSS, and more. |
| **Access Control** | Use signed URLs and cookies for restricted content. |
| **Geo Restriction** | Allow or block content delivery by country. |
| **Origin Access Identity (OAI)** | Restrict S3 access to only CloudFront. |
| **Field-Level Encryption** | Encrypt sensitive data before it reaches your servers. |

---

## 🧠 Performance Optimization

| Technique | Benefit |
|------------|----------|
| **Cache Key Customization** | Fine-tune how CloudFront caches data. |
| **Compression** | Enable GZIP/Brotli to reduce file sizes. |
| **HTTP/3 Support** | Faster and more secure data delivery. |
| **Lambda@Edge** | Customize requests/responses at the edge. |
| **Origin Groups** | Configure primary and backup origins for failover. |

---

## 💰 Pricing Overview

| Component | Description | Cost |
|------------|--------------|------|
| **Data Transfer Out** | Based on region and volume | Starts at $0.085/GB |
| **HTTP/HTTPS Requests** | Per 10,000 requests | ~$0.0075 |
| **Invalidation Requests** | First 1,000 paths/month free | Then $0.005 per path |
| **Field-Level Encryption** | Per 10,000 requests | ~$0.02 |
| **AWS Shield Standard** | Included | Free |

✅ **Free Tier:** 1 TB of data transfer out per month for one year.

---

## 🧾 CloudFront CLI Commands Cheat Sheet

| Task | Command |
|------|----------|
| List distributions | `aws cloudfront list-distributions` |
| Get distribution details | `aws cloudfront get-distribution --id <ID>` |
| Create invalidation | `aws cloudfront create-invalidation --distribution-id <ID> --paths "/*"` |
| Delete distribution | `aws cloudfront delete-distribution --id <ID>` |
| Enable distribution | `aws cloudfront update-distribution --id <ID> --if-match <ETag> --distribution-config file://config.json` |

---

## 🧠 Example Architecture

```
[ Users ]
   ↓
[ CloudFront Edge Location (Cache) ]
   ↓
[ S3 Bucket / EC2 / ALB (Origin) ]
   ↓
[ Application / Website / API ]
```

**Scenario:**
- CloudFront caches static files (HTML, images) from an S3 bucket.
- Dynamic requests are forwarded to an ALB connected to EC2 instances.
- Route 53 routes domain traffic to the CloudFront distribution.

---

## 🧰 Best Practices

- Enable **compression (GZIP/Brotli)** for faster data transfer.  
- Use **Origin Access Identity (OAI)** to secure S3 origins.  
- Configure **HTTPS-only** viewer connections.  
- Set **low TTL** for frequently changing content.  
- Monitor performance with **CloudWatch metrics**.  
- Use **Lambda@Edge** for content personalization and redirection.  
- Invalidate caches after website updates.  

---

## 🧩 Troubleshooting

| Issue | Possible Cause | Solution |
|--------|----------------|-----------|
| Content not updating | Cache not invalidated | Run invalidation command or lower TTL. |
| SSL errors | Certificate not valid for domain | Reissue ACM certificate with correct domain. |
| Slow performance | Poor cache hit ratio | Adjust cache behavior or add more origins. |
| Access denied | No OAI configured for S3 | Add OAI to allow CloudFront access. |

---

## 📊 CloudWatch Metrics

| Metric | Description |
|--------|--------------|
| **Requests** | Number of requests handled. |
| **BytesDownloaded/Uploaded** | Total data transfer. |
| **4xx/5xx Error Rate** | Percentage of client/server errors. |
| **CacheHitRate** | Ratio of cache hits to total requests. |
| **TotalErrorRate** | Overall percentage of errors. |

---

## 🧠 Summary

| Key Point | Description |
|------------|--------------|
| **Service Type** | Content Delivery Network (CDN) |
| **Main Use** | Fast, secure delivery of web content |
| **Global Reach** | 600+ Edge Locations in 100+ cities |
| **Integration** | Works seamlessly with S3, EC2, ALB, Route 53 |
| **Security** | Built-in DDoS protection with AWS Shield |
| **Customization** | Supports Lambda@Edge and signed URLs |

---

## 📚 References

- [AWS CloudFront Documentation](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html)  
- [AWS CloudFront Pricing](https://aws.amazon.com/cloudfront/pricing/)  
- [Lambda@Edge Overview](https://aws.amazon.com/lambda/edge/)  
- [CloudFront Security Best Practices](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/best-practices.html)

---

## 👨‍💻 Author
**Aditya Jadhav**  
Cloud & DevOps Learner  
🌐 [GitHub Profile](https://github.com/AdiJadhav1608)

---

⭐ *If you found this helpful, give it a star and explore more AWS Networking & Delivery Services!*

