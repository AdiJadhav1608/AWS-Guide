# ⚖️ AWS Load Balancer

## 🧠 Introduction

An **AWS Load Balancer** automatically distributes incoming **network traffic** across multiple targets, such as **EC2 instances, containers, or IP addresses**, in one or more **Availability Zones**.  
It improves **availability, scalability, and fault tolerance** of your applications by ensuring that no single server becomes overloaded.

Load balancing is managed through the **Elastic Load Balancing (ELB)** service in AWS.

---

## 🌍 Types of AWS Load Balancers

AWS provides **four main types** of Load Balancers under the **Elastic Load Balancing (ELB)** service:

| Load Balancer Type | Layer | Description | Best For |
|--------------------|--------|--------------|-----------|
| **Application Load Balancer (ALB)** | Layer 7 (HTTP/HTTPS) | Routes traffic based on content (URL, headers, host) | Web applications, microservices |
| **Network Load Balancer (NLB)** | Layer 4 (TCP/UDP) | Handles millions of requests with ultra-low latency | High-performance workloads |
| **Gateway Load Balancer (GWLB)** | Layer 3 | Distributes traffic to third-party virtual appliances | Firewalls, intrusion detection systems |
| **Classic Load Balancer (CLB)** | Layer 4/7 | Legacy load balancer; supports EC2-Classic | Older applications |

---

## ⚙️ Key Features

- 🔄 **Automatic Load Distribution** – Distributes incoming requests among multiple targets.  
- 🌐 **Multi-AZ Availability** – Supports high availability across multiple Availability Zones.  
- 🧩 **Health Checks** – Continuously monitors target health and routes traffic only to healthy instances.  
- 🔐 **SSL/TLS Termination** – Supports HTTPS for secure data transmission.  
- 🧠 **Intelligent Routing** – ALB supports path-based and host-based routing.  
- 📊 **Integration with CloudWatch** – Monitor metrics like latency, request count, and error rates.  
- ⚡ **Auto Scaling Integration** – Works seamlessly with EC2 Auto Scaling groups.  

---

## 🏗️ Architecture Overview

```
             ┌─────────────────────────────────────────────┐
             │           AWS Load Balancer (ELB)           │
             │---------------------------------------------│
             │   Health Checks | Routing | SSL Termination │
             └──────────────┬────────────┬────────────────┘
                            │            │
                            │            │
               ┌────────────┘            └────────────┐
               │                                      │
       ┌─────────────┐                        ┌─────────────┐
       │ EC2 Instance│                        │ EC2 Instance│
       │  (Target 1) │                        │  (Target 2) │
       └─────────────┘                        └─────────────┘
```

---

## 💡 How It Works

1️⃣ Clients send traffic to the **Load Balancer DNS name**.  
2️⃣ The Load Balancer **routes requests** to registered **healthy targets** (like EC2 instances).  
3️⃣ If a target fails a **health check**, traffic is automatically rerouted.  
4️⃣ Load Balancer scales automatically based on incoming traffic volume.  

---

## 🧩 Application Load Balancer (ALB)

- Operates at **Layer 7 (HTTP/HTTPS)**.  
- Supports:
  - **Host-based routing** (e.g., `api.example.com`, `admin.example.com`)
  - **Path-based routing** (e.g., `/login`, `/products`)
  - **Redirects** and **fixed responses**
  - **WebSocket** and **HTTP/2** support
- Best suited for **web applications** and **microservices** architectures.

### Example Use Case:
Routing requests:
```
/api/* → API servers
/images/* → Media servers
```

---

## ⚡ Network Load Balancer (NLB)

- Operates at **Layer 4 (TCP/UDP)**.  
- Designed for **ultra-high performance** and **low latency**.  
- Can handle **millions of requests per second**.  
- Supports **static IP addresses** and **elastic IPs**.  
- Best for **gaming**, **IoT**, and **real-time streaming** applications.

---

## 🧱 Gateway Load Balancer (GWLB)

- Operates at **Layer 3 (Network layer)**.  
- Integrates **third-party virtual appliances** (like firewalls, IDS, IPS).  
- Automatically scales and distributes traffic to these appliances.  
- Ideal for **network inspection** and **traffic filtering** use cases.

---

## 🧮 Classic Load Balancer (CLB)

- Legacy load balancer supporting **both HTTP and TCP** traffic.  
- Works at **Layer 4 and Layer 7** but lacks advanced routing features.  
- Use **ALB or NLB** instead for new applications.

---

## 🔧 Setup Example (Application Load Balancer)

### 1️⃣ Create Target Group
- Go to **EC2 → Target Groups → Create Target Group**
- Choose **Instances** as target type
- Specify protocol (HTTP/HTTPS) and port (e.g., 80)

### 2️⃣ Register Targets
- Add EC2 instances to the target group.

### 3️⃣ Create Load Balancer
- Go to **EC2 → Load Balancers → Create Load Balancer**
- Choose **Application Load Balancer**
- Configure:
  - Name
  - Scheme: Internet-facing
  - Listeners: HTTP (80) or HTTPS (443)
  - Availability Zones
- Attach target group.

### 4️⃣ Verify
- Copy the **Load Balancer DNS name**
- Access it in a browser to confirm it routes to your instances.

---

## 🧠 Health Checks

- Load balancer sends **periodic health checks** to targets.
- If a target fails multiple checks, it’s marked **unhealthy**.
- Parameters include:
  - **Ping path** (e.g., `/health`)
  - **Timeout**
  - **Interval**
  - **Unhealthy threshold**

---

## 📊 Monitoring Metrics (via CloudWatch)

| Metric | Description |
|---------|--------------|
| `RequestCount` | Number of requests handled |
| `HealthyHostCount` | Number of healthy targets |
| `UnHealthyHostCount` | Number of unhealthy targets |
| `TargetResponseTime` | Average time for target response |
| `HTTPCode_ELB_5XX` | Number of 5xx server errors from the load balancer |

---

## ⚖️ Advantages

✅ High availability across multiple AZs  
✅ Automatic scaling and traffic distribution  
✅ Secure and encrypted communication (HTTPS)  
✅ Intelligent routing and monitoring  
✅ Fault tolerance and reduced downtime  

---

## ⚠️ Limitations

❌ Additional cost per hour and per GB processed  
❌ Slight latency due to traffic routing layer  
❌ Classic Load Balancer is deprecated for new workloads  

---

## 💼 Common Use Cases

- Distribute web traffic across multiple **EC2 instances**  
- Host **multi-tier or microservice** applications  
- Balance **TCP/UDP** traffic for real-time services  
- Route requests based on **paths, hosts, or ports**  
- Improve **resilience and failover** for applications  

---

## 📚 References

- [Elastic Load Balancing (ELB) Documentation](https://docs.aws.amazon.com/elasticloadbalancing/)  
- [Application Load Balancer Guide](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html)  
- [Network Load Balancer Guide](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/introduction.html)  
- [Gateway Load Balancer Guide](https://docs.aws.amazon.com/elasticloadbalancing/latest/gateway/introduction.html)  
- [AWS Free Tier](https://aws.amazon.com/free/)  

---

## 👨‍💻 Author

**Aditya Jadhav**  
Cloud & DevOps Learner  
🌐 [GitHub Profile](https://github.com/AdiJadhav1608)

---

⭐ *If you found this helpful, give it a star and keep exploring AWS Networking & Load Balancing!*
