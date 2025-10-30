# 🌐 AWS Networking

## 🧠 Introduction

**AWS Networking** forms the backbone of all cloud infrastructure in **Amazon Web Services**.  
It enables communication between **resources, users, and the internet** securely and efficiently.  
At its core, AWS networking is built around the **Amazon Virtual Private Cloud (VPC)** — a logically isolated section of the AWS cloud where you can launch AWS resources.

---

## 🏗️ Core Components of AWS Networking

### 1️⃣ **Amazon VPC (Virtual Private Cloud)**
- A **logically isolated virtual network** in AWS.
- You can define your own **IP address range**, **subnets**, **route tables**, and **network gateways**.
- Provides full control over inbound and outbound network traffic.

---

### 2️⃣ **Subnets**
- **Subnets** divide a VPC’s IP address range into smaller networks.
- Each subnet resides entirely within a single **Availability Zone (AZ)**.
- Types:
  - **Public Subnet** → connected to the Internet via **Internet Gateway**
  - **Private Subnet** → internal communication only, no direct Internet access

---

### 3️⃣ **Internet Gateway (IGW)**
- A gateway that enables communication between **VPC instances and the Internet**.
- It must be **attached to a VPC** and routes public subnet traffic to the Internet.

---

### 4️⃣ **NAT Gateway / NAT Instance**
- Enables **instances in private subnets** to **access the Internet** (for updates, downloads) without exposing them publicly.
- **NAT Gateway** is managed by AWS (recommended), while **NAT Instance** is user-managed.

---

### 5️⃣ **Route Tables**
- Define **how traffic is directed** within a VPC.
- Each subnet is associated with a route table.
- Example:
  - Public route: `0.0.0.0/0 → Internet Gateway`
  - Private route: `10.0.0.0/16 → Local VPC`

---

### 6️⃣ **Security Groups**
- Virtual **firewalls for EC2 instances**.
- Control **inbound and outbound traffic** at the instance level.
- Example: Allow inbound SSH (port 22), HTTP (port 80), HTTPS (port 443).

---

### 7️⃣ **Network Access Control Lists (NACLs)**
- Act as **firewalls at the subnet level**.
- Provide **stateless filtering**, meaning inbound and outbound rules are evaluated separately.
- Can **allow or deny** specific IPs or ports.

---

### 8️⃣ **VPC Peering**
- Connects **two VPCs privately** without going over the Internet.
- Enables communication between instances in different VPCs as if they were in the same network.

---

### 9️⃣ **AWS Transit Gateway**
- A **centralized hub** to connect multiple VPCs, on-premises networks, and VPNs.
- Simplifies network architecture by reducing complex peering connections.

---

### 🔟 **Elastic IP (EIP)**
- A **static public IPv4 address** associated with your AWS account.
- You can remap it between instances to handle failures or scaling.

---

## 🌉 Additional Networking Services

| Service | Description |
|----------|--------------|
| **AWS Direct Connect** | Provides a **dedicated physical connection** from on-premises to AWS for high bandwidth and low latency. |
| **AWS PrivateLink** | Enables **private access to AWS services** without traversing the public Internet. |
| **AWS Global Accelerator** | Improves performance and availability using **AWS global network edge locations**. |
| **Amazon Route 53** | A **highly available DNS and domain management** service. |
| **AWS CloudFront** | A **Content Delivery Network (CDN)** that speeds up content delivery using edge locations. |
| **VPC Endpoints** | Allow access to AWS services **privately within VPC** using **PrivateLink**. |

---

## ⚙️ Example Architecture

```
                    +--------------------------+
                    |      Internet Gateway     |
                    +-----------+---------------+
                                |
                         [ Public Subnet ]
                                |
              +----------------+----------------+
              |                                 |
       EC2 Web Server                     NAT Gateway
              |                                 |
              +----------------+----------------+
                               |
                        [ Private Subnet ]
                               |
                        EC2 Database Server
```

---

## 🔐 Security in AWS Networking

- **Use least privilege** for security groups and NACLs.  
- **Avoid exposing SSH/RDP** to the entire Internet (`0.0.0.0/0`).  
- **Use VPN or Direct Connect** for hybrid connections.  
- **Enable VPC Flow Logs** to monitor network traffic for security and troubleshooting.  

---

## 📈 Best Practices

✅ Use **multiple Availability Zones** for high availability.  
✅ Keep **public and private resources separated** via subnets.  
✅ Use **NAT Gateway** for secure internet access from private subnets.  
✅ Apply **IAM roles** instead of storing credentials on EC2.  
✅ Enable **Flow Logs** for auditing and visibility.  

---

## 🧩 Common Use Cases

- Hosting **multi-tier web applications** (frontend + backend)  
- Connecting **on-premises data centers to AWS** via VPN or Direct Connect  
- Running **private microservices** using VPC Endpoints  
- Serving global users using **CloudFront + Route 53**  

---

## 📚 References

- [AWS VPC Documentation](https://docs.aws.amazon.com/vpc/)  
- [AWS Networking Overview](https://aws.amazon.com/what-is/cloud-networking/)  
- [Amazon Route 53 Documentation](https://docs.aws.amazon.com/Route53/)  
- [AWS Direct Connect](https://aws.amazon.com/directconnect/)  
- [AWS CloudFront](https://aws.amazon.com/cloudfront/)  

---

## 👨‍💻 Author

**Aditya Jadhav**  
Cloud & DevOps Learner  
🌐 [GitHub Profile](https://github.com/AdiJadhav1608)

---

⭐ *If you found this helpful, give it a star and keep exploring AWS Networking!*
