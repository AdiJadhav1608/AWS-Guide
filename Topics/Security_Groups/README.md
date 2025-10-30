# 🔒 AWS Security Groups

Welcome to the **AWS Security Groups** guide — a key concept in AWS networking and instance-level security.  
This guide will help you understand what Security Groups are, how they work, and how to configure them properly for secure access to your AWS resources.

---

## 🧭 What is a Security Group?

A **Security Group (SG)** in AWS acts as a **virtual firewall** that controls **inbound and outbound traffic** to your AWS resources, such as **EC2 instances**, **RDS databases**, or **Load Balancers**.

It defines which type of traffic is **allowed to enter or leave** your instances based on **rules** you specify.

> 🧠 Think of it like a “door guard” for your instance — only traffic matching your rules can pass through.

---

## ⚙️ Key Features

| Feature | Description |
|----------|--------------|
| **Stateful** | Responses to allowed traffic are automatically allowed (no need for separate outbound rules). |
| **Instance-Level** | Applied directly to instances, not subnets. |
| **Allow Rules Only** | You can **allow** traffic, but not explicitly **deny** it. |
| **Multiple Groups** | You can attach multiple Security Groups to a single instance. |
| **Default Group** | Each VPC has a default Security Group that allows traffic between instances using it. |

---

## 🔁 Inbound vs Outbound Rules

| Rule Type | Direction | Description | Example |
|------------|------------|--------------|----------|
| **Inbound** | Incoming traffic | Controls traffic **coming into** your instance | Allow HTTP (port 80) or SSH (port 22) |
| **Outbound** | Outgoing traffic | Controls traffic **leaving** your instance | Allow all outbound traffic (default) |

---

## 🧱 Common Protocols and Ports

| Protocol | Port | Description |
|-----------|------|--------------|
| **SSH** | 22 | Secure shell access to Linux EC2 |
| **RDP** | 3389 | Remote desktop access to Windows EC2 |
| **HTTP** | 80 | Web traffic (non-secure) |
| **HTTPS** | 443 | Secure web traffic |
| **Custom TCP/UDP** | Any | For application-specific traffic |

---

## 🧩 Example: EC2 Security Group Setup

### ✅ Scenario:
You are launching an EC2 instance to host a website.

### Steps:
1. Open the **EC2 Console → Security Groups → Create Security Group**
2. Name: `web-server-sg`
3. Description: “Allow web and SSH access”
4. Add inbound rules:
   - **Type:** HTTP | **Port:** 80 | **Source:** 0.0.0.0/0  
   - **Type:** HTTPS | **Port:** 443 | **Source:** 0.0.0.0/0  
   - **Type:** SSH | **Port:** 22 | **Source:** *Your IP only* (for security)
5. Add outbound rule:
   - **Type:** All traffic | **Destination:** 0.0.0.0/0  
6. Attach this Security Group to your EC2 instance when launching.

---

## 🛡️ Best Practices

✅ **Limit SSH/RDP Access:** Always restrict to your IP instead of 0.0.0.0/0  
✅ **Use HTTPS:** Encrypt your web traffic with SSL/TLS  
✅ **Least Privilege Principle:** Open only required ports  
✅ **Separate Security Groups:** Use different SGs for different layers (web, app, DB)  
✅ **Regular Review:** Periodically check for unnecessary open ports  

---

## 🧩 Security Groups vs Network ACLs

| Feature | Security Groups | Network ACLs |
|----------|------------------|--------------|
| Level | Instance level | Subnet level |
| Stateful | ✅ Yes | ❌ No |
| Rules | Allow only | Allow + Deny |
| Default | Allows all outbound | Allows all inbound & outbound |
| Use Case | Control instance access | Control subnet access |

---

## 🧭 Visualization

```
          ┌───────────────────────────┐
          │       Internet            │
          └──────────┬────────────────┘
                     │
             [ Security Group ]
                     │
           ┌─────────┴──────────┐
           │ EC2 Instance (Web) │
           └────────────────────┘
```

---

## 📚 References

- [AWS Security Groups Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html)
- [AWS Best Practices for Security](https://aws.amazon.com/architecture/security-identity-compliance/)
- [AWS CLI Commands Reference](https://docs.aws.amazon.com/cli/latest/reference/ec2/)

---

## 👨‍💻 Author

**Aditya Jadhav**  
Cloud & DevOps Learner  
🌐 [GitHub Profile](https://github.com/AdiJadhav1608)

---

⭐ *If you found this helpful, give it a star and keep learning AWS securely!*
