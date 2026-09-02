# 🚀 Day 36 – Build a Custom Apache2 Docker Image

## 📌 Problem Statement

The Nautilus application development team needed a **custom Docker image** for one of their projects.

The requirement was to create a Dockerfile on **App Server 1 (`stapp01`)** and use it to build a custom image with **Apache2 installed and configured to work on port `8085`**.

The Dockerfile had to be created at:

```text
/opt/docker/Dockerfile
```

The existing Apache configuration should not be changed except for the required port configuration.

---

## 🎯 Objective

The task required us to:

- Create `/opt/docker/Dockerfile`.
- Use `ubuntu:24.04` as the base image.
- Install `apache2`.
- Configure Apache to listen on port `8085`.
- Keep other Apache configuration settings unchanged.
- Build a Docker image using the Dockerfile.

---

## 🛠️ Solution

### Step 1: Connect to App Server 1

From the Jump Server, connect to App Server 1:

```bash
ssh tony@stapp01
```

---

### Step 2: Go to the Required Docker Directory

Navigate to `/opt/docker`:

```bash
cd /opt/docker
```

Verify the current directory:

```bash
pwd
```

Expected output:

```text
/opt/docker
```

---

### Step 3: Create the Dockerfile

Create the required Dockerfile:

```bash
sudo vi /opt/docker/Dockerfile
```

Add the following content:

```dockerfile
FROM ubuntu:24.04

RUN apt-get update && \
    apt-get install -y apache2 && \
    sed -i 's/^Listen 80$/Listen 8085/' /etc/apache2/ports.conf && \
    sed -i 's/<VirtualHost \*:80>/<VirtualHost *:8085>/' /etc/apache2/sites-enabled/000-default.conf

EXPOSE 8085

CMD ["apache2ctl", "-D", "FOREGROUND"]
```

Save and exit Vim:

```text
Esc
:wq
```

---

### Step 4: Verify the Dockerfile

Check the Dockerfile:

```bash
cat /opt/docker/Dockerfile
```

Verify that the following requirements are present:

```dockerfile
FROM ubuntu:24.04
```

Apache installation:

```dockerfile
apt-get install -y apache2
```

Apache port:

```text
Listen 8085
```

VirtualHost:

```text
<VirtualHost *:8085>
```

---

### Step 5: Understand the Port Configuration

Apache normally listens on port `80`.

The task requires Apache to work on port `8085`.

Therefore, the Dockerfile changes:

```text
Listen 80
```

to:

```text
Listen 8085
```

The default VirtualHost is also changed from:

```text
<VirtualHost *:80>
```

to:

```text
<VirtualHost *:8085>
```

No other Apache configuration such as the document root is modified.

---

### Step 6: Build the Docker Image

Go to the Dockerfile directory:

```bash
cd /opt/docker
```

Build the image:

```bash
docker build -t apache:8085 .
```

The `.` tells Docker to use the current directory as the build context.

During the build, Docker will:

1. Pull `ubuntu:24.04`.
2. Install Apache2.
3. Configure Apache to use port `8085`.
4. Create the custom Docker image.

---

### Step 7: Verify the Docker Image

After the build completes, check the available images:

```bash
docker images
```


---

### Step 8: Verify the Dockerfile Location

Confirm that the Dockerfile exists at the required location:

```bash
ls -l /opt/docker/Dockerfile
```

The file should be present:

```text
/opt/docker/Dockerfile
```

---

## 🔍 Important Dockerfile Instructions

### `FROM`

```dockerfile
FROM ubuntu:24.04
```

Uses Ubuntu 24.04 as the base image.

### `RUN`

```dockerfile
RUN apt-get update && \
    apt-get install -y apache2
```

Updates the package repository and installs Apache2 while building the image.

### Apache Port Configuration

```dockerfile
sed -i 's/^Listen 80$/Listen 8085/' /etc/apache2/ports.conf
```

Changes Apache's listening port from `80` to `8085`.

### VirtualHost Configuration

```dockerfile
sed -i 's/<VirtualHost \*:80>/<VirtualHost *:8085>/' /etc/apache2/sites-enabled/000-default.conf
```

Updates the default VirtualHost to use port `8085`.

### `EXPOSE`

```dockerfile
EXPOSE 8085
```

Documents that the container is intended to use port `8085`.

### `CMD`

```dockerfile
CMD ["apache2ctl", "-D", "FOREGROUND"]
```

Runs Apache in the foreground so that the container can remain running.

---

## 💡 Why Do We Use a Custom Docker Image?

Instead of manually installing and configuring Apache every time a container is created, we can define everything inside a **Dockerfile**.

This provides:

- Repeatable deployments
- Consistent configuration
- Faster container creation
- Easier application deployment
- Less manual configuration

In this task, every container created from the custom image will already have Apache2 installed and configured for port `8085`.

---

## 🧪 Verification

Check the image:

```bash
docker images
```

Check the Dockerfile:

```bash
cat /opt/docker/Dockerfile
```

Check the Dockerfile location:

```bash
ls -l /opt/docker/Dockerfile
```

The final setup should have:

```text
Server: stapp01
Dockerfile: /opt/docker/Dockerfile
Base Image: ubuntu:24.04
Web Server: Apache2
Apache Port: 8085
Docker Image: Successfully Built
```

---

## 📝 Commands Practiced

```bash
ssh
cd
pwd
vi
cat
ls
docker build
docker images
```

---

## 🧠 What I Learned

- How to create a custom Docker image using a Dockerfile.
- How to use `ubuntu:24.04` as a Docker base image.
- How to install Apache2 during the image build.
- How to configure Apache to use a custom port.
- The difference between Docker's `EXPOSE` instruction and Apache's actual `Listen` configuration.
- How to build and verify a Docker image.
- Why Dockerfiles are useful for creating repeatable environments.
- Why following the exact file path and task requirements is important in DevOps.

---

## ✅ Final Result

The required Dockerfile was successfully created at:

```text
/opt/docker/Dockerfile
```

The Dockerfile uses:

```text
ubuntu:24.04
```

Apache2 was installed and configured to use:

```text
Port 8085
```

The custom Docker image was successfully built using:

```bash
docker build -t apache:8085 .
```

The image was verified using:

```bash
docker images
```
