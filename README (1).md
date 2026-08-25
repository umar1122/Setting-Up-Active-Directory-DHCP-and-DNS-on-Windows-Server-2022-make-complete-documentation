# Setting Up Active Directory, DHCP, and DNS on Windows Server 2022

A complete, beginner-friendly walkthrough for building a working Windows Server 2022 lab with Active Directory Domain Services,  DNS, and DHCP from a blank server to a client machine successfully joining the domain.

This is written the way I'd explain it to a friend, not copied from a manual. If you're studying for a certification, building a home lab, or just trying to understand how a real Windows domain environment works, this should get you there.




## Table of Contents

- [What You'll Need](#what-youll-need-before-starting)
- [Understanding the Three Pieces](#understanding-the-three-pieces-in-plain-english)
- [Part 1: Static IP Setup](#part-1-setting-a-static-ip-address)
- [Part 2: Installing Active Directory](#part-2-installing-active-directory-domain-services-ad-ds)
- [Part 3: Verifying AD and DNS](#part-3-verifying-active-directory-and-dns)
- [Part 4: Installing and Configuring DHCP](#part-4-installing-and-configuring-dhcp)
- [Part 5: Testing Everything Together](#part-5-testing-everything-together)
- [Common Issues and Fixes](#common-issues-and-fixes)
- [Next Steps](#next-steps)



## What You'll Need Before Starting

- A machine (physical or virtual) running **Windows Server 2022**
- At least 2 GB RAM and 40 GB disk space (a VM in VirtualBox, VMware, or Hyper-V works fine)
- A static IP address already set on the server (don't skip this — DHCP and DNS servers need a fixed address, not a dynamic one)
- Administrator access on the server
- A second machine (Windows 10/11) to test joining the domain later — optional but recommended


## Understanding the Three Pieces (In Plain English)

Before touching the server, here's what each service actually does:

**Active Directory (AD DS)** — Think of it as a big phonebook and rulebook for your network. It keeps track of every user, computer, and group, and controls who can log into what.

**DNS (Domain Name System)** — Translates names into IP addresses. When a computer looks for `server1.mycompany.local`, DNS tells it the actual IP address to connect to. Active Directory depends on DNS to work at all.

**DHCP (Dynamic Host Configuration Protocol)** — Automatically hands out IP addresses to devices on the network, so you don't have to manually configure every machine by hand.



## Part 1: Setting a Static IP Address

Before installing anything, your server needs a fixed IP address.

1. Open **Control Panel > Network and Sharing Center > Change adapter settings**
2. Right-click your network adapter and choose **Properties**
3. Select **Internet Protocol Version 4 (TCP/IPv4)** and click **Properties**
4. Set the following (example values, adjust to your own network):
   - IP address: `192.168.1.10`
   - Subnet mask: `255.255.255.0`
   - Default gateway: `192.168.1.1`
   - Preferred DNS server: `127.0.0.1` (the server will point to itself once DNS is installed)

Click **OK** and close out.



## Part 2: Installing Active Directory Domain Services (AD DS)

### Step 1: Open Server Manager

Server Manager should open automatically when you log in. If not, click the icon in the taskbar.

### Step 2: Add the AD DS Role

1. Click **Manage > Add Roles and Features**
2. Click **Next** through the initial screens (Installation Type: Role-based, Server Selection: choose your local server)
3. On the **Server Roles** screen, check the box for **Active Directory Domain Services**
4. A popup will ask to add required features — click **Add Features**
5. Click **Next** through the remaining screens, then click **Install**
6. Wait for the installation to finish (usually a few minutes), then click **Close**

### Step 3: Promote the Server to a Domain Controller

Installing the role isn't enough — you now need to actually promote the server.

1. In Server Manager, click the **notification flag** icon at the top
2. Click **Promote this server to a domain controller**
3. Select **Add a new forest**
4. Enter a root domain name, for example: `mycompany.local`
5. Click **Next**
6. Set a **Directory Services Restore Mode (DSRM) password** — write this down somewhere safe, you'll rarely need it but it's important
7. Click **Next** through the DNS warning (this is normal on a new forest)
8. Confirm the **NetBIOS name** (auto-filled, usually fine)
9. Keep the default paths for the database, log files, and SYSVOL unless you have a specific reason to change them
10. Review the summary, then click **Next**
11. Wait for the prerequisite check to pass, then click **Install**

The server will automatically restart once this is complete. When it comes back up, you'll now be logging in as a **domain administrator** instead of just a local admin.


## Part 3: Verifying Active Directory and DNS

Since DNS installs automatically alongside AD DS, let's confirm everything is working.

1. Open **Server Manager > Tools > DNS**
2. Expand your server name, then expand **Forward Lookup Zones**
3. You should see a zone matching your domain name (e.g., `mycompany.local`) with some auto-created records inside it

If you see that zone with records, DNS is working correctly.

You can also open **Tools > Active Directory Users and Computers** to confirm your domain structure is visible, with folders like Users, Computers, and Domain Controllers.

## Part 4: Installing and Configuring DHCP

### Step 1: Add the DHCP Role

1. In Server Manager, click **Manage > Add Roles and Features**
2. Click **Next** through to **Server Roles**
3. Check **DHCP Server**
4. Click **Add Features** when prompted, then **Next** through the rest
5. Click **Install**, then **Close** once finished

### Step 2: Complete DHCP Post-Deployment Configuration

1. Click the notification flag in Server Manager
2. Click **Complete DHCP configuration**
3. Click **Next**, then **Commit**
4. Click **Close**

This step authorizes the DHCP server in Active Directory, which is required before it can start handing out addresses.

### Step 3: Create a DHCP Scope

A "scope" is just the range of IP addresses DHCP is allowed to give out.

1. Open **Server Manager > Tools > DHCP**
2. Expand your server, right-click **IPv4**, and choose **New Scope**
3. Click **Next** on the wizard welcome screen
4. Give the scope a name, like `Office-LAN`
5. Set the IP address range, for example:
   - Start IP: `192.168.1.100`
   - End IP: `192.168.1.200`
   - Subnet mask: `255.255.255.0`
6. Add any exclusions if needed (IPs you don't want handed out, like ones used by servers or printers)
7. Set a lease duration (default of 8 days is fine for most setups)
8. When asked to configure DHCP options now, choose **Yes**
9. Enter your default gateway (router IP), for example `192.168.1.1`
10. Under DNS settings, your domain name and DNS server IP should already be filled in correctly (pointing to your server) — confirm and click **Next**
11. Skip WINS server settings unless you specifically need it
12. Choose **Yes, I want to activate this scope now**
13. Click **Finish**

Your DHCP server is now live and ready to assign IP addresses.



## Part 5: Testing Everything Together

1. On a second machine (physical or virtual), set its network adapter back to **Obtain an IP address automatically**
2. Restart the network adapter or reboot the machine
3. Open Command Prompt and run:
   ```
   ipconfig /all
   ```
4. You should see an IP address from the range you configured (e.g., `192.168.1.101`), along with the correct DNS server and gateway



To test the domain join:

1. On that second machine, go to **Settings > System > About > Rename this PC (Advanced)**
2. Click **Change**, select **Domain**, and enter your domain name (e.g., `mycompany.local`)
3. Enter domain administrator credentials when prompted
4. Restart when asked

If the machine successfully joins and shows up under **Computers** in Active Directory Users and Computers, everything is working as it should.



## Common Issues and Fixes

**DNS isn't resolving the domain name**
Double-check that the server's own network adapter is pointing to itself (`127.0.0.1` or its own static IP) as the preferred DNS server.

**DHCP isn't handing out addresses**
Make sure the scope is activated and that the DHCP server is authorized in Active Directory. An unauthorized DHCP server will silently refuse to lease addresses.

**Client can't join the domain**
Confirm the client machine's DNS setting points to your AD server's IP, not your router or a public DNS like 8.8.8.8. Domain join relies entirely on DNS working correctly first.

**"The following error occurred attempting to join the domain" errors**
This is almost always a DNS or connectivity issue. Ping the domain controller by name and by IP from the client to narrow down where the problem is.



## Next Steps

At this point, you've built a small but complete Windows network from scratch — a Domain Controller managing identities, DNS handling name resolution, and DHCP automatically configuring client machines. This is the same foundational setup used in real-world business networks, just on a smaller scale.

Good next steps to explore:

- Creating Organizational Units (OUs) and Group Policy Objects (GPOs)
- Setting up a secondary domain controller for redundancy
- Configuring DNS forwarders for internet name resolution
- Hardening security with fine-grained password policies



## Contributing

Found an error or want to add screenshots from your own setup? Pull requests are welcome.

