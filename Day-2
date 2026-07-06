# Day 2 – Group Creation and User Assignment

## Problem Statement
The system administrators at xFusionCorp Industries decided to implement group-based access control to simplify user permission management across multiple application servers.

## Objective
a. Create a group named nautilus_sftp_users on all App Servers.
b. Add the user kano to the nautilus_sftp_users group.
c. If the user kano does not exist, create it first.

## Solution
Step 1: Connect to the server 

ssh tony@stapp01
sudo su -
**We'll repeat same process for others servers too stapp02 and stapp03**


Step 2. Check if the user exits or not

id kano 
**If the user does not exist, create user kano using useradd command:**
useradd kano

Step 3. Create the group "nautilus_sftp_users"

groupadd nautilus_sftp_users

Step 4. Add the user "kano" to the group "nautilus_sftp_users"

usermod -aG nautilus_sftp_users kano

-a stands for apend user in existing secondary group
-G Add user to a secondary group

Step 5. Verify the configuration
id kano
groups kano # check group membership
getent group nautilus_sftp_users           # Check group information

Key Concepts Learned:- 
Linux Group Management
Secondary Groups
Group-Based Access Control (RBAC)
User Verification
Managing users across multiple servers