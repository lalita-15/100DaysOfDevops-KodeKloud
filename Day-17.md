# Day 17 - Linux Administration & Bash Scripting

# Task 1: Set Process Limits for a User

## Objective

The application server was facing performance issues because the `nfsuser` account could create too many processes.

The goal was to configure process limits for this user by setting:

- Soft limit: 1027
- Hard limit: 2027

---

## What I Learned

- What soft and hard process limits are.
- How Linux controls the maximum number of processes a user can create.
- How to configure user limits using `/etc/security/limits.conf`.

---

## Steps I followed.
## Step 1 
```
sudo vi /etc/security/limits.conf
```

Added:

```
nfsuser soft nproc 1027
nfsuser hard nproc 2027
```

Verification:

```
grep nfsuser /etc/security/limits.conf
```

---

---

## Key Takeaways

- `soft` limit is the default working limit.
- `hard` limit is the maximum value allowed.
- Root permission is required to modify system configuration files.

---

# Task 2: Automate  Backup Using Bash Script

## Objective

Create a bash script that:

- Creates a zip archive of the website.
- Stores it in `/archives`.
- Copies the archive to the Nautilus Storage Server.
- Works without asking for a password.
- Does not use `sudo` inside the script.

---

## What I Learned

- How to automate backups using Bash scripting.
- How to create zip archives.
- How to copy files securely using `scp`.
- How passwordless SSH authentication works.
- Why automation should not require manual password entry.

---

## Script Created

```bash
#!/bin/bash

zip -r /archives/xfusioncorp_beta.zip /var/www/html/beta

scp /archives/xfusioncorp_beta.zip natasha@ststor01:/archives/
```

---

## Commands Used

Generate SSH key:

```bash
ssh-keygen -t rsa
```

Copy public key:

```bash
ssh-copy-id natasha@ststor01
```

Create script:

```
vi /scripts/beta_archive.sh
```

Make executable:

```
chmod +x /scripts/beta_archive.sh
```

Run script:

```
/scripts/beta_archive.sh
```

---

## Challenges I Faced

- At first, I copied the archive to the wrong server instead of the Storage Server.
- My script was asking for a password because passwordless SSH was not configured.
- After configuring SSH keys and updating the script, everything worked correctly.

---

## Key Takeaways

- `zip -r` is used to create compressed backups of directories.
- `scp` securely transfers files between Linux servers.
- SSH key authentication is essential for automation.
- Automation scripts should avoid manual intervention.
- Always verify server names, usernames, and destination paths before writing automation scripts.

---

# Day 17 Summary

Today I worked on two practical Linux administration tasks.

In the first task, I learned how to control user process limits using `/etc/security/limits.conf`, which helps improve system stability.

In the second task, I built a Bash script to automate website backups. I learned how to create zip archives, transfer files using `scp`, and configure passwordless SSH for fully automated backups.

