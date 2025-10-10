# 🖥️ Server Management Guide

This guide provides step-by-step instructions for accessing servers, checking proxy services (SOCKS5 and HTTP), and managing system cache.

---

## ✅ Step 1: Log in to the Server

Use SSH to access the server:

```bash
ssh root@<server_ip_address> -p 22
```

## 🔎 Step 2: Check SOCKS5 Proxy (Danted)

Check the status of the Danted proxy service:
```bash
sudo systemctl status danted
```
⚠️ Only applicable to servers running a SOCKS5 proxy.

## 🔎 Step 3: Check HTTP/HTTPS Proxy (Squid)

Check the status of the Squid proxy service:
```bash
sudo systemctl status squid
```
If multiple Squid instances exist, use:
```bash
sudo systemctl status squid-*
```
⚠️ Only applicable to servers running an HTTP/HTTPS proxy.

## 🧹 Step 4: Clear System Cache
4.1 Check Current Memory and Cache Usage
```bash
free -h
```
4.2 Clear System Cache
```bash
sync; echo 3 > /proc/sys/vm/drop_caches
```
⚠️ This will drop page cache, dentries, and inodes. Use with caution.

## 🌐 Step 5: Verify Proxy Servers
✅ SOCKS5 Proxy Test
```bash
curl -x socks5://<username>:<password>@<proxy_ip>:<port> https://ifconfig.me
```
✅ HTTP/HTTPS Proxy Test
```bash
curl -x http://<username>:<password>@<proxy_ip>:<port> https://ifconfig.me
```
Example:
```bash
curl -x http://**:*****@98.***.158.**:3143 https://ifconfig.me
```
### 📌 Notes

Run proxy checks only on relevant servers.

Always verify network connectivity and proxy authentication.

Clearing cache may impact running services—ensure it's safe before execution.
