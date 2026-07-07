# Day 6 – Linux User Data Transfer
## Problem Statement

The system administrators at xFusionCorp Industries needed to migrate user-owned files from one location to another while preserving the original directory structure. The task required transferring only the files owned by a specific user without copying unnecessary files or directories.

## Objective
Perform the task on App Server 1
Find all regular files owned by ammar
Search inside the /home/usersdata directory
Copy the files to /commerce
Preserve the original directory structure during the copy operation

## Solution

Step 1. Connect to the target server
ssh tony@stapp01
"switch to the root user"
sudo su -

Step 2. Find all files owned by user "ammar"
find /home/usersdata -type f -user ummar

"find → Searches for files and directories.
/home/usersdata → Directory where the search begins.
-type f → Returns only regular files.
-user ammar → Filters files owned by the user ammar."

Step 3. Copy files while preserving the directory structure
find /home/usersdata -type f -user ammar -exec cp --parents {} /commerce \;

-exec:- Executes a command on every file returned by find
cp:- Copies the file
--parents:-	Preserves the original directory structure
{}:-	Represents the current file found by find
/commerce:-	Destination directory
\;:-Marks the end of the -exec command