# Day 2: Docker Container Deployment

## Objective
Deploy a specific version of an Nginx web server container on an application server following strict naming conventions.

## Task Details
* **Target Server:** Application Server 2
* **Container Name:** `nginx_2`
* **Docker Image:** `nginx`
* **Image Tag:** `alpine`
* **Target State:** Running (Detached mode)

---

## Step-by-Step Implementation

### 1. Verify Environment
Check if there are any existing containers with conflicting names or ports:
```
docker ps -a
```

### 2. Deploy the Container
Run the container using the specified detached mode, naming flag, and image tag:
```
docker run -d --name nginx_2 nginx:alpine
```

### 3. Verify Deployment
Confirm that the container is up and running successfully:
```
docker ps
```
*Expected Output:* You should see `nginx_2` listed with a status of `Up X seconds/minutes`.

---

## Key Takeaways
* **`-d` (Detached Mode):** Runs the container in the background, allowing the terminal to remain interactive.
* **`--name` Flag:** Explicitly names the container instead of allowing Docker to assign a random, automated name.
* **Image Tags (`:alpine`):** Specifies a lightweight, security-oriented Linux distribution version of the image to minimize resource footprint.
