# 📅 Day 10 - Linux Access Control Lists (ACL)

## 📝 Problem Statement

Following a security audit within the Stratos Datacenter, the Nautilus security team identified incorrect permissions on a critical system file. The task was to configure the Access Control Lists (ACLs) for the `/etc/hosts` file on **App Server 2** according to the security requirements.

---

# 🎯 Objective

- Connect to **App Server 2**.
- Change the file owner and group owner to `root`.
- Ensure **Others** have **read-only** permission.
- Remove all permissions for user **anita**.
- Grant **read-only** permission to user **jerome**.
- Verify all permission changes.

---

# 🏗️ Infrastructure

| Server | Hostname |
|---------|----------|
| App Server 2 | `stapp02` |

---

# Solution 
## Step 1: connect to App Server 2 

'''
ssh steve@stapp02
'''
---
## Step2: Switch to the Root User

'''
sudo su -
'''
---
## Step 3: Change the Ownership of File and Group
'''
chown root:root /etc/hosts
'''
---
## Step 4: Give Read-Only Permission to Others 
'''
chmod o-r /etc/hosts
'''
---
## Step 5: Remove All Permissions To User **anita**

***Here I need to browse how to remove all file permission to a specific user***

'''
setfacl -m u:anita:--- /etc/hosts
'''
---
## Step 6: Give Read-On Permission to User **jerome**
'''
setfacl -m u:jerome:r-- /etc/hosts
'''

---
## Step 7: Verify the ACL Configuration
'''
getfacl /etc/hosts
'''
### Recieved Output
'''
user:anita:---
user:jerome:r--
other::r--
'''
#  Commands Used

```
ssh
sudo su -
chown
chmod
setfacl
getfacl
```
# 🧠 Key Concepts Learned

- Linux Access Control Lists (ACL)
- File Ownership
- Standard Linux Permissions
- User-specific Permissions
- ACL Verification
