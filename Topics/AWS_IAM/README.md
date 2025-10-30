# 🔐 AWS IAM (Identity and Access Management)

## 📘 Introduction
**AWS Identity and Access Management (IAM)** is a secure web service that helps you **control access** to AWS resources.  
It enables you to manage **who can access your AWS account (authentication)** and **what actions they can perform (authorization)** — ensuring **least privilege** and **secure operations** across your AWS environment.

---

## 🎯 Key Objectives
- ✅ **Secure Access Control:** Manage users, groups, and permissions centrally.  
- 🧩 **Granular Permissions:** Define precise access levels using policies.  
- 👥 **Multi-User Environment:** Safely manage access for multiple team members.  
- 🧠 **Federated Access:** Integrate existing user directories (like Microsoft AD).  
- 🛡️ **Least Privilege Principle:** Give only the permissions required — nothing more.

---

## 🧱 Core Components

| Component | Description |
|------------|--------------|
| **Users** | Individual identities with long-term credentials (access keys, passwords). |
| **Groups** | Collection of IAM users with shared permissions. |
| **Roles** | Temporary access permissions assigned to AWS services, users, or applications. |
| **Policies** |  documents that define permissions (allow or deny actions). |
| **Identity Providers (IdP)** | External authentication sources like Google Workspace or Active Directory. |

---

## 🧩 IAM Policy Structure
IAM policies are written in ** format** and specify what actions are allowed or denied on which resources.

### Example Policy
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:*",
      "Resource": "*"
    }
  ]
}
```
✅ **Meaning:** Allows full access (`s3:*`) to all S3 resources in the account.

---

## 🔑 Authentication & Authorization
| Concept | Description |
|----------|--------------|
| **Authentication** | Verifies *who you are* (e.g., user login or access key). |
| **Authorization** | Determines *what you can do* (based on IAM policies). |

---

## ⚙️ IAM Role vs User
| Feature | IAM User | IAM Role |
|----------|-----------|-----------|
| Credential Type | Long-term (passwords, access keys) | Temporary (STS tokens) |
| Use Case | Human access | Service-to-service access |
| Example | Developer logging into AWS Console | EC2 instance accessing S3 bucket |

---

## 🔧 Common Use Cases
- Granting developers limited access to specific AWS services.  
- Allowing EC2 instances to access S3 securely via IAM roles.  
- Enabling federated logins using corporate credentials.  
- Creating cross-account roles for multi-account architectures.  

---

## 🧭 How It Works
1. **Create IAM Users/Groups** for your team members.  
2. **Attach Policies** defining what each user/group can access.  
3. **Assign IAM Roles** to AWS resources like EC2 or Lambda.  
4. **Use CloudTrail** to monitor API calls and access logs.  
5. **Apply MFA (Multi-Factor Authentication)** for enhanced security.  

---

## 🛠️ Example: Create IAM User and Attach Policy (CLI)
```bash
# Create IAM user
aws iam create-user --user-name dev-user

# Attach existing policy (e.g., AmazonS3ReadOnlyAccess)
aws iam attach-user-policy \
  --user-name dev-user \
  --policy-arn arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess

# Create access keys for programmatic access
aws iam create-access-key --user-name dev-user
```

---

## 🧩 IAM Best Practices
- 🔒 **Enable MFA** for all users (especially root account).  
- 🚫 **Avoid using root credentials** for daily operations.  
- 🧠 **Follow Least Privilege Principle** — only grant necessary permissions.  
- 🕵️‍♂️ **Rotate credentials regularly.**  
- 🪪 **Use IAM roles** instead of embedding credentials in applications.  
- 🧩 **Tag IAM resources** for organization and tracking.  
- 📊 **Monitor and audit IAM activity** using AWS CloudTrail.  

---

## ⚡ Advanced IAM Concepts
| Feature | Description |
|----------|--------------|
| **IAM Identity Center (AWS SSO)** | Centralized login for multiple AWS accounts. |
| **Access Analyzer** | Identifies resources shared publicly or with other accounts. |
| **Service Control Policies (SCP)** | Enforce permissions boundaries in AWS Organizations. |
| **IAM Permission Boundaries** | Limit the maximum permissions a user/role can have. |
| **Resource-Based Policies** | Attach policies directly to resources (e.g., S3 buckets). |

---

## 🧠 Example Architecture
A typical IAM setup includes:
- IAM Users (Developers, Admins)
- IAM Groups (Dev-Team, QA-Team)
- IAM Roles (EC2-Access, Lambda-Execution)
- Managed Policies (AWS Managed + Custom Policies)
- Multi-Factor Authentication (MFA)
- CloudTrail Logging for Access Monitoring

---

## 🧩 Conclusion
AWS IAM is the **foundation of AWS security**, providing fine-grained access control and authentication across all services.  
By implementing IAM best practices, you can ensure a **secure, compliant, and well-managed AWS environment**.

---

## 📚 References
- [AWS IAM Documentation](https://docs.aws.amazon.com/iam/)  
- [IAM Policy Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html)  
- [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)  
- [AWS IAM Pricing](https://aws.amazon.com/iam/pricing/)  
- [AWS Free Tier](https://aws.amazon.com/free/)

---

## 👨‍💻 Author
**Aditya Jadhav**  
Cloud & DevOps Learner  
🌐 [GitHub Profile](https://github.com/AdiJadhav1608)

---

⭐ *If you found this helpful, give it a star and keep exploring AWS!*
