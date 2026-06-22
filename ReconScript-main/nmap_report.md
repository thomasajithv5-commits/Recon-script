# Network Infrastructure Scan Report (Nmap Option 1)

**Target IP Audited:** `192.168.122.117`  
**Target Hostname:** `metasploitable.localdomain`  
**Scan Engine Command:** `nmap -A -sV -p1-65535 192.168.122.117`  
**Environment Baseline:** QEMU Virtual Machine running Linux Kernel 2.6.x (Ubuntu 8.04 Base)

---

## 📊 Scan Overview & Port Statistics

* **Total Ports Probed:** 65,535 (Full TCP Port Range)
* **Closed Ports:** 65,505 returned a direct TCP Reset (`RST`) flag.
* **Active Discovered Sockets:** **30 ports are verified open**, representing an extraordinarily dense external attack surface.

---

## 🚨 Critical Service Vulnerabilities & Exploitation Risks

The aggressive service identification run exposed multiple severe, well-known legacy system flaws that allow for full host compromise:

### 1. Pre-Compromised Backdoors
* **Port 21 (vsftpd 2.3.4):** This software release contains a famous, historic backdoor. Sending specific syntax strings triggers an immediate root listener. Anonymous FTP access is also left fully open.
* **Port 6667 / 6697 (UnrealIRCd):** This IRC service version contains a trojanized backdoor sequence that executes arbitrary operating system commands when triggered over the network.
* **Port 1524 (Metasploitable Root Shell):** An unauthenticated bindshell listener is running openly on this port. Connecting via raw netcat (`nc`) drops any remote attacker directly into a root command prompt.

### 2. Unauthenticated Remote Code Execution (RCE)
* **Port 445 (Samba 3.0.20-Debian):** This implementation is highly vulnerable to command injection via shell metacharacters within username authentication parameters, leading to instant root system takeover.
* **Port 3632 (distccd v1):** The distributed compiler service is misconfigured to accept remote execution tasks without validating identity or tracking client authorizations.

### 3. Cleartext Communications & Network Sniffing
* **Port 23 (Linux telnetd):** Terminal management is running via unencrypted Telnet. All administrator usernames and password strings pass across the network layer in plain text, making them easily retrievable by a standard packet sniffer.

---

## 🔍 Database and Web Application Footprint

The host exposes primary database engines directly to the local network routing layer rather than restricting them to local application processes:
* **Port 3306 (MySQL 5.0.51a):** Exposed database port providing operational parameters, database salt data, and full handshake interaction capability.
* **Port 5432 (PostgreSQL 8.3):** Active database engine footprint using standard public-facing configurations.
* **Port 80 & 8180 (Apache Web Servers):** Running legacy instances of Apache `2.2.8` and an old Apache Tomcat `5.5` servlet engine, expanding application exploitation pathways.

---

## 🔒 Architectural Structural Weaknesses

```text
Host script results:
|_message_signing: disabled (dangerous, but default)
