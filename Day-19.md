# Day 19 - Apache Service & Network Troubleshooting (KodeKloud Engineer)

## Objective
Troubleshoot an Apache (`httpd`) service that was not accessible from the jump host and restore connectivity on the required port.

### Problem
The monitoring tool reported that the Apache service was unreachable on **port 5003** . The service was down and inaccessible from the **jump-host**.

## Troubleshooting Process

### 1. Checked the Apache service status on App Server 1 
```
sudo systemctl status httpd
```
The service was **not running**.

### 2. Tried to start the service
```
sudo systemctl start httpd
```
The service failed to start.

### 3. Checked the logs
```
sudo journalctl -xeu httpd
```
The logs showed:
```
Address already in use
```
which indicated a **port conflict**.

### 4. Identified the process using the port
```
sudo ss -tulpn | grep 5003
```
The output showed that the **sendmail** service was already occupying the required port.

### 5. Stopped the conflicting service
```
sudo systemctl stop sendmail
```

Verified the port again:
```
sudo ss -tulpn | grep 5003
```
No output confirmed that the port was now free.

### 6. Started Apache again
```
sudo systemctl start httpd
```
Apache started successfully.

### 7. Verified locally
```
curl http://stapp01:5003
```
The application was accessible from the local server.

### 8. Tested from the Jump Host
```
curl http://stapp01:5003
```
It returned **"No route to host"**, indicating a **network/firewall issue**.

### 9. Checked iptables rules
```
sudo iptables -S
```
Only **SSH (port 22)** traffic was allowed.

### 10. Allowed the Apache port
```
sudo iptables -I INPUT -p tcp --dport 5003 -j ACCEPT
```

### 11. Verified the fix
```
curl http://stapp01:5003
```
The application became accessible from the jump host, and the task passed successfully.

---

## Root Cause
- Apache service was not running.
- The required port was occupied by the **sendmail** service.
- **iptables** blocked incoming traffic to the Apache port, preventing access from the jump host.

## Key Learnings
- Use **journalctl** to troubleshoot service startup failures.
- Check for **port conflicts** using `ss -tulpn`.
- Ensure the required port is free before starting a service.
- A running service is not enough—always verify **network accessibility**.
- **iptables** rules can block application traffic even when the service is healthy.
- Always validate the application from the **client (jump host)** after applying fixes.