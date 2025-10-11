# 🧩 SOCKS5 & HTTP Proxy Setup Guide (Dante + Squid)

This repository provides configuration and setup instructions for running **SOCKS5** and **HTTP(S)** proxy servers using **Dante** and **Squid** on Linux.  
Easily deploy your own proxy servers for secure, controlled, and auditable traffic routing.

---

## 🚀 Features

- ✅ SOCKS5 Proxy (via **Dante**)
- ✅ HTTP / HTTPS Proxy (via **Squid**)
- ✅ Supports authentication (optional)
- ✅ IPv4 & IPv6 support
- ✅ Auto-start on boot (systemd)
- ✅ Easy configuration for multiple users or IP restrictions

---

## 🧰 Requirements

- Linux (Ubuntu / Debian / CentOS recommended)
- Root or sudo privileges
- Internet connection

---

## ⚙️ Installation

### 1. Update System

```bash
sudo apt update && sudo apt upgrade -y
```

## 🌐 HTTP Proxy (Squid)
Install Squid
```bash
sudo apt install squid -y
```

### Configuration File Path
```bash
/etc/squid/squid.conf
```

### Example Configuration
```bash
http_port 3128
visible_hostname proxy-server
# Allow localhost and specific IPs
acl allowed_ips src 127.0.0.1/32 192.168.1.0/24
http_access allow allowed_ips
http_access deny all

# Optional: Enable basic authentication
auth_param basic program /usr/lib/squid/basic_ncsa_auth /etc/squid/passwd
auth_param basic realm ProxyAuth
acl authenticated proxy_auth REQUIRED
http_access allow authenticated

# Logging
access_log /var/log/squid/access.log
cache_log /var/log/squid/cache.log
```

### Create Authentication File (Optional)
```bash
sudo apt install apache2-utils -y
sudo htpasswd -c /etc/squid/passwd username
```

### Restart Squid
```bash
sudo systemctl restart squid
sudo systemctl enable squid
```
### Test HTTP Proxy
```bash
curl -x http://your-server-ip:3128 -U username:password http://api.ipify.org
```

## 🧦 SOCKS5 Proxy (Dante)
### Install Dante Server
```bash
sudo apt install dante-server -y
```

### Configuration File Path
```bash
/etc/danted.conf
```

### Example Configuration
```bash
logoutput: /var/log/danted.log
internal: eth0 port = 1080
external: eth0

# Client access
method: username none
user.notprivileged: nobody

client pass {
    from: 0.0.0.0/0 to: 0.0.0.0/0
    log: connect disconnect error
}

# Authentication rules
pass {
    from: 0.0.0.0/0 to: 0.0.0.0/0
    protocol: tcp udp
    log: connect disconnect error
    method: username none
}
```
### Create Dante User (Optional Authentication)
```bash
sudo useradd -r -s /bin/false proxyuser
sudo passwd proxyuser
```

Then update the config:
```bash
method: username
```
### Restart Dante
```bash
sudo systemctl restart danted
sudo systemctl enable danted
```
### Test SOCKS5 Proxy
```bash
curl -x socks5://your-server-ip:1080 -U proxyuser:password http://api.ipify.org
```
## 🔒 Firewall Configuration

### Allow proxy ports in your firewall:
```bash
sudo ufw allow 3128/tcp
sudo ufw allow 1080/tcp
sudo ufw reload
```
## 🧩 Verify

### Check services:
```bash
sudo systemctl status squid
sudo systemctl status danted
```

## Check proxy IP:
```bash
curl -x http://your-server-ip:3128 http://api.ipify.org
curl -x socks5://your-server-ip:1080 http://api.ipify.org
```
### 🧹 Logs
Service	Log File
Squid	`/var/log/squid/access.log`
Dante	`/var/log/danted.log`

### 🧠 Tips

Change default ports to increase security.

Use strong credentials for authentication.

Limit IPs in acl or client pass rules.

Combine with iptables for advanced traffic control.

### 🧰 Useful Commands
Description	Command
Restart all proxies	`sudo systemctl restart squid danted`
Check logs	`tail -f /var/log/squid/access.log /var/log/danted.log`
Test HTTP proxy	`curl -x http://127.0.0.1:3128 http://api.ipify.org`
Test SOCKS5 proxy	`curl -x socks5://127.0.0.1:1080 http://api.ipify.org`
