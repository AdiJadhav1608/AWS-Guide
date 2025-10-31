# ☁️ AWS CloudWatch

## 📘 Introduction
**Amazon CloudWatch** is a **monitoring and observability service** built for **DevOps engineers, developers, site reliability engineers (SREs), and IT managers**.  
It provides data and actionable insights to monitor your **applications, respond to system-wide performance changes**, and **optimize resource utilization**.

With CloudWatch, you can **collect metrics**, **monitor logs**, **set alarms**, and **automate responses** across your AWS environment.

---

## 🎯 Key Features
| Feature | Description |
|----------|--------------|
| **Metrics Monitoring** | Tracks resource and application performance in real time. |
| **Alarms** | Automatically trigger actions (like scaling or notifications) based on metrics. |
| **Logs Management** | Centralized collection, monitoring, and analysis of logs. |
| **Dashboards** | Visualize metrics and logs using customizable dashboards. |
| **Events** | Detect and respond to changes in AWS resources automatically. |
| **Anomaly Detection** | Uses machine learning to detect unusual behavior in metrics. |

---

## 🧠 Components of CloudWatch

### 1. **Metrics**
- Fundamental monitoring data representing time-ordered sets of data points.
- Examples:
  - `CPUUtilization`
  - `NetworkIn` / `NetworkOut`
  - `DiskReadOps`, `DiskWriteOps`

### 2. **Alarms**
- Monitor metrics and automatically **initiate actions**.
- Example: Send SNS notification or trigger Auto Scaling.

### 3. **Logs**
- Collect, store, and analyze log data from AWS resources.
- Can stream application logs to CloudWatch Logs for debugging and auditing.

### 4. **Events (Now called EventBridge)**
- Responds automatically to AWS resource changes (e.g., EC2 instance state change).

### 5. **Dashboards**
- Visual interface to display selected metrics and alarms for real-time insights.

---

## ⚙️ How CloudWatch Works

```
[ AWS Resources ] 
        ↓
[ CloudWatch Metrics & Logs ]
        ↓
[ CloudWatch Alarms / Events ]
        ↓
[ Notifications / Auto Scaling / Actions ]
```

- AWS services automatically send metrics to CloudWatch.  
- You can publish **custom metrics** from your own applications.  
- CloudWatch evaluates metrics using **alarms** and **rules**, then performs actions such as:
  - Sending SNS notifications
  - Triggering Lambda functions
  - Starting/stopping EC2 instances

---

## 🧩 Commonly Monitored AWS Services

| Service | Example Metrics |
|----------|----------------|
| **EC2** | CPUUtilization, NetworkIn/Out, DiskReadOps |
| **RDS** | DatabaseConnections, FreeStorageSpace |
| **S3** | NumberOfObjects, BucketSizeBytes |
| **Lambda** | Invocations, Errors, Duration |
| **EBS** | VolumeReadOps, VolumeWriteOps |
| **ELB/ALB** | RequestCount, HealthyHostCount |

---

## 🧰 Getting Started with CloudWatch

### Step 1️⃣: View Default Metrics
```
aws cloudwatch list-metrics
```

### Step 2️⃣: Get Metric Statistics
```
aws cloudwatch get-metric-statistics \
--metric-name CPUUtilization \
--namespace AWS/EC2 \
--statistics Average \
--dimensions Name=InstanceId,Value=i-0abcd1234ef56789 \
--start-time 2024-11-01T00:00:00Z \
--end-time 2024-11-01T23:59:00Z \
--period 300
```

### Step 3️⃣: Create an Alarm
```
aws cloudwatch put-metric-alarm \
--alarm-name "HighCPUUtilization" \
--metric-name CPUUtilization \
--namespace AWS/EC2 \
--statistic Average \
--period 300 \
--threshold 70 \
--comparison-operator GreaterThanThreshold \
--dimensions Name=InstanceId,Value=i-0abcd1234ef56789 \
--evaluation-periods 2 \
--alarm-actions arn:aws:sns:ap-south-1:123456789012:NotifyMe \
--treat-missing-data notBreaching
```

---

## 🧱 CloudWatch Dashboards
You can create **custom dashboards** for visualization.

### Example:
```
aws cloudwatch put-dashboard \
--dashboard-name MyDashboard \
--dashboard-body file://dashboard.json
```

**dashboard.json:**
```
{
  "widgets": [
    {
      "type": "metric",
      "x": 0,
      "y": 0,
      "width": 12,
      "height": 6,
      "properties": {
        "metrics": [
          ["AWS/EC2", "CPUUtilization", "InstanceId", "i-0abcd1234ef56789"]
        ],
        "period": 300,
        "stat": "Average",
        "region": "ap-south-1",
        "title": "EC2 Instance CPU Utilization"
      }
    }
  ]
}
```

---

## 📜 CloudWatch Logs
CloudWatch Logs allows you to monitor, store, and access your application logs.

### Common Commands:
```
aws logs create-log-group --log-group-name MyAppLogs
aws logs create-log-stream --log-group-name MyAppLogs --log-stream-name AppStream
aws logs put-log-events --log-group-name MyAppLogs --log-stream-name AppStream \
--log-events file://logevents.json
```

Example `logevents.json`:
```
[
  { "timestamp": 1730074800000, "message": "Application started" },
  { "timestamp": 1730074860000, "message": "Processing request" }
]
```

---

## ⚡ CloudWatch Alarms and SNS Integration
You can integrate alarms with **Amazon SNS (Simple Notification Service)** to receive alerts via **email, SMS, or Lambda**.

**Steps:**
1. Create an SNS topic  
2. Subscribe to it (email, SMS, or Lambda)  
3. Link the topic ARN in your CloudWatch alarm  

---

## 🧠 CloudWatch Logs Insights
A powerful **query engine** for log analysis.

### Example Query:
```
fields @timestamp, @message
| filter @message like /ERROR/
| sort @timestamp desc
| limit 20
```

---

## 🧩 Pricing Overview
- **Metrics:** $0.30 per metric per month  
- **Logs:** Pay per data ingested and stored  
- **Dashboards:** $3 per dashboard per month  
- **Alarms:** Based on number of active alarms  
- **Free Tier:** 10 custom metrics, 10 alarms, and 5GB of logs  

---

## 🧰 Best Practices
- Use **custom namespaces** for your application metrics.  
- Set **alarms for critical resources** (EC2, RDS, EBS).  
- Aggregate logs across accounts using **CloudWatch Logs Centralization**.  
- Use **metric filters** to extract specific data from logs.  
- Set up **anomaly detection** for proactive alerts.  

---

## ⚙️ Troubleshooting
| Issue | Solution |
|--------|-----------|
| Metrics not visible | Verify that monitoring is enabled for the service. |
| Logs not appearing | Check IAM permissions and log group names. |
| Alarm not triggering | Ensure thresholds and evaluation periods are set correctly. |
| High billing | Delete unused metrics and alarms. |

---

## 🧭 Use Cases
- Monitor **EC2 CPU usage** and trigger scaling.  
- Track **S3 bucket size and object count**.  
- Analyze **application logs for errors**.  
- Create **automated recovery actions** using Lambda.  
- Visualize **system health** on dashboards.  

---

## 🧩 Conclusion
**Amazon CloudWatch** is the central monitoring system for AWS.  
It helps you **observe, analyze, and automate** actions across all resources — from infrastructure to applications — ensuring high availability and performance.

With CloudWatch, you can achieve:
- Full visibility into AWS resources 🌍  
- Proactive alerting 🔔  
- Automated actions ⚙️  
- Optimized operations 🚀  

---

## 📚 References
- [AWS CloudWatch Official Documentation](https://docs.aws.amazon.com/cloudwatch/)  
- [CloudWatch Metrics and Dimensions](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html)  
- [AWS CloudWatch Pricing](https://aws.amazon.com/cloudwatch/pricing/)  
- [AWS CLI CloudWatch Commands](https://docs.aws.amazon.com/cli/latest/reference/cloudwatch/)  
- [CloudWatch Logs Insights](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/AnalyzingLogData.html)

---

## 👨‍💻 Author
**Aditya Jadhav**  
Cloud & DevOps Learner  
🌐 [GitHub Profile](https://github.com/AdiJadhav1608)

---

⭐ *If you found this documentation helpful, give it a star and keep monitoring smarter with CloudWatch!*
