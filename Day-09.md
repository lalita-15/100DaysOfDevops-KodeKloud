# Day 09 - Script Execution Permissions

## 📌 Problem Statement

The xFusionCorp Industries SysAdmin team developed a new bash script named **xfusioncorp.sh**. Although the script was distributed to the required server, it did not have executable permissions.

### Objective

- Connect to **App Server 1**.
- Grant executable permissions to `/tmp/xfusioncorp.sh`.
- Ensure that **all users** can execute the script.

---

# Solution

## Step 1: Connect to App Server 1

```bash
ssh tony@stapp01
```

## Step 2: Switch to the Root User

```bash
sudo su -
```

## Step 3: Navigate to the Script Location

```bash
cd /tmp
```

## Step 4: Verify the Script Exists

```bash
ls -l xfusioncorp.sh
```

## Step 5: Grant Execute Permission

```bash
chmod a+x xfusioncorp.sh
```

> If the task expects standard executable permissions, you can also use:

```bash
chmod 755 xfusioncorp.sh
```

## Step 6: Verify the Permissions

```bash
ls -l xfusioncorp.sh
```

### Expected Output

```text
-rwxr-xr-xc
```

---

# Command Explanation

### `chmod`

Changes file permissions.

### `a+x`

- `a` → All users (User, Group, Others)
- `+` → Add permission
- `x` → Execute permission

Meaning:

Grant execute permission to **everyone**.

---

# Key Concepts Learned

- Linux File Permissions
- Execute Permission (`x`)
- `chmod` Command
- User, Group and Others Permissions
- Script Execution
- Permission Verification using `ls -l`

---



### 1. What does `chmod` do?

It is used to change file or directory permissions.

---

### 2. What does `a+x` mean?

It grants execute permission to **all users** (user, group and others).

---

### 3. What is the difference between `chmod +x` and `chmod 755`?

- `chmod +x` adds only the execute permission while keeping existing permissions unchanged.
- `chmod 755` sets the permissions exactly to `rwxr-xr-x`.

---

### 4. How do you verify file permissions?

```bash
ls -l filename
```

---

### 5. What do the permission characters mean?

- `r` → Read
- `w` → Write
- `x` → Execute

---

# Commands Used

```bash
ssh tony@stapp01
sudo su -
cd /tmp
ls -l xfusioncorp.sh
chmod a+x xfusioncorp.sh
chmod 755 xfusioncorp.sh
ls -l xfusioncorp.sh
```

---

# What I Learned Today

- How to grant execute permissions to shell scripts.
- Difference between symbolic and numeric permission methods.
- Importance of execute permission for running shell scripts.
- How to verify permission changes using `ls -l`.
- Real-world usage of `chmod` in Linux administration.