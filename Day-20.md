# Day 20 - Configure iptables Firewall Rules for Apache Security

##  Task

Secure the Apache application running on port **5003** by configuring **iptables** on all application servers.

### Requirements

- Install **iptables** and its dependencies on each application server.
- Allow incoming traffic on port **5003** **only** from the Load Balancer (LBR).
- Block all other incoming traffic on port **5003**.
- Ensure the firewall rules persist after a system reboot.

---

##  Solution
## Steps : Connect to App Server1

### 1. Install iptables and its dependencies

```
yum install -y iptables iptables-services
```

---

### 2. Find the Load Balancer IP

```
getent hosts stlb01
```

Example Output:

```
10.244.81.30 stlb01.ctz52asymj7smowd.svc.cluster.local
```

---

### 3. Allow Only the Load Balancer

```
iptables -I INPUT -p tcp -s 10.244.81.30 --dport 5003 -j ACCEPT
```

---

### 4. Block Everyone Else

```bash
iptables -A INPUT -p tcp --dport 5003 -j DROP
```

---

### 5. Verify Firewall Rules

```
iptables -S
```

Expected Output:

```
-A INPUT -s 10.244.81.30/32 -p tcp -m tcp --dport 5003 -j ACCEPT
-A INPUT -p tcp -m tcp --dport 5003 -j DROP
```

---

### 6. Save Rules Permanently

```bash
iptables-save > /etc/sysconfig/iptables
```

---

### 7. Restart and Enable iptables

``` 
systemctl restart iptables
systemctl enable iptables
```
##  Perform Same Steps on App Server 2,3 

---

## Result

- Installed **iptables** successfully.
- Allowed only the **Load Balancer** to access Apache on port **5003**.
- Blocked all other incoming traffic.
- Saved firewall rules permanently.
- Restarted and enabled the iptables service.

---

##  Key Learnings

- Learned how **iptables** works as a Linux firewall.
- Understood the purpose of the **INPUT** chain.
- Learned the difference between **ACCEPT** and **DROP** actions.
- Understood why firewall rule order matters.
- Learned how to retrieve the Load Balancer IP using `getent hosts`.
- Learned how to make firewall rules persistent after a reboot using `iptables-save`.

---

##  Commands Used

```
yum install -y iptables iptables-services

getent hosts stlb01

iptables -I INPUT -p tcp -s <LBR_IP> --dport 5003 -j ACCEPT

iptables -A INPUT -p tcp --dport 5003 -j DROP

iptables -S

iptables-save > /etc/sysconfig/iptables

systemctl restart iptables

systemctl enable iptables
```

---

### Concepts Covered

- Linux Firewall
- iptables
- INPUT Chain
- ACCEPT vs DROP
- Load Balancer Access Control
- Persistent Firewall Rules