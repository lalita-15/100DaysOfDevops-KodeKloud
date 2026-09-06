# Day 37 -- Hosting a Static Website Using Docker Compose

## Problem Statement

The Nautilus application development team shared static website content
that needs to be hosted on an httpd web server using a containerised
platform.

The task is to configure Docker Compose on App Server 1 in Stratos
DC and create an Apache HTTP Server container according to these
requirements:

Create the Docker Compose file at /opt/docker/docker-compose.yml.

Use the httpd:latest image.

The container name must be httpd.

Map host port 8087 to container port 80.

Mount /opt/devops on the host to /usr/local/apache2/htdocs
inside the container.

Do not modify existing data in these directories.

Start the container and verify it successfully.

## Solution Steps

### Step 1: Connect to App Server 1

ssh tony@stapp01


### Step 2: Navigate to /opt/docker

cd /opt/docker

Verify:

pwd

Expected output:

/opt/docker

### Step 3: Create the Required Docker Compose File

Create the file:

sudo vi docker-compose.yml

services:
  web:
    image: httpd:latest
    container_name: httpd
    ports:
      - "8087:80"
    volumes:
      - /opt/devops:/usr/local/apache2/htdocs


The required file path is:

/opt/docker/docker-compose.yml

### Step 4: Verify the Compose File

Make sure the image, container name, port mapping, and volume mapping
are correct.

### Step 5: Start the Container

From /opt/docker, run:

sudo docker compose up -d

Docker will pull httpd:latest if needed and create the container.

### Step 6: Verify the Running Container

sudo docker ps

Verify:

Container name: httpd

Image: httpd:latest

Status: Up

Port mapping: 8087:80

Expected mapping:

0.0.0.0:8087->80/tcp

Step 7: Test the Website

curl http://localhost:8087

If the configuration is correct, the Apache server should return the
static website content.

✅ Final Verification

Confirm all requirements:

✔ Docker Compose file: /opt/docker/docker-compose.yml
✔ Image: httpd:latest
✔ Container name: httpd
✔ Host port: 8087
✔ Container port: 80
✔ Host volume: /opt/devops
✔ Container volume: /usr/local/apache2/htdocs
✔ Container status: Running