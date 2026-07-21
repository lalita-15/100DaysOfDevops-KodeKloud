# Day 21 - Troubleshooting Apache Service Unavailability

## Task

The monitoring system at xFusionCorp Industries reported that the Apache (`httpd`) service was unavailable on one of the application servers in the Stratos Datacenter.

### Objective

- Identify the faulty application server.
- Investigate why the Apache service failed.
- Resolve the issue.
- Ensure Apache is running successfully on all application servers.
- Verify Apache is listening on the required port 3003.

---

## Investigation

I connected to each application server using SSH and checked the Apache service status.

```
systemctl status httpd.service
```

On **App Server 1**, the Apache service was found in a **failed** state.

To identify the exact reason, I reviewed the service logs.

```
journalctl -xeu httpd
```

The logs indicated that Apache could not start because the required port was already occupied.

---

## Root Cause Analysis

To determine which process was using the port, I executed:

```
ss -tulpn | grep 3003
```

The output showed that the **Sendmail** service was already listening on the same port, causing a **port conflict** with Apache.

---

## Resolution

I stopped the Sendmail service to free the occupied port.

```
systemctl stop sendmail
```

After releasing the port, I restarted the Apache service.

```
systemctl restart httpd
```

Finally, I verified that the service was running correctly.

```
systemctl status httpd
```

---

## Verification

After fixing App Server 1, I checked the remaining application servers.

- App Server 1 – Apache running successfully
- App Server 2 – Apache already running
- App Server 3 – Apache already running

The issue existed only on **App Server 1**, and after resolving the port conflict, Apache started successfully on all servers.

---

## Commands Used

```bash
systemctl status httpd.service
journalctl -xeu httpd
ss -tulpn | grep 3003
systemctl stop sendmail
systemctl restart httpd
systemctl status httpd
```

---

## Concepts Learned

- Linux service troubleshooting
- Investigating failed services using `systemctl`
- Reading service logs with `journalctl`
- Identifying port conflicts using `ss`
- Resolving service conflicts
- Verifying service health across multiple servers

---

