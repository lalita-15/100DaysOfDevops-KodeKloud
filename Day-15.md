# Day 15 - Linux Administration TimeZone SetUp & Ansible Setup

Today I completed two DevOps hands-on labs focused on Linux system administration TimeZone SetUp and automation using Ansible.

---

# Task 1 - Synchronize Timezone on Application Servers App Server 1, 2, 3

## Problem Statement

The timezone configuration across the Nautilus Application Servers was inconsistent. The objective was to synchronize the timezone with the local datacenter timezone.

### Objective

- Configure all Nautilus Application Servers to use:
  - `Australia/Lindeman`

---

## Solution
## Step 1: Connect to the App Server 1

### Step 2: Verify Current Timezone

```
timedatectl
```

### Step 2: Set Timezone

```
sudo timedatectl set-timezone Australia/Lindeman
```

### Step 3: Verify Again

```
timedatectl
```

---

## Skills Practiced

- Linux Time Management
- timedatectl
- Timezone Configuration

---

# Task 2 - Install Ansible on Jump Host

## Problem Statement

The DevOps team selected Ansible as the configuration management tool. The requirement was to install a specific Ansible version on the Jump Host using **pip3** and make it available globally.

### Objective

- Install **Ansible 4.9.0**
- Ensure all users can execute Ansible commands

---

## Solution

### Step1: Become Root

```bash
sudo -i
```

### Step2: Verify pip

```bash
pip3 --version
```

### Step 3: Install Ansible

```bash
pip3 install ansible==4.9.0
```

### Step 4: Verify Installation

```bash
ansible --version
```

### Step5: Verify Binary

```bash
which ansible
```

---

## Skills Practiced

- Ansible Installation
- Python Package Management (pip3)
- Linux Package Management
- PATH Verification

---

# Commands Used

## Timezone Configuration

```bash
timedatectl
sudo timedatectl set-timezone Australia/Lindeman
timedatectl
```

## Ansible Installation

```bash
sudo -i
pip3 --version
pip3 install ansible==4.9.0
ansible --version
which ansible
```

---

# Key Learnings

- Configured Linux servers with the correct timezone using `timedatectl`.
- Learned how timezone consistency is important for logs, monitoring, and distributed systems.
- Installed Ansible using `pip3` and verified the installation.
- Understood the difference between user-level and global package installation.
- Verified executable availability using `which` and `ansible --version`.

---
## Troubleshooting 
Initially, I installed the wrong Ansible version, so the task validation failed.
- I also learned the difference between installing Ansible for a single user and installing it globally for all users.
- At one point, ansible was not found even after installation then I used commands which ansible, pip3 show ansible, and ansible --version to troubleshoot the issue.
- Finally, I understood the importance of verifying  installed version .