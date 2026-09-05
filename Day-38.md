# Docker Image Transfer Between Servers

## Overview

Today's KodeCloud Engineer task focused on transferring a Docker image from one application server to another.

A custom Docker image named official:datacenter was already available on App Server 1 (stapp01). The requirement was to make the same image available on App Server 3 (stapp03) with the same repository name and tag.

The image was transferred using a Docker archive instead of a container registry.

### Task Objective

The requirements were:

Save official:datacenter as an archive on App Server 1.

Transfer the archive to App Server 3.

Load the archive on App Server 3.

Keep the image name and tag as official:datacenter.

## Step 1: Connect to App Server 1

Connect to App Server 1:

ssh tony@stapp01

Check Docker:

docker ps

If Docker service is down:

sudo systemctl start docker

Verify the required image:

docker images

The image should be available as:

official   datacenter

## Step 2: Save the Docker Image as an Archive

Use docker save to create an archive:

docker save -o /tmp/official-datacenter.tar official:datacenter

## Verify the archive:

ls -lh /tmp/official-datacenter.tar

Why docker save?

docker save exports a Docker image, including its layers and repository/tag information, into a tar archive.

It should not be confused with docker export, which exports a container's filesystem.

## Step 3: Transfer the Archive to App Server 3

Use scp to transfer the archive:

scp /tmp/official-datacenter.tar banner@stapp03:/tmp/

Then connect to App Server 3:

### ssh banner@stapp03

## Step 4: Verify Docker on App Server 3

### Check Docker:

docker ps

If Docker service is down:

sudo systemctl start docker

## Verify that the transferred archive exists:

ls -lh /tmp/official-datacenter.tar

Step 5: Load the Image Archive

Load the image:

docker load -i /tmp/official-datacenter.tar

## Expected output:

Loaded image: official:datacenter

## Step 6: Verify the Image

Run:

docker images