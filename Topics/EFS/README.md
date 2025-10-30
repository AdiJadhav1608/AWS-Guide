# ☁️ Amazon Elastic File System (EFS)

## 🧠 Introduction

**Amazon EFS (Elastic File System)** is a **fully managed, scalable, cloud-based file storage service** offered by AWS.  
It provides **shared file storage** that can automatically scale up or down as files are added or removed — with **no need for manual provisioning**.

---

## ⚙️ Key Features

- **Fully Managed**: AWS automatically handles provisioning, scaling, and maintenance.  
- **Scalable**: Automatically scales from gigabytes to petabytes.  
- **Elastic**: Grows and shrinks as data changes — pay only for what you use.  
- **Highly Available**: Data is stored across multiple Availability Zones (AZs).  
- **Secure**: Integrated with AWS IAM, Security Groups, and KMS encryption.  
- **Shared Access**: Multiple EC2 instances can access the same file system concurrently.  

---

## 🏗️ Architecture

EFS works as a **shared network file system** for your AWS instances.

```
        ┌────────────────────────┐
        │   Amazon EFS FileSystem│
        └────────────┬───────────┘
                     │
       ┌─────────────┴─────────────┐
       │                           │
┌────────────┐             ┌────────────┐
│ EC2 Instance│             │ EC2 Instance│
└────────────┘             └────────────┘
       │                           │
       └──── Shared Mount Point ───┘
```

---

## 🔧 Setup Steps

### 1️⃣ **Create EFS File System**
- Go to **AWS Console → EFS → Create File System**
- Choose **VPC, Availability Zones, and Security Groups**
- Enable **encryption** (recommended)

### 2️⃣ **Configure Security Groups**
- Allow inbound NFS (port 2049) between your EC2 instances and EFS.

### 3️⃣ **Mount EFS on EC2**
```
# Install NFS utilities
sudo yum install -y amazon-efs-utils

# Create mount directory
sudo mkdir /mnt/efs

# Mount using EFS mount helper
sudo mount -t efs fs-xxxxxx:/ /mnt/efs

# Verify
df -h
```

### 4️⃣ **Optional: Add to /etc/fstab for Auto Mount**
```
fs-xxxxxx:/ /mnt/efs efs defaults,_netdev 0 0
```

---

## 🧩 Use Cases

- Shared storage for **web servers** (e.g., WordPress)
- Centralized **data storage** for analytics and ML workloads
- Persistent storage for **containers** in ECS or EKS
- Backup and archive solutions  

---

## 🧮 EFS vs EBS vs S3

| Feature        | **EFS** (File Storage) | **EBS** (Block Storage) | **S3** (Object Storage) |
|----------------|------------------------|--------------------------|--------------------------|
| Access Type    | Shared (multi-instance) | Single-instance          | API-based               |
| Scalability    | Auto, Elastic           | Fixed size (resize manually) | Virtually unlimited     |
| Use Case       | Web servers, data sharing | Databases, OS disks       | Backups, media, archives |
| Protocol       | NFS                     | Block                    | HTTP/HTTPS              |

---

## ⚖️ Advantages

✅ Fully managed and scalable  
✅ Multi-AZ high availability  
✅ Concurrent access from many EC2 instances  
✅ Integration with IAM, CloudWatch, and KMS  

---

## ⚠️ Limitations

❌ Higher latency compared to EBS  
❌ Costlier for small workloads  
❌ Limited to NFS-compatible clients  

---

## 📚 References

- [Amazon EFS Documentation](https://docs.aws.amazon.com/efs/)  
- [EFS Pricing](https://aws.amazon.com/efs/pricing/)  
- [AWS Free Tier](https://aws.amazon.com/free/)  
- [EFS User Guide](https://docs.aws.amazon.com/efs/latest/ug/whatisefs.html)

---

## 👨‍💻 Author

**Aditya Jadhav**  
Cloud & DevOps Learner  
🌐 [GitHub Profile](https://github.com/AdiJadhav1608)

---

⭐ *If you found this helpful, give it a star and keep exploring AWS!*
