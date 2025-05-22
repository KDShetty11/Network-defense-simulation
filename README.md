# Network Defense Simulation Project

Kurudunje Deekshith Shetty 

---

## 🚀 Overview

This project demonstrates the **design and implementation of network defensive technologies** to protect systems, services, and protocols from common cyber attacks. Using VirtualBox, we simulate a network with multiple VMs, launch targeted attacks, and implement firewall and IDS/IPS rules to mitigate them.

---

## 🖥️ Network Architecture

Four Virtual Machines (VMs) are deployed:


| VM Name | OS/Type | IP Address | Network |
| :-- | :-- | :-- | :-- |
| **pfSense** | Firewall | WAN: 10.0.2.15<br>LAN: 192.168.213.100 | WAN: NAT WAN<br>LAN: Host Only |
| **Security Onion** | Ubuntu (NIDS) | 192.168.213.105 | Host Only |
| **Kali (Attacker)** | Kali Linux | 10.0.2.20 | NAT WAN |
| **CSEC (Host)** | Ubuntu | 192.168.213.109 | Host Only |

**Network Topology:**

- **WAN (NAT):** External network for attacker and firewall WAN interface.
- **LAN (Host Only):** Internal network for firewall LAN, NIDS, and host machine.

---

## 🛠️ Setup Instructions

### 1. **Virtual Machine Deployment**

- Install [VirtualBox](https://www.virtualbox.org/) and create the four VMs as per the table above.
- Configure network adapters for each VM:
    - **pfSense:** Two adapters (NAT for WAN, Host Only for LAN)
    - **Security Onion \& CSEC:** Host Only
    - **Kali:** NAT


### 2. **Network Configuration**

- Assign the specified static IPs to each VM.
- Ensure **pfSense** acts as the gateway between WAN and LAN.
- Verify connectivity (ping between VMs as appropriate).


### 3. **Service Setup**

- On **CSEC (Host):**
    - Install and run vulnerable **ProFTPD 1.3.3c** (FTP server).
    - Host a basic HTTP web page.
- On **Security Onion:**
    - Deploy and configure as a Network Intrusion Detection System (NIDS).

---

## 🔥 Attack Demonstrations

### 1. **NMAP Service Scan**

- **Objective:** Reconnaissance to identify open ports.
- **Result:** Ports 21 (FTP), 22 (SSH), 80 (HTTP) found open.


### 2. **ProFTPD Exploit (Metasploit)**

- **Objective:** Exploit ProFTPD 1.3.3c vulnerability for remote root shell.
- **Steps:**
    - Launch Metasploit on Kali.
    - Use `exploit/unix/ftp/proftpd_133c_backdoor`.
    - Set RHOST (victim), RPORT (21), LHOST (attacker), LPORT.
    - Run exploit and gain root shell.


### 3. **DoS Attack (SlowLoris)**

- **Objective:** Deny service on HTTP port using SlowLoris.
- **Steps:**
    - Use Metasploit auxiliary module `dos/http/slowloris`.
    - Configure target IP and port.
    - Launch attack; HTTP service becomes unresponsive.

---

## 🛡️ Defensive Measures

### 1. **Firewall Rules (pfSense)**

#### **Rule 1: Block Social Media**

- Block access to Facebook, Instagram, Twitter for internal users.
- Use aliases and block rules.


#### **Rule 2: Block HTTP (Port 80)**

- Prevent internal users from accessing any HTTP (non-HTTPS) sites.


#### **Rule 3: Block Incoming FTP**

- Block FTP connections on both WAN and LAN interfaces.


#### **Rule 4: Mitigate DoS Attacks**

- Limit HTTP connections per host (max 50), per second (max 20), and set state timeout (10s).
- Block excessive connections to prevent SlowLoris-style attacks.


### 2. **IDS/IPS Alerts (Security Onion)**

- **SGUIL \& Kibana Dashboards:** Monitor and visualize alerts for:
    - NMAP scans
    - ProFTPD exploitation
    - DoS attempts

---

*(Refer to the project PDF for detailed visual guidance.)*

---

## 📚 References

- [Project PDF (Full Documentation)](https://github.com/KDShetty11/Network-defense-simulation/blob/main/Network%20Defence%20project.pdf)
- [pfSense Documentation](https://docs.netgate.com/pfsense/en/latest/)
- [Security Onion Documentation](https://docs.securityonion.net/)
- [Metasploit Unleashed](https://www.offensive-security.com/metasploit-unleashed/)

---

## 📝 Conclusion

This simulation demonstrates a layered defense approach: **firewall filtering, intrusion detection, and strict network segmentation**, effectively mitigating common attacks and providing robust security visibility.

---

## 💡 Tips

- Always test firewall rules in a controlled environment before deploying to production.
- Regularly update IDS signatures and firewall rules.
- Monitor logs and alerts for unusual activity.

---

**Happy Defending! 🛡️**

---

<sup>For any queries or contributions, please open an issue or pull request on this repository.</sup>

<div style="text-align: center">⁂</div>

[^1]: CS-646-Project-2_ks2378_cmj26.pdf

[^2]: Network%20Defence%20project.pdf

