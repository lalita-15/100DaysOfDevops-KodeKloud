# Day 5 – Temporary User Setup with Expiry
## Problem Statement

The system administrators at xFusionCorp Industries needed to provide temporary access to a developer working on a short-term project. To ensure the account is automatically disabled after the project ends, the user account must be created with an expiry date.

# Objective
a. Create a user named ravi
b. Perform the task on App Server 1
c. Set the account expiry date to 2027-01-28

# Solution
Step 1. Connect to the target server
ssh tony@stapp01
"Switch to the root user"
sudo su -

Step 2. Create the temporary user
useradd -e 2027-01-28 ravi

# -e → Sets the account expiry date. 
# 2027-01-28 → Expiry date in YYYY-MM-DD format.

Step 3. Verify the user
id ravi 

"Check the account expiry"

chage -l ravi

# What I Learned
Linux allows us to create temporary user accounts with an expiry date.
The -e option in useradd automatically disables the account after the specified date.
Using temporary accounts improves security by preventing unnecessary long-term access.
Always verify user details after account creation.