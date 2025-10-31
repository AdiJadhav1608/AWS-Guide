# 💻 AWS CLI (Command Line Interface)

## 📘 Introduction
The **AWS Command Line Interface (CLI)** is a unified tool that allows you to **interact with AWS services** directly from your terminal or command prompt.  
It provides a quick, scriptable way to automate AWS resource management, enabling developers, system administrators, and DevOps engineers to **manage their entire AWS infrastructure via commands**.

The AWS CLI supports **Windows, macOS, and Linux**, and can manage **over 200 AWS services** using simple, consistent commands.

---

## 🎯 Key Features
- ⚙️ **Unified Tool:** Manage all AWS services from a single command line tool.  
- 🧠 **Automation Friendly:** Easily script and automate repetitive tasks.  
- 🌍 **Cross-Platform:** Works seamlessly on Windows, macOS, and Linux.  
- 🔐 **Secure:** Integrates with AWS IAM for credential-based access.  
- 🧩 **Customizable Output:** Choose JSON, YAML, text, or table formats.  
- 📜 **Versioning Support:** Compatible with both AWS CLI v1 and v2.  

---

## 🧱 AWS CLI Versions
| Version | Description |
|----------|--------------|
| **AWS CLI v1** | Legacy version, Python-based. Still supported but less recommended. |
| **AWS CLI v2** | Latest, standalone installer with new features, better performance, and simplified installation. |

---

## ⚙️ Installation

### 🪟 Windows
Download and install the AWS CLI MSI installer:
```
https://awscli.amazonaws.com/AWSCLIV2.msi
```

Then verify:
```
aws --version
```

### 🐧 Linux (Ubuntu / Debian)
```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
aws --version
```

### 🍎 macOS
```
curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
sudo installer -pkg AWSCLIV2.pkg -target /
aws --version
```

---

## 🔑 AWS CLI Configuration

After installation, configure credentials:
```
aws configure
```

You’ll be prompted for:
```
AWS Access Key ID [None]: <your-access-key>
AWS Secret Access Key [None]: <your-secret-key>
Default region name [None]: ap-south-1
Default output format [None]: json
```

This creates a config file at:
```
~/.aws/config
~/.aws/credentials
```

---

## 🧩 AWS CLI Command Structure
```
aws <service> <operation> [parameters]
```

### Example:
```
aws s3 ls
aws ec2 describe-instances
aws iam list-users
aws s3 cp file.txt s3://my-bucket/
```

---

## 🧠 Commonly Used AWS CLI Commands

### 🔹 S3
```
aws s3 ls
aws s3 mb s3://my-new-bucket
aws s3 cp myfile.txt s3://my-new-bucket/
aws s3 sync ./local-folder s3://my-new-bucket
```

### 🔹 EC2
```
aws ec2 describe-instances
aws ec2 start-instances --instance-ids i-0abcd1234ef56789
aws ec2 stop-instances --instance-ids i-0abcd1234ef56789
```

### 🔹 IAM
```
aws iam list-users
aws iam create-user --user-name DevUser
aws iam attach-user-policy --user-name DevUser --policy-arn arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess
```

### 🔹 CloudWatch
```
aws cloudwatch list-metrics
aws cloudwatch get-metric-statistics --metric-name CPUUtilization --namespace AWS/EC2 \
--statistics Average --period 300 --start-time 2024-10-20T00:00:00Z --end-time 2024-10-21T00:00:00Z
```

---

## 🧩 Output Formats
You can specify output formats globally or per command:
| Format | Example Command |
|---------|----------------|
| **JSON (default)** | `aws ec2 describe-instances --output json` |
| **YAML** | `aws s3 ls --output yaml` |
| **Table** | `aws ec2 describe-instances --output table` |
| **Text** | `aws iam list-users --output text` |

---

## 🔒 Security Best Practices
- Never share or hardcode AWS credentials.  
- Use **IAM roles** instead of static credentials when possible.  
- Rotate access keys regularly.  
- Enable **MFA (Multi-Factor Authentication)**.  
- Use **AWS Vault** or **SSO** for secure authentication.  

---

## 🧰 Advanced CLI Features
| Feature | Description |
|----------|--------------|
| **AWS CLI Profiles** | Create multiple named profiles for different accounts. |
| **Paginators** | Automatically handle large outputs (e.g., list-instances). |
| **Waiters** | Wait for resource states (e.g., instance to stop/start). |
| **AWS CLI Plugins** | Extend functionality for custom needs. |
| **Command Autocomplete** | Enable tab completion for faster commands. |

Example for multiple profiles:
```
aws configure --profile dev
aws configure --profile prod
aws s3 ls --profile prod
```

---

## 🧭 Use Cases
- Automate daily cloud management tasks.  
- Integrate AWS operations in shell scripts or CI/CD pipelines.  
- Monitor and audit resources programmatically.  
- Manage AWS infrastructure from local or remote servers.  

---

## 🧩 Troubleshooting
| Issue | Solution |
|--------|-----------|
| **Command not found** | Add CLI to system PATH or reinstall. |
| **Access Denied** | Check IAM permissions or attached policies. |
| **Invalid region or credentials** | Verify with `aws configure list`. |
| **Slow response** | Use specific regions or CloudFront endpoints. |

---

## 🧠 Example Script: Automate EC2 Backup
```
#!/bin/bash
# Create EBS snapshot of an instance
INSTANCE_ID="i-0abcd1234ef56789"
VOLUME_ID=$(aws ec2 describe-instances \
  --instance-ids $INSTANCE_ID \
  --query "Reservations[*].Instances[*].BlockDeviceMappings[*].Ebs.VolumeId" \
  --output text)

aws ec2 create-snapshot --volume-id $VOLUME_ID --description "Automated backup"
echo "Snapshot created successfully for volume: $VOLUME_ID"
```

---

## 🧩 Conclusion
The **AWS CLI** is a powerful and flexible tool that enables developers and administrators to **automate and control** every aspect of AWS services.  
Whether you’re provisioning EC2 instances, managing S3 buckets, or scripting entire deployments, AWS CLI simplifies cloud management through the command line.

---

## 📚 References
- [AWS CLI Documentation](https://docs.aws.amazon.com/cli/latest/userguide/)  
- [AWS CLI Command Reference](https://docs.aws.amazon.com/cli/latest/reference/)  
- [AWS CLI GitHub Repository](https://github.com/aws/aws-cli)  
- [AWS CLI v2 Features](https://aws.amazon.com/cli/)  
- [AWS Free Tier](https://aws.amazon.com/free/)

---

## 👨‍💻 Author
**Aditya Jadhav**  
Cloud & DevOps Learner  
🌐 [GitHub Profile](https://github.com/AdiJadhav1608)

---

⭐ *If you found this helpful, give it a star and keep exploring AWS!*
