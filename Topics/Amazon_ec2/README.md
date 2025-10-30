# ⚙️ Amazon EC2 (Elastic Compute Cloud) — Beginner Guide

Welcome to the **Amazon EC2 Service** guide — one of the most important and widely used services in AWS.  
This document will help you understand what EC2 is, how it works, and how to launch and manage instances effectively.

---

## 🧭 What is Amazon EC2?

**Amazon EC2 (Elastic Compute Cloud)** is a web service that provides **resizable compute capacity** (virtual servers) in the AWS Cloud.  
It allows you to run applications on virtual machines called **instances** without having to invest in physical hardware.

👉 In simple words, EC2 = **Virtual Server in the Cloud**

---

## 🧱 Key Features of EC2

| Feature | Description |
|----------|-------------|
| **Elasticity** | Scale compute capacity up or down automatically |
| **Variety of Instance Types** | Choose instances based on CPU, memory, storage, or GPU needs |
| **Pay-as-you-go** | Pay only for the compute time you use |
| **Customizable** | Choose your OS, software, network, and security settings |
| **Secure** | Controlled through **Security Groups** and **Key Pairs** |
| **Integration** | Works with other AWS services (S3, RDS, CloudWatch, etc.) |

---

## 🧩 EC2 Components

| Component | Description |
|------------|--------------|
| **AMI (Amazon Machine Image)** | Template for your instance (OS + software configuration) |
| **Instance Type** | Defines the hardware configuration (CPU, RAM, Storage) |
| **Key Pair** | Used for SSH access and authentication |
| **Security Group** | Firewall rules for inbound/outbound traffic |
| **Elastic IP** | Static public IP for your instance |
| **EBS (Elastic Block Store)** | Persistent storage attached to your instance |

---

## 🪜 How to Launch an EC2 Instance

### Step 1: Open EC2 Dashboard
- Go to **AWS Management Console → EC2 → Launch Instance**

### Step 2: Choose an AMI
- Select OS: **Amazon Linux 2**, **Ubuntu**, **Windows Server**, etc.

### Step 3: Choose an Instance Type
- Example: `t2.micro` (Free Tier eligible)
- Includes 1 vCPU and 1 GB RAM

### Step 4: Configure Key Pair
- Create or select an existing key pair (`.pem` file)
- Download and keep it safe (for SSH access)

### Step 5: Configure Network Settings
- Attach a **Security Group** (allow SSH, HTTP, HTTPS)

### Step 6: Launch the Instance
- Click **Launch Instance**
- Wait a few seconds — your server is ready!

---

## 🔑 Connect to EC2 via SSH (Linux)

```
chmod 400 my-key.pem
ssh -i "my-key.pem" ec2-user@<Public-IP>
```

For Ubuntu:
```
ssh -i "my-key.pem" ubuntu@<Public-IP>
```

---

## 🌐 Access EC2 (Web Server Example)

1. Install a web server:
   ```
   sudo yum install httpd -y   # For Amazon Linux
   sudo systemctl start httpd
   sudo systemctl enable httpd
   ```

2. Add an index file:
   ```
   echo "<h1>Hello from EC2</h1>" | sudo tee /var/www/html/index.html
   ```

3. Open in browser:
   ```
   http://<EC2-Public-IP>
   ```

---

## 💰 EC2 Pricing Options

| Pricing Model | Description | Example Use |
|----------------|-------------|--------------|
| **On-Demand** | Pay per second/hour | Short-term workloads |
| **Reserved Instances** | 1–3 year commitment with discount | Steady workloads |
| **Spot Instances** | Bid for unused capacity | Cost-saving batch jobs |
| **Savings Plans** | Flexible pricing across instance families | Long-term workloads |

---

## 📊 EC2 Monitoring

You can monitor:
- CPU Utilization
- Disk I/O
- Network traffic

Using:
- **AWS CloudWatch** for metrics and alerts  
- **AWS CloudTrail** for API activity logs

---

## 🧠 Best Practices

✅ Use **Security Groups** to control access  
✅ Regularly **stop/terminate** unused instances to save cost  
✅ Always **use IAM roles** instead of embedding credentials  
✅ Create **AMI backups** for disaster recovery  
✅ Use **Elastic IPs** only when necessary  

---

## 🧩 Example: EC2 Instance via Terraform

```
resource "aws_instance" "web" {
  ami           = "ami-02d26659fd82cf299"
  instance_type = "t2.micro"
  key_name      = "my-key"
  security_groups = ["web-sg"]

  tags = {
    Name = "MyEC2Instance"
  }
}
```

---

## 🧭 EC2 Lifecycle Diagram

```
 ┌───────────┐      Start/Stop      ┌────────────┐
 │  Stopped  │  ─────────────────▶  │   Running  │
 └───────────┘  ◀─────────────────  └────────────┘
     ▲   │                           │
     │   ▼ Terminate                 ▼
 ┌────────────┐                 ┌────────────┐
 │   Pending  │                 │ Terminated │
 └────────────┘                 └────────────┘
```

---

## 📚 References

- [AWS EC2 Documentation](https://docs.aws.amazon.com/ec2/)
- [EC2 Pricing](https://aws.amazon.com/ec2/pricing/)
- [AWS Free Tier](https://aws.amazon.com/free/)

---

## 👨‍💻 Author

**Aditya Jadhav**  
Cloud & DevOps Learner  
🌐 [GitHub Profile](https://github.com/AdiJadhav1608)

---

⭐ *If you found this helpful, give it a star and keep exploring AWS!*
