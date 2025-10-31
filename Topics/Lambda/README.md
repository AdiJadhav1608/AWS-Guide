# ⚙️ AWS Lambda (Serverless Computing)

## 📘 Introduction
**AWS Lambda** is a **serverless compute service** that lets you **run code without provisioning or managing servers**.  
You only pay for the compute time your code consumes — **no charges when your code is not running**.

Lambda automatically scales your applications by running code in response to **events**, such as:
- File uploads to Amazon S3  
- Updates in DynamoDB  
- HTTP requests via Amazon API Gateway  
- Scheduled tasks via Amazon EventBridge (CloudWatch Events)

---

## 🎯 Key Features

| Feature | Description |
|----------|--------------|
| **Serverless** | No need to manage or provision servers. |
| **Event-Driven** | Executes automatically in response to AWS service events or API calls. |
| **Auto Scaling** | Automatically scales up or down based on request volume. |
| **Multiple Language Support** | Supports Python, Node.js, Java, Go, .NET, Ruby, etc. |
| **Integrated Security** | IAM-based access control and VPC integration. |
| **Pay-as-you-Go** | Pay only for execution time (per 1ms). |
| **High Availability** | Runs across multiple Availability Zones automatically. |

---

## 🧩 Core Concepts

| Concept | Description |
|----------|--------------|
| **Function** | Your code + configuration (runtime, memory, timeout, triggers). |
| **Trigger** | AWS service or event that invokes the Lambda function. |
| **Handler** | The entry point method in your code that AWS Lambda calls. |
| **Execution Role** | IAM role granting Lambda permissions to access AWS resources. |
| **Concurrency** | Number of requests a function can handle simultaneously. |
| **Layers** | Packages external libraries or dependencies for reuse. |
| **Destination** | Target service where results or errors are sent (SQS, SNS, EventBridge). |

---

## 🧠 How AWS Lambda Works

```
[ Event Source (S3 / API Gateway / DynamoDB) ]
                    ↓
            [ AWS Lambda Function ]
                    ↓
          [ Processed Output / Response ]
```

1. An event triggers the Lambda function.  
2. AWS Lambda automatically provisions resources and runs your code.  
3. The function executes, returns a response, and resources are released automatically.  

---

## 💻 Supported Languages
- Python  
- Node.js  
- Java  
- Go  
- C# / .NET Core  
- Ruby  
- PowerShell  

---

## 🧰 Example: Simple Python Lambda Function

### `lambda_function.py`
```python
def lambda_handler(event, context):
    name = event.get("name", "World")
    message = f"Hello, {name} from AWS Lambda!"
    print(message)
    return {
        "statusCode": 200,
        "body": message
    }
```

---

## ⚙️ Deploying AWS Lambda

### 🪶 Step 1: Create a Lambda Function (via AWS Console)
1. Go to **AWS Lambda Console** → **Create function**.  
2. Choose “Author from scratch.”  
3. Enter a function name and select a runtime (e.g., Python 3.12).  
4. Assign an **execution role** (new or existing IAM role).  
5. Add your code and click **Deploy**.  

---

### 🪶 Step 2: Create Lambda via AWS CLI

```bash
zip function.zip lambda_function.py
aws lambda create-function \
  --function-name myLambdaFunction \
  --runtime python3.12 \
  --role arn:aws:iam::123456789012:role/LambdaRole \
  --handler lambda_function.lambda_handler \
  --zip-file fileb://function.zip
```

---

### 🪶 Step 3: Invoke the Function
```bash
aws lambda invoke \
  --function-name myLambdaFunction \
  --payload '{"name": "Aditya"}' \
  response.json
```

---

## 🧩 Integrations with Other AWS Services

| Service | Use Case |
|----------|-----------|
| **Amazon S3** | Trigger Lambda on object creation or deletion. |
| **API Gateway** | Invoke Lambda for RESTful APIs. |
| **DynamoDB** | Trigger on table updates (Streams). |
| **CloudWatch Events / EventBridge** | Run scheduled or event-based tasks. |
| **SNS / SQS** | Process messages asynchronously. |
| **Step Functions** | Build serverless workflows. |
| **EFS** | Access large shared files directly from Lambda. |

---

## 🧠 Example: S3 Trigger for Lambda

**Use Case:** Automatically process an image when uploaded to an S3 bucket.

1. Create a Lambda function.  
2. Add an S3 trigger (event: “Object Created”).  
3. Grant S3 permission in Lambda’s IAM role.  
4. Lambda automatically executes when a file is uploaded.

---

## 🧩 Lambda Layers

**Lambda Layers** let you include additional code, libraries, or dependencies.  
They promote reusability and cleaner deployment packages.

```bash
aws lambda publish-layer-version \
  --layer-name my-layer \
  --description "Shared Python dependencies" \
  --zip-file fileb://layer.zip \
  --compatible-runtimes python3.12
```

Then attach it to your Lambda function:
```bash
aws lambda update-function-configuration \
  --function-name myLambdaFunction \
  --layers arn:aws:lambda:region:account-id:layer:my-layer:1
```

---

## 🔒 Security & Permissions

| Feature | Description |
|----------|--------------|
| **IAM Role** | Grants permission to access AWS services (S3, DynamoDB, etc.). |
| **Environment Variables** | Store configuration data securely. |
| **VPC Access** | Run Lambda inside your private VPC. |
| **Encryption** | Environment variables encrypted using KMS. |
| **Code Signing** | Ensures only trusted code runs on Lambda. |

---

## 🧮 Lambda Pricing

| Metric | Description |
|---------|--------------|
| **Requests** | First 1M requests/month are free, then $0.20 per million. |
| **Duration** | Charged per ms of execution, depending on allocated memory. |
| **Provisioned Concurrency** | Extra cost for pre-warmed execution environments. |
| **Data Transfer** | Standard AWS data transfer rates apply. |

✅ **Free Tier:**  
- 1 million requests per month  
- 400,000 GB-seconds of compute time  

---

## 🧠 Monitoring and Logging

| Tool | Purpose |
|------|----------|
| **Amazon CloudWatch Logs** | Automatically captures function logs. |
| **CloudWatch Metrics** | Tracks invocations, errors, throttles, and duration. |
| **AWS X-Ray** | Provides end-to-end tracing of requests and performance insights. |

### Example: View Logs
```bash
aws logs filter-log-events \
  --log-group-name /aws/lambda/myLambdaFunction
```

---

## 🧰 Best Practices

- Use **environment variables** for configuration.  
- Keep functions **lightweight** and modular.  
- Use **Lambda Layers** for dependencies.  
- Set appropriate **timeouts and memory**.  
- Enable **CloudWatch monitoring** for debugging.  
- Implement **error handling and retries**.  
- Use **Provisioned Concurrency** for low-latency workloads.  
- Secure sensitive data using **KMS encryption**.  

---

## 🧱 Example Architecture

```
[ User/API Request ]
        ↓
 [ API Gateway ]
        ↓
 [ AWS Lambda Function ]
        ↓
 [ DynamoDB / S3 / SNS ]
```

**Scenario:**  
A user uploads a file → API Gateway triggers Lambda → Lambda processes and stores results in S3 or DynamoDB.

---

## ⚡ Lambda vs EC2 vs Fargate

| Feature | Lambda | EC2 | Fargate |
|----------|---------|-----|----------|
| **Server Management** | Fully managed | Manual | Semi-managed |
| **Scalability** | Auto | Manual | Auto |
| **Billing Model** | Per execution | Per hour | Per container-second |
| **Startup Time** | Milliseconds | Minutes | Seconds |
| **Use Case** | Event-driven tasks | Full applications | Container workloads |

---

## 🧩 Common Use Cases

- File processing (S3 trigger)  
- Real-time data transformation  
- Serverless REST APIs  
- Chatbots and automation  
- IoT device data processing  
- Scheduled clean-up jobs  
- Event-driven microservices  

---

## 🧠 Troubleshooting

| Issue | Cause | Solution |
|--------|--------|-----------|
| Timeout errors | Function exceeds time limit | Increase timeout or optimize code |
| Permission denied | Missing IAM policy | Attach proper IAM role |
| Cold start delays | Function not warm | Use provisioned concurrency |
| Log errors | Missing CloudWatch permissions | Add `AWSLambdaBasicExecutionRole` policy |

---

## 📚 References

- [AWS Lambda Documentation](https://docs.aws.amazon.com/lambda/)  
- [AWS Lambda Pricing](https://aws.amazon.com/lambda/pricing/)  
- [Lambda CLI Reference](https://docs.aws.amazon.com/cli/latest/reference/lambda/index.html)  
- [Lambda Layers Guide](https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html)  
- [Serverless Best Practices](https://aws.amazon.com/serverless/best-practices/)

---

## 👨‍💻 Author
**Aditya Jadhav**  
Cloud & DevOps Learner  
🌐 [GitHub Profile](https://github.com/AdiJadhav1608)

---

⭐ *If you found this helpful, give it a star and keep building serverless applications with AWS Lambda!*
