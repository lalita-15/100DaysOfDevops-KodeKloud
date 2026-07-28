# Day 20 - Host Multiple Static Websites on Apache(httpd) 

## 🎯 Lab Objective

The objective of this lab was to learn how to configure an Apache HTTP Server to host **multiple static websites** on a **single web server** using different URL paths. This is a common real-world scenario where organizations host multiple web applications on the same server while using a custom port.

---

## 📝 Task Requirements

- Install the Apache (`httpd`) package and its dependencies on **App Server 2**.
- Configure Apache to listen on **port 8088** instead of the default port 80.
- Copy the two website backups (`ecommerce` and `demo`) from the Jump Host.
- Deploy both websites under Apache's default web root.
- Ensure the following URLs are accessible:
  - `http://localhost:8088/ecommerce/`
  - `http://localhost:8088/demo/`
- Verify the websites using the `curl` command.

---

## 🛠️ Steps Performed

### 1. Connected to App Server 2

```bash
ssh steve@stapp02
```

### 2. Installed Apache

```bash
sudo yum install -y httpd
```

---

### 3. Configured Apache to Listen on Port 8088

Edited the Apache configuration file:

```bash
sudo vi /etc/httpd/conf/httpd.conf
```

Modified:

```apache
Listen 80
```

to

```apache
Listen 8088
```

---

### 4. Copied Website Backups from Jump Host

From the Jump Host:

```bash
scp -r /home/thor/ecommerce steve@stapp02:/tmp/
scp -r /home/thor/demo steve@stapp02:/tmp/
```

---

### 5. Deployed Websites

```bash
sudo cp -r /tmp/ecommerce /var/www/html/
sudo cp -r /tmp/demo /var/www/html/
```

---

### 6. Set Proper Ownership and Permissions

```bash
sudo chown -R apache:apache /var/www/html/ecommerce
sudo chown -R apache:apache /var/www/html/demo

sudo chmod -R 755 /var/www/html/ecommerce
sudo chmod -R 755 /var/www/html/demo
```

---

### 7. Started and Enabled Apache

```bash
sudo systemctl enable httpd
sudo systemctl restart httpd
```

---

### 8. Verified the Deployment

```bash
curl http://localhost:8088/ecommerce/
```

```bash
curl http://localhost:8088/demo/
```

Both commands returned the respective website content successfully.

---

## 📂 Directory Structure

```
/var/www/html/
├── ecommerce/
│   └── index.html
└── demo/
    └── index.html
```

---

## 💡 What I Learned

- Installing and configuring Apache HTTP Server.
- Changing Apache's default listening port.
- Hosting multiple static websites on a single Apache server.
- Deploying website files into Apache's document root.
- Managing file ownership and permissions for Apache.
- Verifying web applications using the `curl` command.
- Understanding how Apache serves different applications using URL paths.

---

## 🎯 Lab Motive

This lab was designed to demonstrate how a single Apache web server can host multiple static websites by organizing them into separate directories and serving them through different URL paths. It also reinforced essential DevOps skills such as web server installation, configuration management, file deployment, permission handling, service management, and application validation using command-line tools.

---

## ✅ Outcome

Successfully configured Apache on **App Server 2** to listen on **port 8088** and hosted two independent static websites:

- ✅ `http://localhost:8088/ecommerce/`
- ✅ `http://localhost:8088/demo/`

Both websites were accessible and verified successfully using the `curl` command.