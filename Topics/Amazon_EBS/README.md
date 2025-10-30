# 🧠 Amazon EBS (Elastic Block Store)

## 📘 Introduction
Amazon **Elastic Block Store (EBS)** is a **block-level storage service** designed for use with Amazon EC2 instances.  
It provides **persistent storage volumes** that can be attached to EC2 instances to store data like files, databases, or application logs.

---

## ⚙️ Key Features
- 💾 **Persistent Storage:** Data remains even after EC2 instance termination (if volume is not deleted).
- 🔄 **Elasticity:** Easily increase or decrease volume size and change type without downtime.
- ⚡ **High Performance:** Supports SSD and HDD volume types optimized for different workloads.
- 🛡️ **Durability:** Automatically replicated within an Availability Zone (AZ) to prevent data loss.
- 🧩 **Snapshots:** You can create point-in-time backups (snapshots) stored in Amazon S3.

---

## 🧱 EBS Volume Types
| Type | Description | Best For |
|------|--------------|----------|
| gp3 / gp2 | SSD-based | General purpose workloads |
| io2 / io1 | SSD-based | High-performance databases |
| st1 | HDD-based | Throughput-intensive workloads |
| sc1 | HDD-based | Low-cost, infrequent access data |

---

## 🔧 Common Use Cases
- Hosting file systems and databases  
- Running enterprise applications requiring low-latency storage  
- Backup and recovery using EBS snapshots  
- Supporting containerized workloads (e.g., Docker on EC2)

---

## 🧭 How It Works
1. Create an **EBS volume** in the same Availability Zone as your EC2 instance.  
2. **Attach** the volume to the instance.  
3. **Mount** it to the file system.  
4. Use it like a regular hard drive for storing and retrieving data.  
5. Optionally, **create snapshots** for backup or replication.

---

## 💡 Best Practices
- Enable **EBS encryption** for sensitive data.  
- Regularly take **snapshots** for disaster recovery.  
- Detach EBS volumes properly before deleting EC2 instances.  
- Monitor EBS performance metrics using **Amazon CloudWatch**.  
- Use **EBS-optimized instances** for improved I/O performance.  
- Tag EBS volumes properly for better resource management and cost tracking.  

---

## 🖥️ Example
```bash
# Create a new EBS volume (via AWS CLI)
aws ec2 create-volume \
  --availability-zone ap-south-1a \
  --size 10 \
  --volume-type gp3

# Attach it to an EC2 instance
aws ec2 attach-volume \
  --volume-id vol-0abc123def456ghi7 \
  --instance-id i-0a1b2c3d4e5f6g7h8 \
  --device /dev/sdf
```

---

## 🧩 Conclusion
Amazon EBS is an essential storage component for EC2, offering **scalable, high-performance, and durable block storage**.  
It provides the flexibility to adapt to changing storage needs while ensuring data persistence and reliability.

---

## 📚 References

- [Amazon EBS Documentation](https://docs.aws.amazon.com/ebs/)  
- [EBS Volume Types](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html)  
- [Amazon EBS Snapshots](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-creating-snapshot.html)  
- [EBS Pricing](https://aws.amazon.com/ebs/pricing/)  
- [AWS Free Tier](https://aws.amazon.com/free/)

---

## 👨‍💻 Author

**Aditya Jadhav**  
Cloud & DevOps Learner  
🌐 [GitHub Profile](https://github.com/AdiJadhav1608)

---

⭐ *If you found this helpful, give it a star and keep exploring AWS!*
