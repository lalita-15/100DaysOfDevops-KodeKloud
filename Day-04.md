# Day 4 – Service User Creation without Home Directory

## Problem Statement

The system administrators at xFusionCorp Industries needed to create a dedicated service account for an application. Since the account is intended only for running background services, it should not have a home directory.

## Objective
Create a user named anita
Perform the task on App Server 2
Ensure that no home directory is created for the user.

# Solution 
Step 1: Connect to the target server
ssh steve@stapp02
 "Switch to the root user"
sudo su -

Step 2. Step 2: Create the service user without a home directory

useradd -M anita

-M :- Prevents the creation of a home directory

Step 3. Verify the user
id anita

"Check the user entry"

grep "^anita:" /etc/passwd

"Verify that no home directory exists"

ls -ld /home/anita

"Expected Output"

ls: cannot access '/home/anita': No such file or directory

# Key Concepts Learned
Service User Creation
Home Directory Management
User Verification
Linux User Administration