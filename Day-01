# Day 1 - Custom Apache User Creation

## Scenario

The security team required a dedicated Apache user for a web application to improve security and isolate application access.

## Objective

- Create a user named `yousuf`
- Assign UID `1931`
- Set the home directory to `/var/www/yousuf`

## Steps Performed

1. Connected to the target server


ssh banner@stapp03
sudo su -

2.  Created User
 
 useradd yousuf

3. Updated the user's UID and home directory

usermod -u 1931 -d /var/www/yousuf -m yousuf

4.  Verified the configuration

id yousuf
grep "^yousuf:" /etc/passwd


What I Learned
Creating Linux users
Assigning custom UIDs
Changing home directories
Verifying user configuration