##  Task 18: Install and Configure Tomcat Server
### Objective
Install and configure the Apache Tomcat server, change its default port, and deploy a Java web application.
---
## Task

- Install Tomcat Server on App Server 1.
- Configure Tomcat to run on **port 8089**.
- Copy the `ROOT.war` file from the Jump Host.
- Deploy the application on Tomcat.
- Verify that the application is accessible at:
  ```
  http://stapp01:8089
  ```

---
## Solution
## Step 1: Connect to App Server1
'''
ssh tony@stapp01
'''
## Step2: Install tomcat server on App server1
'''
yum install -y tomcat tomcat-webapps tomcat-admin-webapps
'''
## Step 3: Verify tomcat server
'''
rpm -qa | grep tomcat
'''
## St3p 4: Configure Tomcat Port

Edit the Tomcat configuration file:
'''
vi /etc/tomcat/server.xml
'''
change port 8080 with 8089 as mentioned
'''
Connector port="8080"
'''
## Step 5: Copy ROOT.war from Jump Host

On the stapp01 Host:
'''
scp /tmp/ROOT.war tony@stapp01:/tmp/
'''
## Step 6: Deploy the Application

Move the WAR file to Tomcat's webapps directory:

```
mv /tmp/ROOT.war /var/lib/tomcat/webapps/

```
## Step 7: Start tomcat server 
```bash
systemctl enable tomcat
```

Verify:

```
systemctl status tomcat
```

---

## Step 8: Test the Application

```bash
curl http://localhost:8089 or 
curl http://stapp01:8089
```
## Step 9: Output
'''
<h2>Welcome to xFusionCorp Industries!</h2>
'''

## What I Learned

- How to install Apache Tomcat on a Linux server.
- Difference between `server.xml` and `tomcat.conf`.
- How to change Tomcat's default listening port.
- What a `.war` (Web Application Archive) file is.
- Why `ROOT.war` is deployed at the base URL (`/`).
- How Tomcat automatically extracts and deploys WAR files.
- Basic verification of a deployed Java web application using `curl`.