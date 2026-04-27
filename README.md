# 📂 EFS to S3 Sync in Custom VPC

## 📌 Overview
This project demonstrates a centralized file sharing and automated backup system using AWS.

---

## 🛠️ Services Used
- Amazon EC2
- Amazon EFS
- Amazon S3
- AWS IAM
- Amazon VPC

---

## 🏗️ Architecture Diagram

<p align="center">
  <img src="L1 architecture diagram.png" width="700"/>
</p>

---

## ⚙️ Implementation Steps

### 1. VPC Setup
- Created VPC (10.0.0.0/16)
- Created public subnets
- Attached Internet Gateway

### 2. EC2 Setup
- Launched 2 EC2 instances
- Attached IAM role

### 3. EFS Setup
- Created file system
- Mounted on both EC2 instances

### 4. S3 Setup
- Created S3 bucket
- Blocked public access

### 5. Real-Time Sync
- Installed inotify-tools
- Created sync script
- Synced files to S3

---

## 🔄 Project Flow
1. File created in EC2
2. Stored in EFS
3. Inotify detects change
4. Script syncs to S3
5. Backup stored in S3

---

## 📜 Script Used

```bash
#!/bin/bash
while inotifywait -r -e modify,create,delete /share/projects
do
  aws s3 sync /share/projects s3://your-bucket-name
done
