# 🏗️ Amazon VPC (Virtual Private Cloud)

## 🧠 Introduction

**Amazon Virtual Private Cloud (VPC)** is a **logically isolated network** within the AWS cloud where you can launch and manage your AWS resources securely.  
It gives you **complete control** over your virtual networking environment — including **IP address ranges**, **subnets**, **route tables**, **internet connectivity**, and **security settings**.

Essentially, VPC is the **foundation of all AWS networking** — it allows you to design and control your network layout just like a traditional data center but in the **cloud**.

---

## ⚙️ Key Features

- 🔒 **Isolation** — Each VPC is isolated from other VPCs and AWS accounts.  
- 🌍 **Custom IP Ranges** — Define your own IPv4 and IPv6 address ranges using **CIDR blocks**.  
- 🧩 **Subnets** — Create **public** and **private** subnets for resource segmentation.  
- 🚪 **Gateways** — Use **Internet Gateway**, **NAT Gateway**, or **VPN Gateway** for traffic control.  
- 📡 **Security Layers** — Protect your instances using **Security Groups** and **Network ACLs**.  
- 🔄 **VPC Peering & Transit Gateway** — Connect multiple VPCs or hybrid environments seamlessly.  
- 🧮 **Flow Logs** — Monitor and capture network traffic for security and debugging.

---

## 🏗️ Architecture Overview

```
               ┌────────────────────────────────────┐
               │          Amazon VPC (10.0.0.0/16)  │
               │                                    │
               │   ┌──────────────┐   ┌──────────────┐
               │   │ Public Subnet│   │ Private Subnet│
               │   │ (10.0.1.0/24)│   │ (10.0.2.0/24)│
               │   └──────┬───────┘   └──────┬───────┘
               │          │                  │
          ┌────┴────┐     │             ┌────┴────┐
          │Internet │     │             │ NAT     │
          │Gateway  │     │             │Gateway  │
          └────┬────┘     │             └────┬────┘
               │          │                  │
          ┌────┴────┐  ┌──┴──┐           ┌───┴───┐
          │  EC2    │  │Route│           │  EC2  │
          │ (Public)│  │Table│           │Private │
          └─────────┘  └─────┘           └────────┘
```

---

## 🧩 Components of a VPC

### 1️⃣ **CIDR Block**
- Defines the **IP address range** for your VPC (e.g., `10.0.0.0/16`).
- You can have **multiple subnets** within this range.

---

### 2️⃣ **Subnets**
- Logical divisions of the VPC CIDR block.
- Each subnet resides in **one Availability Zone**.
- Types:
  - **Public Subnet** → connected to an Internet Gateway.
  - **Private Subnet** → internal-only communication.

---

### 3️⃣ **Route Tables**
- Define how traffic is directed inside and outside the VPC.
- Each subnet must be associated with one route table.
- Example Routes:
  - Local: `10.0.0.0/16 → local`
  - Public: `0.0.0.0/0 → Internet Gateway`
  - Private: `0.0.0.0/0 → NAT Gateway`

---

### 4️⃣ **Internet Gateway (IGW)**
- Allows communication between **VPC resources** and the **public Internet**.
- Must be attached to your VPC and referenced in the route table.

---

### 5️⃣ **NAT Gateway**
- Allows **private subnet instances** to access the Internet securely without exposing themselves publicly.

---

### 6️⃣ **Security Groups**
- Act as **stateful firewalls** controlling inbound and outbound traffic at the **instance level**.
- Example rule: Allow inbound SSH (port 22) from a specific IP range.

---

### 7️⃣ **Network ACLs (NACLs)**
- Provide **stateless filtering** at the subnet level.
- Can **allow or deny** traffic based on IPs, ports, or protocols.

---

### 8️⃣ **VPC Peering**
- Connects **two VPCs privately** using AWS backbone network — no Internet exposure.

---

### 9️⃣ **VPC Endpoints**
- Enable **private connectivity** to AWS services (like S3, DynamoDB) **without using the Internet**.

---

### 🔟 **Elastic IP**
- Static public IPv4 address that you can associate with EC2 instances for Internet communication.

---

## 🔧 Example: Creating a VPC using AWS CLI

```
# 1. Create VPC
aws ec2 create-vpc --cidr-block 10.0.0.0/16

# 2. Create Subnets
aws ec2 create-subnet --vpc-id vpc-xxxxxx --cidr-block 10.0.1.0/24
aws ec2 create-subnet --vpc-id vpc-xxxxxx --cidr-block 10.0.2.0/24

# 3. Create Internet Gateway
aws ec2 create-internet-gateway

# 4. Attach IGW to VPC
aws ec2 attach-internet-gateway --vpc-id vpc-xxxxxx --internet-gateway-id igw-xxxxxx

# 5. Create Route Table
aws ec2 create-route-table --vpc-id vpc-xxxxxx

# 6. Add Route to Internet Gateway
aws ec2 create-route --route-table-id rtb-xxxxxx --destination-cidr-block 0.0.0.0/0 --gateway-id igw-xxxxxx
```

---

## 💡 Use Cases

- Hosting **multi-tier web applications** (frontend + backend).  
- Creating **secure environments** for databases or internal services.  
- Building **hybrid architectures** with **VPN or Direct Connect**.  
- Running **isolated workloads** for testing or compliance.  

---

## ⚖️ Advantages

✅ Full control over networking setup  
✅ Secure and isolated environment  
✅ Flexible — supports both IPv4 and IPv6  
✅ Integration with all major AWS services  
✅ Scalable and customizable  

---

## ⚠️ Limitations

❌ Initial setup may be complex for beginners  
❌ Requires correct route/security configuration  
❌ Costs can increase with multiple NAT/Transit Gateways  

---

## 📈 Best Practices

- 🧱 Keep **public and private subnets separate**  
- 🔐 Use **Security Groups** for instance-level control and **NACLs** for subnet-level rules  
- 🌍 Restrict **SSH/RDP** access to trusted IPs only  
- 📊 Enable **VPC Flow Logs** for monitoring and auditing  
- 🧮 Plan **CIDR blocks** to avoid overlapping networks in peering setups  

---

## 📚 References

- [Amazon VPC Documentation](https://docs.aws.amazon.com/vpc/)  
- [VPC Best Practices](https://aws.amazon.com/answers/networking/aws-single-vpc-design/)  
- [AWS Networking Overview](https://aws.amazon.com/what-is/cloud-networking/)  
- [VPC Pricing](https://aws.amazon.com/vpc/pricing/)  

---

## 👨‍💻 Author

**Aditya Jadhav**  
Cloud & DevOps Learner  
🌐 [GitHub Profile](https://github.com/AdiJadhav1608)

---

⭐ *If you found this helpful, give it a star and keep exploring AWS Networking!*
