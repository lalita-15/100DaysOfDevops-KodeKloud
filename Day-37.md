# Day-37:  Docker Network – Custom Bridge Network Configuration

### Overview

Today's KodeCloud Engineer task focused on creating a custom Docker bridge network with a specific subnet and IP range.

The requirement was to create a Docker network named news on App Server 2 (stapp02) with the following configuration:

Network Name: news

Driver: bridge

Subnet: 192.168.30.0/24

IP Range: 192.168.30.0/24

## Task Objective

Create a custom Docker network that can be used by containers for controlled communication with a predictable network configuration.

## Step 1: Connect to App Server 2

First, connect to the required application server:

ssh steve@stapp02

Verify Docker:

docker --version

## Step 2: Check Existing Docker Networks

Before creating the network, check the existing Docker networks:

docker network ls

This helps confirm whether the news network already exists.

## Step 3: Create the Custom Docker Network

Create the news network using the bridge driver with the required subnet and IP range:

docker network create   --driver bridge   --subnet 192.168.30.0/24   --ip-range 192.168.30.0/24   news

## Command Explanation

docker network create → Creates a new Docker network.

--driver bridge → Uses the Docker bridge network driver.

--subnet 192.168.30.0/24 → Defines the network subnet.

--ip-range 192.168.30.0/24 → Defines the IP allocation range.

news → Name of the Docker network.

## Step 4: Verify the Network Configuration

List the Docker networks:

docker network ls

The news network should now be visible.

Then inspect the network:

docker network inspect news

Verify the following configuration:

Driver: bridge
Subnet: 192.168.30.0/24
IPRange: 192.168.30.0/24

## What I Learned

Docker networks allow containers to communicate with each other in a controlled way.

A user-defined bridge network provides better control than the default bridge network.

--subnet defines the network address range.

--ip-range defines the range used for container IP allocation.

docker network inspect helps verify the network configuration.