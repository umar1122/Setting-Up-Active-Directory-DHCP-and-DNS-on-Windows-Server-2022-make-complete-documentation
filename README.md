# Active Directory Home Lab

A home lab built in Hyper-V where I set up a working Active Directory environment from the ground up domain controller, DNS, DHCP, organizational units, and a domain-joined client.

## Overview

This was my first full AD build. The goal was to get a proper domain running that I can keep expanding later (more domain controllers, group policy, more OUs, etc). I kept the first version simple: one domain controller, one client PC, and just enough structure to organize users.

## Lab Topology

| Machine | Role | OS | IP |
|---|---|---|---|
| DC01 | Domain Controller, DNS, DHCP | Windows Server 2022 | `192.168.0.1` (static) |
| PC01 | Domain-joined client | Windows 10 | DHCP (`192.168.0.50`–`200` range) |

- Domain name: `int.acme.com`
- NetBIOS name: `ACME`
- Both VMs run on Hyper-V, connected through a private virtual switch

## What's Included

- Active Directory Domain Services (new forest, new domain)
- DNS with forward and reverse lookup zones
- DHCP scope with gateway/DNS options handed out to clients
- Organizational Unit structure: `ACME > IT` and `ACME > Staff`
- Two test user accounts (one IT admin, one regular staff)
- A domain-joined client PC verified with real logins

## Tools Used

- Microsoft Hyper-V
- Windows Server 2022
- Windows 10

## Setup Summary

1. Deployed Windows Server 2022, renamed to `DC01`, set static IP
2. Installed the AD DS role (DNS installed alongside it)
3. Promoted the server to a domain controller and created the `int.acme.com` forest
4. Verified DNS and manually added the missing reverse lookup zone
5. Installed and configured DHCP, authorized it against AD
6. Built an OU structure for IT and Staff
7. Created two users and assigned one to Domain Admins
8. Joined PC01 to the domain and got an IP from DHCP
9. Logged in with both domain accounts to confirm everything worked end to end

Full step-by-step writeup with details and reasoning: [active-directory-homelab.md](./active-directory-homelab.md)

## What I Learned

- Why internal AD domain names should be separate from your public domain (avoiding split-brain DNS)
- AD DS creates a forward DNS zone automatically but not a reverse zone — that has to be added manually
- DHCP needs to be authorized against AD before it can hand out leases in a domain environment
- The difference between logging into a machine locally vs authenticating against a domain controller
- Why you keep the built-in `administrator` account out of daily use and instead promote a named account to Domain Admins

## Next Steps

- [1] Add a second domain controller for redundancy
- [2] Configure Group Policy Objects
- [3] Expand OU structure and add more security groups
- [4] Set up DHCP failover

---
*Home lab project :- built for learning, not production use.*
