# Day 35 – Configure Apache2 in Docker Container

## Overview

Today's KodeKloud Engineer lab focused on Docker container management and Apache web server configuration.

The task simulated a real production scenario where a DevOps engineer needs to install and configure Apache inside a running Docker container.

Task

A Nautilus DevOps team member was working to configure services on a Docker container named kkcloud, running on App Server 3 (stapp03).

The following requirements had to be completed:

Install apache2 inside the kkcloud container using apt.

Configure Apache to listen on port 8089 instead of the default port 80.

Apache should not be bound to a specific IP address or hostname.

Make sure the Apache service is up and running.

Keep the kkcloud container in a running state at the end.

### Solution

Step 1: Connect to App Server 3

From the Jump Server, connect to App Server 3.

ssh banner@stapp03

Step 2: Check the Docker Container

Verify that the kkcloud container is running.

docker ps

The kkcloud container should be visible in the output.

Step 3: Enter the kkcloud Container

Open a shell inside the running container.

docker exec -it kkcloud /bin/bash

Now the remaining commands will be executed inside the container.

Step 4: Update Package Repository

Update the Ubuntu package repository.

apt update

Step 5: Install Apache2

Install Apache2 using the apt package manager.

apt install -y apache2

Verify the Apache installation.

apache2 -v

Step 6: Configure Apache to Listen on Port 8089

Apache normally listens on port 80.

Open the Apache ports configuration file:

vi /etc/apache2/ports.conf

Change:

Listen 80

to:

Listen 8089

Alternatively, use:

sed -i 's/^Listen 80$/Listen 8089/' /etc/apache2/ports.conf

Step 7: Configure Apache VirtualHost

Check the enabled Apache VirtualHost configuration:

grep -R "<VirtualHost" /etc/apache2/sites-enabled/

If you find:

<VirtualHost *:80>

change it to:

<VirtualHost *:8089>

You can make the change using:

sed -i 's/:80>/:8089>/g' /etc/apache2/sites-enabled/*.conf

Step 8: Verify Apache Configuration

Check the Apache configuration for syntax errors:

apache2ctl configtest

Expected output:

Syntax OK

Step 9: Start Apache Service

Start the Apache service:

service apache2 start

Check the Apache service status:

service apache2 status

Apache should be in a running state.

Step 10: Verify Apache Is Listening on Port 8089

Check whether Apache is listening on port 8089:

ss -lntp | grep 8089

Expected output should look similar to:

LISTEN 0 511 0.0.0.0:8089 0.0.0.0:*

This confirms that Apache is listening on port 8089.

Step 11: Test Apache

Test the Apache web server using curl:

curl http://localhost:8089

The Apache default page HTML should be displayed.

Step 12: Exit the Container

Exit from the Docker container:

exit

Step 13: Verify Container Status

Verify that the kkcloud container is still running:

docker ps

The container should show an Up status.