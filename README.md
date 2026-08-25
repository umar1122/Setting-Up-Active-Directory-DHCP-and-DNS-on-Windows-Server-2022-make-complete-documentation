# 🖥️ Windows Server & Cybersecurity Home Lab

> **Status: 🚧 Ongoing Project**

This is my personal **hands-on IT infrastructure and cybersecurity home lab**. The goal of this project is to build a small physical network and gradually expand it with Windows Server administration, networking, security, monitoring, and troubleshooting.

I am documenting the configuration, experiments, problems, solutions, and lessons learned throughout the project.

---

## 📌 Project Overview

The current lab consists of:

* One physical Ethernet switch
* One physical laptop acting as the virtualization host
* VirtualBox running on the laptop
* Windows Server 2022 running as a virtual machine
* Active Directory Domain Services (AD DS)
* DNS Server
* DHCP Server
* Two physical Windows client machines connected directly to the switch

The physical clients communicate through the switch with the Windows Server virtual machine hosted on the laptop.

The lab is being expanded gradually to include **network monitoring, firewall configuration, security testing, logging, and cybersecurity concepts**.

---

## 🏗️ Current Network Architecture

```text
                         Physical Network
                              │
                              │
                    ┌─────────▼─────────┐
                    │   Physical Switch │
                    └───────┬─────┬─────┘
                            │     │
                 Ethernet   │     │   Ethernet
                            │     │
                  ┌─────────▼─┐ ┌─▼──────────┐
                  │ Windows   │ │ Windows    │
                  │ Laptop    │ │ Client 1   │
                  └───────────┘ └────────────┘
                            │
                            │
                            │
                    ┌───────▼─────────┐
                    │     Laptop      │
                    │ VirtualBox Host │
                    └───────┬─────────┘
                            │
                     Virtual Network
                            │
                    ┌───────▼─────────┐
                    │ Windows Server  │
                    │      2022       │
                    │                 │
                    │ Active Directory│
                    │ DNS             │
                    │ DHCP            │
                    └─────────────────┘
```

---

## 🖥️ Current Lab Components

| Component                | Role                                    |
| ------------------------ | --------------------------------------- |
| Physical Ethernet Switch | Connects the lab devices                |
| Laptop                   | Physical virtualization host            |
| VirtualBox               | Virtualization platform                 |
| Windows Server 2022      | Server infrastructure                   |
| Active Directory         | Centralized identity and authentication |
| DNS                      | Name resolution and AD support          |
| DHCP                     | Automatic IP address configuration      |
| Windows Client 1         | Domain/network client                   |
| Windows Client 2         | Domain/network client                   |

---

# 🔧 Current Configuration

## 1. Physical Network

I started the lab by using a **physical Ethernet switch** as the central connection point.

The switch provides physical connectivity between:

* The laptop hosting the virtual server
* Windows Client 1
* Windows Client 2

This allows me to work with a physical network rather than using only an isolated virtual network.

---

## 2. Virtualization

I installed **VirtualBox** on the physical laptop.

Inside VirtualBox, I created a virtual machine running:

**Windows Server 2022**

The Windows Server VM provides the main infrastructure services for the lab.

---

## 3. Windows Server 2022

The Windows Server 2022 VM is configured to provide several core network services.

### Active Directory Domain Services

I installed and configured:

* Active Directory Domain Services (AD DS)
* Active Directory domain
* Domain users
* Groups
* Organizational Units (OUs)
* Domain authentication

---

## 4. DNS

DNS is configured on the Windows Server.

The lab uses DNS to support:

* Hostname resolution
* Domain communication
* Active Directory functionality
* Client-to-server communication

One of the important things I learned from this lab is how closely **DNS and Active Directory** are connected.

---

## 5. DHCP

I configured the Windows Server as a DHCP server.

The DHCP service provides clients with network configuration such as:

* IP address
* Subnet mask
* Default gateway
* DNS server

I also tested DHCP address assignment from the Windows clients.

---

## 6. Windows Clients

Two Windows client machines are physically connected to the switch using Ethernet cables.

The clients are being used to test:

* DHCP
* DNS
* Network connectivity
* Domain connectivity
* Domain authentication
* Client/server communication

---

# 📚 What I Have Learned

Through this lab I have gained practical experience with:

### Windows Server

* Installing Windows Server 2022
* Configuring server networking
* Installing server roles
* Basic Windows Server administration

### Active Directory

* Installing AD DS
* Creating an Active Directory domain
* Managing users
* Managing groups
* Creating Organizational Units
* Understanding domain authentication

### DNS

* Installing DNS
* Understanding DNS zones and records
* Understanding the relationship between DNS and Active Directory
* Testing name resolution

### DHCP

* Installing DHCP
* Creating DHCP scopes
* Configuring IP address ranges
* Configuring DHCP options
* Testing automatic IP configuration

### Networking

* Working with a physical Ethernet switch
* Connecting physical clients
* Understanding IP addressing
* Understanding client/server communication
* Troubleshooting network connectivity
* Working with physical and virtual network interfaces

### Virtualization

* Creating virtual machines with VirtualBox
* Running Windows Server in a virtual environment
* Connecting virtual machines to a physical network

---

# 🔐 Cybersecurity Roadmap

The project is still ongoing.

My next goal is to extend the lab from basic Windows infrastructure into a **small cybersecurity testing and monitoring environment**.

## Planned Security Components

### 🔥 Firewall

I plan to add firewall configuration and testing to the lab.

Areas I want to explore:

* Windows Defender Firewall
* Inbound rules
* Outbound rules
* Allowing/denying specific ports
* Network segmentation
* Testing firewall rules
* Understanding how firewall rules affect communication

---

### 🦈 Wireshark Network Monitoring

I plan to use **Wireshark** to capture and analyze traffic generated by the lab.

Wireshark is a network protocol analyzer that can capture live traffic and allow individual packets and protocols to be examined.

I want to investigate:

* ARP traffic
* DHCP traffic
* DNS queries
* TCP connections
* UDP traffic
* ICMP/ping traffic
* HTTP/HTTPS traffic
* Client-to-server communication
* Normal network behavior

I will document example packet captures and explain what I observe.

> **Important:** Packet captures will only be performed on my own lab network and systems that I am authorized to monitor.

---

### 🛡️ Windows Security

I plan to investigate:

* Windows Defender
* Windows Firewall
* Windows Event Viewer
* Security logs
* Authentication events
* Failed login attempts
* Account management
* Local security policies
* Password policies
* User privileges

---

### 📊 Monitoring & Logging

I plan to build a basic monitoring and logging workflow.

Possible areas include:

* Windows Event Viewer
* Security logs
* System logs
* Network traffic monitoring
* DNS logs
* DHCP logs
* Authentication events
* Suspicious activity detection

---

### 🔎 Cybersecurity Fundamentals

As the project develops, I will study and document:

* CIA Triad
* Authentication vs authorization
* Least privilege
* Network segmentation
* Attack surface
* Common network protocols
* Common Windows security risks
* Secure configuration
* Logging and monitoring
* Incident detection
* Basic incident response

---

# 🧪 Planned Security Experiments

The following experiments are planned for future stages of the lab:

* [ ] Configure Windows Defender Firewall rules
* [ ] Test blocked and allowed network connections
* [ ] Capture DHCP traffic with Wireshark
* [ ] Capture DNS traffic with Wireshark
* [ ] Analyze ARP traffic
* [ ] Analyze TCP handshakes
* [ ] Analyze ICMP traffic
* [ ] Investigate Windows authentication logs
* [ ] Configure stronger password policies
* [ ] Create different user privilege levels
* [ ] Study Windows security events
* [ ] Implement basic network monitoring
* [ ] Document common Windows security weaknesses
* [ ] Research defensive security techniques
* [ ] Build a small incident-response exercise
* [ ] Document lessons learned from each experiment

---

# 🗂️ Documentation Structure

As the project grows, I plan to organize the documentation into sections:

```text
docs/
│
├── 01-windows-server/
│   ├── installation.md
│   └── configuration.md
│
├── 02-active-directory/
│   ├── domain-setup.md
│   ├── users-and-groups.md
│   └── organizational-units.md
│
├── 03-dns/
│   └── dns-configuration.md
│
├── 04-dhcp/
│   └── dhcp-configuration.md
│
├── 05-networking/
│   └── network-topology.md
│
├── 06-firewall/
│   └── firewall-configuration.md
│
├── 07-wireshark/
│   ├── packet-captures.md
│   ├── dns-analysis.md
│   ├── dhcp-analysis.md
│   └── tcp-analysis.md
│
└── 08-cybersecurity/
    ├── security-basics.md
    ├── windows-security.md
    ├── monitoring.md
    └── incident-response.md
```

---

# 🎯 Project Goals

The long-term goal is to turn this small home lab into a practical environment for learning:

**System Administration → Networking → Security → Monitoring → Incident Response**

I want to use the lab to understand not only how to configure systems, but also how to **secure, monitor, troubleshoot, and investigate them**.

---

# 🚀 Future Plans

The lab will continue to evolve.

Potential future additions include:

* Windows Firewall
* Advanced firewall/router
* Wireshark
* Network monitoring
* Windows Event Logging
* Group Policy
* File servers
* Additional Windows clients
* Additional domain controller
* Linux server
* Security monitoring
* Vulnerability management
* SIEM experimentation
* Backup and recovery
* PowerShell automation
* Security hardening
* Incident-response exercises

---

# 📈 Project Status

| Area                          | Status      |
| ----------------------------- | ----------- |
| Physical switch               | ✅ Completed |
| VirtualBox                    | ✅ Completed |
| Windows Server 2022           | ✅ Completed |
| Active Directory              | ✅ Completed |
| DNS                           | ✅ Completed |
| DHCP                          | ✅ Completed |
| Windows Client 1              | ✅ Completed |
| Windows Client 2              | ✅ Completed |
| Physical network connectivity | ✅ Completed |
| Firewall                      | 🚧 Planned  |
| Wireshark                     | 🚧 Planned  |
| Network monitoring            | 🚧 Planned  |
| Windows security monitoring   | 🚧 Planned  |
| Cybersecurity experiments     | 🚧 Planned  |
| SIEM / advanced monitoring    | 🔮 Future   |

---

# 🧠 Key Learning

This project is helping me move beyond theoretical knowledge and gain practical experience with a real physical network and virtualized server environment.

The most important part of the project is the continuous learning process: **build → configure → test → troubleshoot → secure → monitor → document**.

---

## 👤 Author

**Umar**

GitHub: [umar1122](https://github.com/umar1122)

---

## 📖 References

* [GitHub README Documentation](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-readmes)
* [Wireshark User Guide](https://www.wireshark.org/docs/wsug_html/)
* [Wireshark Capture Setup Guide](https://wiki.wireshark.org/CaptureSetup)

---

⭐ This project is continuously evolving as I add new technologies, security experiments, monitoring tools, and documentation.
