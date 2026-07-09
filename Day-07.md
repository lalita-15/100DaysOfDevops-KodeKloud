# 📅 Day 07 – Secure Root SSH Access

## 📝 Problem Statement

Following a security audit, the security team at xFusionCorp Industries introduced a new security policy to restrict direct root SSH login across all application servers in the Stratos Datacenter. The objective was to improve server security by preventing direct root access over SSH.

---

## 🎯 Objective

- Disable direct root SSH login on all application servers.
- Update the SSH configuration.
- Restart the SSH service.
- Verify that the configuration has been applied successfully.

---

## 🏗️ Infrastructure

| Server | Hostname |
|---------|----------|
| App Server 1 | `stapp01` |
| App Server 2 | `stapp02` |
| App Server 3 | `stapp03` |

---

# 🚀 Solution

## Step 1: Connect to the target server

### App Server 1

```bash
ssh tony@stapp01
sudo su -
```

### App Server 2

```bash
ssh steve@stapp02
sudo su -
```

### App Server 3

```bash
ssh banner@stapp03
sudo su -
```

---

## Step 2: Open the SSH configuration file

```bash
vi /etc/ssh/sshd_config
```

Locate the following line:

```text
PermitRootLogin yes
```

Replace it with:

```text
PermitRootLogin no
```

Save and exit the file.

---

## Step 3: Restart the SSH service

```bash
systemctl restart sshd
```

---

## Step 4: Verify the configuration

```bash
grep "^PermitRootLogin" /etc/ssh/sshd_config
```

### Expected Output

```text
PermitRootLogin no
```

Verify that the SSH service is running:

```bash
systemctl status sshd
```



#  Key Concepts Learned

- SSH Configuration
- Linux Security Best Practices
- Root Login Restriction
- Service Management
- Configuration Verification

---

# 💡 What I Learned

- The SSH server configuration is stored in `/etc/ssh/sshd_config`.
- The `PermitRootLogin` directive controls whether the root user can log in via SSH.
- Setting `PermitRootLogin no` disables direct root SSH access.
- Restarting the SSH service is required after modifying the configuration.
- Always verify the configuration after making security-related changes.

---


