# 🔑 SSH Service Usage in AWS

This guide explains how to **use SSH (Secure Shell) to connect to AWS EC2 instances** securely.  
SSH is the most common way to access Linux-based EC2 instances for administration and deployment tasks.

---

## 🧭 What is SSH?

**SSH (Secure Shell)** is a **protocol for secure remote login** and command execution over an unsecured network.  
It encrypts the connection to protect data and passwords.

**Key Features:**
- Encrypted connection (secure)
- Remote access to servers
- File transfer using SCP/SFTP
- Command execution from anywhere

---

## 🔧 Prerequisites for SSH in AWS

1. **EC2 Instance running Linux**
2. **Security Group** allowing SSH (port 22)
3. **Private Key File (.pem)** downloaded from AWS during instance creation
4. SSH client (Linux/macOS terminal or Windows using PowerShell/Windows Terminal/Putty)

---

## 🛠️ Connecting to EC2 Using SSH

### Step 1: Set proper permissions for the `.pem` file
```bash
chmod 400 my-key-pair.pem
```
- This ensures the private key file is **readable only by you**, otherwise SSH will reject it.

### Step 2: Connect to your EC2 instance
```bash
ssh -i "my-key-pair.pem" ec2-user@<Public-IP-or-DNS>
```

**Parameters explained:**
- `-i "my-key-pair.pem"` → Specifies the private key file
- `ec2-user` → Default username for Amazon Linux. For Ubuntu, use `ubuntu`
- `<Public-IP-or-DNS>` → Public IPv4 address or DNS of your EC2 instance

### Step 3: Accept the fingerprint
- First-time connection will prompt:
```
The authenticity of host 'xx.xx.xx.xx' can't be established.
ECDSA key fingerprint is SHA256:...
Are you sure you want to continue connecting (yes/no)?
```
- Type `yes` and press Enter

---

## 🔑 Example for Ubuntu EC2

```bash
ssh -i "ubuntu-key.pem" ubuntu@ec2-18-222-111-123.compute-1.amazonaws.com
```

---

## 🔁 Copy Files Using SCP (Optional)

- Copy local file to EC2:
```bash
scp -i "my-key-pair.pem" localfile.txt ec2-user@<Public-IP>:/home/ec2-user/
```

- Copy file from EC2 to local:
```bash
scp -i "my-key-pair.pem" ec2-user@<Public-IP>:/home/ec2-user/remote.txt ./localfile.txt
```

---

## ⚠️ Common SSH Issues

| Issue | Cause | Solution |
|-------|-------|---------|
| Permission denied (publickey) | Wrong key file or permissions | `chmod 400 key.pem`, check username |
| Connection timed out | Security Group port 22 blocked | Add inbound rule: SSH, TCP, 22, Source: your IP |
| Host key verification failed | Fingerprint changed | Remove old host from `~/.ssh/known_hosts` |

---

## 🛡️ Best Practices

- Use **unique key pairs** for each instance  
- Never share your private key  
- Limit SSH access by **IP in Security Group**  
- Consider **SSH key rotation** periodically  

---

## 📚 References

- [AWS EC2 Connect Docs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html)  
- [SSH Official Documentation](https://www.ssh.com/ssh/)  

---

## 👨‍💻 Author

**Aditya Jadhav**  
Cloud & DevOps Learner  
🌐 [GitHub Profile](https://github.com/AdiJadhav1608)


⭐ *If you found this helpful, give it a star and keep learning AWS securely!*