# AWS EC2 – EBS Volume Hands-On Project

## Project Overview

This project demonstrates how to create and attach an additional EBS volume to an EC2 instance, format the disk, mount it, and store data on it. The goal is to understand how persistent storage works in AWS and how external disks can be used for applications, logs, backups, or user data.

This hands-on project was completed as part of EC2 storage learning.

---

## AWS Services Used

* Amazon EC2 – Virtual server
* Amazon EBS – Persistent block storage

---

## Architecture

User connects to EC2 instance.
An additional EBS volume is attached to the instance and mounted to a directory where data can be stored.

```
EC2 Instance
│
├── Root Volume (OS Disk)
│     └── Operating System
│
└── Extra EBS Volume
      └── Mounted at /data
            └── Stores application data
```

---

## Step 1 – Create an EBS Volume

Navigate to:
EC2 → Volumes → Create Volume

Configuration:

* Volume type: gp3
* Size: 8 GB
* Availability Zone: Same as the EC2 instance

Important:
The EBS volume must be created in the same Availability Zone as the EC2 instance.

---

## Step 2 – Attach Volume to EC2

1. Select the created EBS volume
2. Click **Actions → Attach Volume**
3. Select the EC2 instance
4. Use the default device name

After attaching, the disk becomes visible inside the EC2 instance.

---

## Step 3 – Verify Disk in EC2

Connect to the instance and run:

```
lsblk
```

Example output:

```
nvme0n1  → root disk
nvme1n1  → new EBS volume
```

---

## Step 4 – Format the Disk

A new disk must be formatted before storing data.

Command:

```
sudo mkfs -t ext4 /dev/nvme1n1
```

This creates a filesystem on the disk.

---

## Step 5 – Create Mount Directory

Create a folder where the disk will be accessible.

```
sudo mkdir /data
```

---

## Step 6 – Mount the Disk

Mount the EBS
