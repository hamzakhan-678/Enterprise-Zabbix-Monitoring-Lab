# 📊 Enterprise Infrastructure & NOC Monitoring Lab (Zabbix)

## 📌 Project Overview
This project demonstrates the deployment and configuration of a centralized **Enterprise Infrastructure Monitoring Server (Zabbix)** on **Ubuntu Linux Server**. The lab monitors a multi-platform corporate network over **OpenVPN**, tracking system health, critical Windows Server roles, firewall bandwidth via **SNMP**, web application availability, and real-time incident recovery.

---

## 🖧 Monitored Infrastructure Inventory

| Hostname | IP & Port | Monitoring Protocol | Monitored Metrics & Services |
| :--- | :--- | :--- | :--- |
| **Zabbix server** | `127.0.0.1:10050` | Zabbix Agent (`ZBX`) | Ubuntu Server LTS, MySQL DB, Apache2/PHP, CPU, RAM (153 Items, 16 Graphs) |
| **Windows-Server-01** | `10.0.0.1:10050` | Zabbix Agent (`ZBX`) | AD DS, DNS, DHCP, IIS (`W3SVC`), MS SQL Server (`MSSQLSERVER`), NTFS `C:` Drive (131 Items, 12 Graphs) |
| **pfSense-Firewall** | `10.0.0.254:161` | Agentless (`SNMPv2`) | WAN/LAN Bandwidth (`em1`), Packet Counters, Firewall States (178 Items, 19 Graphs) |

---

## 🛠️ Key Configurations & Implementations

* **Linux Monitoring Server Deployment:** Installed Ubuntu Server LTS (`10.0.0.200`) with static IP routing via Netplan, remote SSH management, MySQL database schema integration, and Apache2/PHP web frontend.
* **Windows Server Agent Integration (`ZBX`):** Deployed the Zabbix Agent on `Windows-Server-01` (`10.0.0.1`) to automatically discover and monitor 131 system metrics, including Active Directory Domain Services, DNS, DHCP, IIS Web Server, and Microsoft SQL Server (`MSSQLSERVER`).
* **Firewall Telemetry via SNMP (`SNMPv2`):** Configured the SNMP daemon on `pfSense-Firewall` (`10.0.0.254`) to monitor network interface throughput (`em1` LAN traffic), packet errors, and firewall state tables without installing an agent.
* **Multi-Website HTTP Host-Header Monitoring:** Created custom Zabbix Web Scenarios and high-severity triggers to monitor two internal IIS web portals (`http://hr.myhome.local` and `http://portal.myhome.local`) hosted on a single IP, verifying `HTTP 200 OK` status codes, download speeds, and millisecond response times.
* **Live Incident Simulation & Alert Tuning:** Simulated a production outage by stopping the Windows IIS service (`W3SVC`) to validate real-time alert generation, downtime duration tracking (`3m`), and automated recovery (`RESOLVED`), while tuning false-positive SNMP triggers.

---

## 📸 Lab Visual Documentation

### 1. Global NOC Dashboard, LAN Bandwidth (`em1`) & OpenVPN Access
Real-time NOC dashboard displaying host availability, server resource utilization, live pfSense LAN traffic graphs, and active remote administration via OpenVPN (`10.8.0.2`).
![Zabbix Global Dashboard](images/zabbix-dashboard.png)

---

### 2. Multi-Protocol Host Integration (`ZBX` Agent & `SNMPv2`)
Centralized host management verifying active green connectivity across Linux (`ZBX`), Windows Server (`ZBX`), and pfSense Firewall (`SNMP`).
![Zabbix Monitored Hosts](images/zabbix-hosts.png)

---

### 3. Windows Server Low-Level Discovery (AD DS, DNS, DHCP & SQL Server)
Automated discovery of 131 items on `Windows-Server-01`, actively tracking `Active Directory Domain Services`, `DNS Server`, `DHCP Server`, `SQL Server (MSSQLSERVER)`, `W3SVC`, and `NTFS` storage.
![Windows Server Latest Data](images/windows-latest-data.png)

---

### 4. IIS Multi-Site Web Availability & Response Time Monitoring
Active HTTP web scenario monitoring both host-header bound portals (`hr.myhome.local` and `portal.myhome.local`), confirming `200 OK` status codes and fast response latency (`8.06ms` and `11.25ms`).
![IIS Web Monitoring](images/IIS-web-monitoring.png)

---

### 5. Real-Time Incident Detection & Automated Recovery (`RESOLVED`)
Fault-injection test demonstrating immediate detection when `W3SVC` (World Wide Web Publishing Service) stopped, accurate downtime measurement (`3m`), and automatic resolution upon service restart.
![IIS Incident Auto Recovery](images/iis-incident-resolved.png)

---

## 👨‍💻 Author
**Mohammad Hamza Bashir**  
*IT Support & System Administration Engineer*  
📍 Karachi, Pakistan  
📧 hamzabashirkhan678@gmail.com
