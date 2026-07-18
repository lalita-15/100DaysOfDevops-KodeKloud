# Day 01 - Install Docker CE and Docker Compose

## Objective

Install Docker CE and Docker Compose on App Server 1 and start the Docker service.

---

## Task

- Install Docker CE.
- Install Docker Compose.
- Start and enable the Docker service.
- Verify the installation.

---
## Solution: 
## Step 1: Install Required Utilities

```
yum install -y yum-utils

yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
'''

## Step 2: Install Docker CE

```bash
yum install -y docker-ce docker-ce-cli containerd.io
```

---

## Step 4: Install Docker Compose

```
yum install -y docker-compose
```

---

## Step 5: Start and Enable Docker

```bash
systemctl enable docker
```

Verify the service:

```bash
systemctl status docker
```

---

## Step 6: Verify Installation

Check Docker version:

```bash
docker --version
```

Check Docker Compose version:

```bash
docker compose version
```

---

# What I Learned

- How to install Docker CE on a Linux server.
- How to configure the official Docker repository.
- Difference between Docker Engine and Docker Compose.
- How to start and enable Docker using `systemctl`.
- How to verify Docker and Docker Compose installations.

---

