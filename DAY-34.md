# KodeKloud Task: Copy Encrypted File to Docker Container

## Task

The Nautilus DevOps team has confidential data on **App Server 1** in the **Stratos Datacenter**.

A container named `ubuntu_latest` is running on the same server.

The task was to copy the encrypted file `/tmp/nautilus.txt.gpg` from the Docker host to the `ubuntu_latest` container at `/opt/` and ensure that the file is not modified during the operation.

---

## Steps Performed

### 1. Connect to App Server 1

From the Jump Host, I connected to App Server 1 using SSH:

```bash
ssh tony@stapp01
```

After entering the password, I was logged in as user `tony` on App Server 1.

---

### 2. Copy the encrypted file to the container

Used `docker cp` to copy `/tmp/nautilus.txt.gpg` from the Docker host to the `ubuntu_latest` container under `/opt/`:

```bash
docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/opt/
```

Output:

```text
Successfully copied 2.05kB to ubuntu_latest:/opt/
```

This confirmed that the file was successfully copied.

---

### 3. Initially tried to check MD5 checksum

I first ran:

```bash
md5sum nautilus.txt.gpg
```

It returned:

```text
md5sum: nautilus.txt.gpg: No such file or directory
```

The error occurred because the file was located at `/tmp/nautilus.txt.gpg`, not in the current directory.

---

### 4. Check the original file's MD5 checksum

I then used the correct path:

```bash
md5sum /tmp/nautilus.txt.gpg
```

Output:

```text
eed23c2959d3961a0145cbcdfe5973c6  /tmp/nautilus.txt.gpg
```

This checksum represents the original file's integrity.

---

### 5. Check the copied file's MD5 checksum inside the container

I used `docker exec` to run `md5sum` inside the `ubuntu_latest` container:

```bash
docker exec ubuntu_latest md5sum /opt/nautilus.txt.gpg
```

Output:

```text
eed23c2959d3961a0145cbcdfe5973c6  /opt/nautilus.txt.gpg
```

---

## Verification

Original file checksum:

```text
eed23c2959d3961a0145cbcdfe5973c6
```

Copied file checksum:

```text
eed23c2959d3961a0145cbcdfe5973c6
```

Both checksums are **identical**.

Therefore, the encrypted file was copied successfully to:

```text
/opt/nautilus.txt.gpg
```

inside the `ubuntu_latest` container without modification.

## Final Commands

```bash
ssh tony@stapp01

docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/opt/

md5sum /tmp/nautilus.txt.gpg

docker exec ubuntu_latest md5sum /opt/nautilus.txt.gpg
```
## md5sum Command Used:- 
* **`md5sum`**: It creates a unique **digital fingerprint (checksum)** of a file.
* **Why we used it:** To verify that the file was **not changed during copying**.
* **How we verify:** Run `md5sum` on the **original file** and the **copied file**. If both MD5 values are **exactly the same**, the file was not modified.
