# 📅 Day 08 – Data Backup for Developer

## 📝 Problem Statement

The Jump Host server hosts a directory named `/data`, which stores non-confidential data for multiple developers. Developer **siva** requested a backup of their data stored in `/data/siva`.

The task was to create a compressed archive of the directory and place it in the `/home` directory on the Jump Host server.

---

## 🎯 Objective

- Create a compressed archive named **siva.tar.gz**.
- Archive the `/data/siva` directory.
- Store the archive in the `/home` directory.
- Verify that the archive has been created successfully.

---

## 🏗️ Infrastructure

| Server | Hostname |
|---------|----------|
| Jump Host | `jump-host` |

---

# 🚀 Solution

## Step 1: Switch to the root user

```bash
sudo su -
```

---

## Step 2: Create the compressed archive

```bash
tar -czf /home/siva.tar.gz -C /data siva
```

### Command Explanation

| Option | Description |
|---------|-------------|
| `tar` | Archive utility used to create and extract archives |
| `-c` | Creates a new archive |
| `-z` | Compresses the archive using gzip |
| `-f` | Specifies the archive filename |
| `-C /data` | Changes to the `/data` directory before archiving |
| `siva` | Directory to be archived |

---

## Step 3: Verify the archive

Check whether the archive was created successfully:

```bash
ls -lh /home/siva.tar.gz
```

View the contents of the archive without extracting it:

```bash
tar -tzf /home/siva.tar.gz
```

Expected Output:

```text
siva/
siva/...
```

---

---

# Key Concepts Learned

- Linux Backup
- tar Utility
- gzip Compression
- Archive Verification
- Linux File Management

---

# What I Learned

- The `tar` command is commonly used to create backups in Linux.
- The `-z` option compresses the archive using gzip, reducing its size.
- The `-C` option changes the working directory before creating the archive, helping maintain a cleaner directory structure.
- Always verify the archive after creating it to ensure the backup is valid.
