# Day -3 Backup Agent User with Non-Interactive Shell
## Problem Statement

The system administration team needed to create a dedicated service account for a backup agent. Since this account is intended only for running background services and should not allow interactive logins, it must be configured with a non-interactive shell

## Objective

a. Create a user named siva
b. Perform the task on App Server 2
c. Assign a non-interactive shell to the user

## Solution
Step 1: Connect to the target server

ssh steve@stapp02
sudo su - 

Step 2. Create the user named "siva"
useradd -s /sbin/nologin siva


-s → Specifies the login shell.
/sbin/nologin → Prevents interactive login while allowing the account to be used by services.

Step 3. Verify the user
id siva
grep "^siva:" /etc/passwd

 ## Key Concepts Learned
Service User Creation
Login Shell
Non-Interactive Shell
User Verification