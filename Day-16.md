# Day 16 - Firewall Configuration & MariaDB Service Troubleshooting

## Task 1: Configure Firewall for Backup UI Application

### Problem Statement

The Nautilus system administrators rolled out a new Backup UI application on Nautilus App Server 1. The application runs on **port 6300**, and the firewall needed to be configured to allow all incoming traffic.

### Objective

- Install and enable the `firewalld` service.
- Allow incoming traffic on **6300/tcp**.
- Ensure the default firewall zone is **public**.

---

## Solution

### Step 1: Connect to Application Server

```
ssh tony@stapp01
sudo su -
```

### Step 2: Install Firewalld

```bash
yum install firewalld -y 
```

### Step 3: Enable and Start Firewalld

```
systemctl start firewalld

systemctl enable firewalld
```

### Step 4: Set Default Zone and Allow Port 6300

```bash
firewall-cmd --zone=public --add-port=6300/tcp --permanent
```


### Step 6: Reload Firewall

```
firewall-cmd --reload
```

### Step 7: Verify

```
systemctl status firewalld
firewall-cmd --get-default-zone
firewall-cmd --list-ports
```



# Task 2: Fix MariaDB Service Issue

## Problem Statement

The Nautilus application was unable to connect to the database because the **MariaDB service was down** on the database server.

### Objective

- Identify the issue preventing MariaDB from starting.
- Resolve the issue.
- Start the MariaDB service successfully.

---

## Solution

### Step 1: Connect to Database Server

```
ssh peter@stdb01
sudo su -
```

### Step 2: Check MariaDB Status

```
systemctl status mariadb
```

The service was **inactive (dead)**.

### Step 3: Try to Start MariaDB

```
systemctl start mariadb
```

MariaDB failed to start and displayed an error.

### Step 4: Find the Root Cause

After checking the error message, I found that the **mysql user did not have the required ownership and permissions** on the database directory.

### Error

```text
chown: changing ownership of '/var/lib/mysql': Operation not permitted
```

Because of this permission issue, MariaDB was unable to access its data directory and could not start.

### Step 5: Fix Directory Ownership and Permissions

```
chown -R mysql:mysql /var/lib/mysql
chmod 755 /var/lib/mysql
```

### Step 6: Start MariaDB Again

```
systemctl start mariadb
```

### Step 7: Verify Service Status

```
systemctl status mariadb
```

The MariaDB service started successfully and was running normally.

---

## Troubleshooting

### Problem Faced

Initially, I checked the MariaDB service status and found that it was inactive.

```bash
systemctl status mariadb
```

I tried to start the service.

```
systemctl start mariadb
```

However, it failed with an error.

### Root Cause

The **mysql** user did not have the required ownership and permissions for the `/var/lib/mysql` directory.

Error:

```text
chown: changing ownership of '/var/lib/mysql': Operation not permitted
```

### Resolution

I corrected the ownership and permissions using the following commands:

```bash
chown -R mysql:mysql /var/lib/mysql
chmod 755 /var/lib/mysql
```

Then I started the MariaDB service again.

```bash
systemctl start mariadb
```

Finally, I verified that the service was running successfully.

```bash
systemctl status mariadb
```

---

# Key Learnings

- Learned how to install and configure **Firewalld**.
- Learned how to allow specific ports through the firewall.
- Understood the importance of verifying firewall rules after configuration.
- Learned how to troubleshoot a failed **MariaDB** service.
- Understood how incorrect directory ownership and permissions can prevent database services from starting.
- Improved troubleshooting skills using `systemctl` and Linux permission management.

---
