# 🗂️ Network File System (NFS)

## 🧠 Introduction

**Network File System (NFS)** is a **distributed file system protocol** that allows users to access files over a **network** as if they were located on their **local machine**.  
It was developed by **Sun Microsystems** and is widely used for **sharing files between Linux systems**.

---

## ⚙️ Key Features

- **Centralized Storage**: Store files on a single server and share them with multiple clients.
- **File Sharing**: Enables multiple users or systems to access the same files.
- **Transparency**: Remote files appear as local files to the user.
- **Performance**: Efficient for Linux-based environments and low-latency networks.
- **Access Control**: You can configure which clients have read/write access.

---

## 🏗️ Architecture

NFS operates in a **client-server architecture**:
- **NFS Server**: Stores the shared files and directories.
- **NFS Client**: Mounts and accesses shared directories over the network.

Example:
```
Server (192.168.1.10)
 ├── /shared/data
Client (192.168.1.20)
 └── /mnt/data → mounts /shared/data
```

---

## 🔧 NFS Setup (Linux Example)

### **On NFS Server**
```
# Install NFS server package
sudo apt install nfs-kernel-server -y

# Create a shared directory
sudo mkdir -p /srv/nfs/shared

# Set permissions
sudo chown nobody:nogroup /srv/nfs/shared

# Edit export file
sudo nano /etc/exports
/srv/nfs/shared 192.168.1.0/24(rw,sync,no_subtree_check)

# Apply changes
sudo exportfs -a
sudo systemctl restart nfs-kernel-server
```

### **On NFS Client**
```
# Install NFS client package
sudo apt install nfs-common -y

# Create mount directory
sudo mkdir -p /mnt/shared

# Mount shared folder
sudo mount 192.168.1.10:/srv/nfs/shared /mnt/shared

# Verify
df -h
```

---

## 🧩 Advantages

✅ Easy to set up and manage  
✅ Transparent remote access  
✅ Centralized storage solution  
✅ Works well for internal Linux networks  

---

## ⚠️ Limitations

❌ Not ideal for the public internet  
❌ Limited scalability for large, multi-region deployments  
❌ Security concerns if not configured properly  

---

## 📚 References

- [NFS Overview - Linux Documentation](https://help.ubuntu.com/community/SettingUpNFSHowTo)  
- [NFS Wikipedia](https://en.wikipedia.org/wiki/Network_File_System)  
- [NFS Admin Guide - Red Hat](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html/managing_file_systems/assembly_nfs-server_configuring-and-managing-network-file-systems)

---

## 👨‍💻 Author

**Aditya Jadhav**  
Cloud & DevOps Learner  
🌐 [GitHub Profile](https://github.com/AdiJadhav1608)

---

⭐ *If you found this helpful, give it a star and keep exploring AWS & Linux!*
