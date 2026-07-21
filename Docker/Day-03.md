# Day 3 - Copy File from Docker Host to Running Container

## Task

The Nautilus DevOps team had a confidential encrypted file located on the Docker host:

```text
/tmp/nautilus.txt.gpg
```

A running container named **ubuntu_latest** required this file to be copied into:

```text
/opt/
```

The file had to remain unchanged during the transfer.

---

## Objective

* Copy an encrypted file from the Docker host to a running Docker container.
* Preserve the file without modifying its contents.
* Verify that the file was successfully copied.

---

## Command Used

```bash
docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/opt/
```

---

## Verification

```bash
docker exec ubuntu_latest ls -l /opt/nautilus.txt.gpg
```

---

## Output

The encrypted file was successfully copied to:

```text
/opt/nautilus.txt.gpg
```

inside the **ubuntu_latest** container.

---

## Concepts Learned

* Docker container file management
* Using the `docker cp` command
* Copying files between the Docker host and a running container
* Verifying files inside a container with `docker exec`

---

## Key Takeaway

`docker cp` provides a simple and secure way to transfer files between the Docker host and containers without altering the original file, making it useful for configuration files, backups, logs, and encrypted data.
