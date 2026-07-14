# Day 14 - Linux Administration Tasks

##  Overview

Today, I completed two Linux administration tasks focused on **SSH authentication** and **system boot target configuration**.

---

# 🛠️ Task 1: Configure Password-less SSH Authentication

## 🎯 Objective

Configure password-less SSH authentication from the **thor** user on the jump host to all application servers using their respective sudo users.

---

## Solution

### Step 1: Check current user

```bash
whoami
```

### Step 2: Generate SSH key pair 

```bash
ssh-keygen 
```

### Step 3: Verify generated keys

```bash
ls -la ~/.ssh
```

### Step 4: Copy public key to App Server

```
ssh-copy-id tony@stapp01
ssh-copy-id steve@stapp02
ssh-copy-id banner@stapp02
```

### Test password-less login

```
ssh tony@stapp01
ssh steve@stapp02
ssh banner@stapp02
```

---

## Key Concepts

- SSH Key Authentication
- Public Key (`id_ed25519.pub`)
- Private Key (`id_ed25519`)
- `ssh-copy-id`

---

## Skills Practiced

- SSH
- Linux Authentication
- Remote Server Management

---

# 🛠️ Task 2: Enable GUI Booting by Default

## 🎯 Objective

Configure the server to boot into **GUI mode by default** without rebooting the server.

---

## Solution
## Step1 1: Connect to the Server App Server 1

### Step 2: Check current default target

```
systemctl get-default
```

### Step3: Change default boot target

```
sudo systemctl set-default graphical.target
```

### Step 4: Verify configuration

```
systemctl get-default
```
**Repeat Same Steps From 1-4 on App server2 and App server3**
---

## Key Concepts

### multi-user.target

- Command Line Interface (CLI)
- No graphical desktop

### graphical.target

- Graphical User Interface (GUI)
- Desktop environment starts automatically
---


#  What I Learned Today

- Configured password-less SSH authentication using SSH keys.
- Understood how `ssh-copy-id`.
- Learned how Linux stores SSH keys.
- Managed Linux boot targets using `systemctl`.
- Enabled GUI boot mode without rebooting the server.
- Strengthened Linux administration and troubleshooting skills.

---

