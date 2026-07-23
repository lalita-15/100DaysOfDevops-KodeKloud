# Day 23 – Install and Configure Nginx with SSL (KodeKloud Engineer)

## 📌 Task

The DevOps team needed to prepare **App Server 1** for application deployment by:

- Installing and configuring Nginx.
- Deploying a self-signed SSL certificate.
- Creating a simple web page displaying **"Welcome!"**.
- Verifying HTTPS connectivity from the Jump Host.

---

## 🏢 Real-World Scenario

In production, applications are usually served through a web server such as **Nginx**.

Before an application goes live, a DevOps Engineer is responsible for:

- Installing the web server.
- Configuring HTTPS using SSL certificates.
- Deploying the application files.
- Verifying that the service is accessible from another server.

This lab simulates that real deployment process.

---

## 🛠️ Steps Performed

### 1. Installed Nginx

```bash
yum install -y nginx
```

---

### 2. Created SSL Directory

```bash
mkdir -p /etc/nginx/ssl
```

---

### 3. Moved SSL Certificate & Key

```bash
mv /tmp/nautilus.crt /etc/nginx/ssl/
mv /tmp/nautilus.key /etc/nginx/ssl/
```

---

### 4. Configured HTTPS

Created a new configuration file:

```bash
vi /etc/nginx/conf.d/ssl.conf
```

Configuration:

```nginx
server {
    listen 443 ssl;
    server_name stapp01;

    ssl_certificate /etc/nginx/ssl/nautilus.crt;
    ssl_certificate_key /etc/nginx/ssl/nautilus.key;

    root /usr/share/nginx/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

---

### 5. Created Website

```bash
echo "Welcome!" > /usr/share/nginx/html/index.html
```

---

### 6. Validated Configuration

```bash
nginx -t
```

Output:

```
syntax is ok
test is successful
```

---

### 7. Started Nginx

```bash
systemctl enable nginx
systemctl restart nginx
```

---

### 8. Verified HTTPS from Jump Host

```bash
curl -Ik https://stapp01/
```

Output:

```
HTTP/1.1 200 OK
Server: nginx
```

---

# 📂 Important Files

| File | Purpose |
|------|---------|
| `/etc/nginx/nginx.conf` | Main Nginx configuration |
| `/etc/nginx/conf.d/ssl.conf` | HTTPS virtual host configuration |
| `/etc/nginx/ssl/nautilus.crt` | SSL Certificate |
| `/etc/nginx/ssl/nautilus.key` | Private Key |
| `/usr/share/nginx/html/index.html` | Website homepage |

---

# 🧠 Concepts Learned

- What is Nginx?
- Difference between HTTP and HTTPS.
- Why SSL certificates are required.
- Purpose of a Private Key.
- Nginx Server Block configuration.
- Document Root in Nginx.
- How to validate Nginx configuration.
- Testing HTTPS using curl.

---

# 📖 Key Commands

```bash
yum install -y nginx
systemctl enable nginx
systemctl restart nginx
nginx -t
mkdir -p /etc/nginx/ssl
mv /tmp/nautilus.crt /etc/nginx/ssl/
mv /tmp/nautilus.key /etc/nginx/ssl/
echo "Welcome!" > /usr/share/nginx/html/index.html
curl -Ik https://stapp01/
```

---

# 💡 What I Learned Today

Today I learned how to deploy and configure an Nginx web server with HTTPS using a self-signed SSL certificate.

I understood how SSL certificates and private keys work together to secure web traffic, how Nginx serves content from its document root, and how to verify a secure deployment using `curl`.

This lab also gave me practical exposure to configuring a production-style web server, validating Nginx configuration files, and troubleshooting HTTPS services.

---

# 🎯 Interview Questions

### 1. What is Nginx?
A high-performance web server, reverse proxy, and load balancer.

### 2. What is the default document root in Nginx?
`/usr/share/nginx/html`

### 3. Why do we use SSL certificates?
To encrypt communication between clients and servers.

### 4. What is the difference between HTTP and HTTPS?

| HTTP | HTTPS |
|------|-------|
| Not encrypted | Encrypted |
| Port 80 | Port 443 |
| Less secure | More secure |

### 5. What does `nginx -t` do?
It validates the Nginx configuration before restarting the service.

### 6. Why is `curl -Ik` used?

- `-I` → Fetch only HTTP headers.
- `-k` → Ignore SSL certificate verification (useful for self-signed certificates).

---

