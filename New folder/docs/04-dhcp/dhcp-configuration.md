# DHCP Configuration

## Goal

Configure DHCP for automatic IP address assignment in the lab.

## Step 1: Install DHCP Server

Use **Server Manager → Add Roles and Features** and select **DHCP Server**.

**Screenshot:**  
`![DHCP role](../screenshots/25-dhcp-role.png)`

## Step 2: Complete DHCP configuration

Complete the DHCP post-installation configuration.

**Screenshot:**  
`![DHCP configuration](../screenshots/26-dhcp-configuration.png)`

## Step 3: Create a scope

Create a scope matching the lab network.

Example:

- Network: `192.168.10.0/24`
- Start: `192.168.10.100`
- End: `192.168.10.200`

Use a range appropriate for your network.

**Screenshot:**  
`![DHCP scope](../screenshots/27-dhcp-scope.png)`

## Step 4: Configure options

Configure the required gateway and DNS server options.

**Screenshot:**  
`![DHCP options](../screenshots/28-dhcp-options.png)`

## Step 5: Test from a client

On a Windows client:

```powershell
ipconfig /release
ipconfig /renew
ipconfig /all
```

**Screenshot:**  
`![DHCP lease](../screenshots/29-dhcp-lease.png)`

## Result

The client receives an IP configuration from the lab DHCP server.
