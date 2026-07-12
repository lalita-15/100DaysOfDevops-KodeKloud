# 🚀 Day 12 – Secure File Transfer & SELinux Configuration

##  Overview

Today's KodeKloud Engineer lab focused on **Linux security and system administration**. The tasks simulated real production scenarios where a system administrator is responsible for securely transferring sensitive files and configuring server security settings.

---

##  Task 1: Secure File Transfer using SCP

### Objective
A confidential file named `nautilus.txt.gpg` was stored on the **Jump Server**. Since developers did not have direct access to the application servers, the file had to be securely copied to **App Server 2** in the `/home/webdata` directory.

### Step1: Commands Used

```
scp /tmp/nautilus.txt.gpg banner@stapp02:/home/webdata/
```

### Step2: Verification

```
ssh banner@stapp02

ls -l /home/webdata/
```

### What I Learned

- How to use `scp` for secure file transfer.
- The role of a **Jump (Bastion) Server** in production environments.
- Verifying file transfer after copying.

---

## Task 2: Permanently Disable SELinux

### Objective

Install the required SELinux packages and configure SELinux to remain **disabled after the next reboot**. The current runtime status was not required to be changed.

## Solution

## Step1: Connect to the App Server2
```
ssh steve@stapp02
```


###  Step2: Install Required Packages

```
sudo yum install -y selinux-policy selinux-policy-targeted policycoreutils
```

### Step3: Update SELinux Configuration

Open the configuration file:

```
sudo vi /etc/selinux/config
```

Update the following line:

```text
SELINUX=disabled
```

### Step 4: Verification

```
grep '^SELINUX=' /etc/selinux/config
```

Expected Output:

```text
SELINUX=disabled
```

> **Note:** No reboot was required because the task specified that the change should take effect after the scheduled maintenance reboot.

---

#  Key Takeaways

- Secure file transfer using `scp`.
- Understanding the purpose of a Jump Server.
- Installing SELinux packages.
- Difference between runtime and persistent SELinux configuration.
- Editing `/etc/selinux/config` makes SELinux changes effective after reboot.

---

##  Commands Practiced

```bash
scp
ssh
ls
yum install
vi
grep
```

---

