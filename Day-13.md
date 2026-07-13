# Day 13 – Cron Jobs & Crontab Access Control

##  Overview

Today's Lab focused on **task automation and user access control** in Linux. I worked on configuring scheduled tasks using **Cron** and learned how to control which users are allowed to create and manage cron jobs.

---

#  Task 1: Configure a Sample Cron Job

## Objective

The goal was to prepare all three application servers for automated task scheduling by:

- Installing the **cronie** package.
- Starting the **crond** service.
- Creating a sample cron job for the **root** user that runs every 5 minutes.

---

## Solution
## Step 1. Connect to App Server3

### Step 2. Install Cronie

```
sudo yum install -y cronie
```

### Step3. Start Cron Service

```
sudo systemctl start crond
```
Check the cron service status:

```
systemctl status crond
```

### Step4. Add a Cron Job for Root

```
sudo crontab -e
```

Add the following entry:

```
*/5 * * * * echo hello > /tmp/cron_text
```

---

## Verification

Check the root user's cron jobs:

```
sudo crontab -l
```



---

## What I Learned

- How Cron automates repetitive tasks.
- Difference between the `cronie` package and the `crond` service.
- How to schedule commands using cron expressions.
- How to create cron jobs for the root user.

---

#  Task 2: Restrict Crontab Access

## Objective

Configure crontab access on **App Server 3** by:

- Allowing **kirsty** to use crontab.
- Denying **garrett** from using crontab.

---

## Step1:  Configuration

### Step2: Allow User

```
sudo vi /etc/cron.allow
```

```
kirsty
```

### Step 3: Deny User

```
sudo vi /etc/cron.deny
```

```
garrett
```

---

## Step 4: Verification

```bash
cat /etc/cron.allow
```

Expected Output:

```
ammar
```

```bash
cat /etc/cron.deny
```

Expected Output:

```
rod
```

---

## What I Learned

- How Linux controls access to cron jobs.
- The purpose of `cron.allow` and `cron.deny`.
- `cron.allow` has higher priority than `cron.deny`.
- Restricting cron access improves system security.



---

## 💻 Commands Practiced

```bash
yum install
systemctl start
systemctl status
crontab -e
crontab -l
cat
```


