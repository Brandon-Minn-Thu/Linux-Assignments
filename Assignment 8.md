# Assignment 8 (Firewall)

For this assignment, we were tasked to make a firewall for the servers that loads when we start our servers.

## Firewall Setup  
The firewall was configured using to secure the server.

### Permitted Services

#### SSH (OpenSSH Server) 

**Command:**  
```
sudo ufw limit ssh
```

**Explanation:**  
- Enables remote access via SSH on port 22.  
- The `limit` option restricts the rate of incoming connections, helping to defend against brute-force login attempts and SYN flood attacks.

#### Web Server (HTTP)  

**Command:**  
```
sudo ufw limit http
```

**Explanation:**  
- Allows incoming traffic on port 80 (TCP).  
- This makes the web server accessible to users over standard HTTP.

#### Secure Web Server (HTTPS)  

**Command:**  
```
sudo ufw limit https
```

**Explanation:**  
- Opens port 443 (TCP) for encrypted communication.  
- Ensures secure data transfer between clients and the server.

---

## Logging Setup

**Command:**  
```
sudo ufw logging medium
```

**Explanation:**  
- Activates firewall logging at a medium level.  
- Captures blocked traffic and new connection attempts.  
- Useful for identifying suspicious behavior, debugging, and monitoring network activity.

**Log file location:**  
```
/var/log/ufw.log
```

---

## Protection Against SYN Flood Attacks

**Command:**  
```
sudo ufw limit ssh
```

**Explanation:**  
- Controls the rate of incoming TCP connection requests.  
- Helps prevent resource exhaustion caused by excessive half-open connections during a SYN flood attack.

---

## Additional Security Measures

### SSH Brute-Force Defense

**Command:**  
```
sudo ufw limit ssh
```

**Explanation:**  
- Detects repeated login attempts from the same IP address.  
- Temporarily blocks further attempts if the rate exceeds allowed limits.

---

## Checking Firewall Status

To confirm the configuration, the following command was used:

```
sudo ufw status verbose
```

**Resulting configuration includes:**
- Incoming traffic: denied by default  
- Outgoing traffic: allowed by default  
- SSH: rate-limited  
- HTTP and HTTPS: permitted  
- Logging: enabled (medium level)

## Image
![alt text](<Screenshot 2026-03-19 at 2.09.53 PM.png>)