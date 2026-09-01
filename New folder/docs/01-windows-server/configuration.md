# Windows Server Configuration

## Goal

Perform the initial configuration before installing server roles.

## Step 1: Rename the server

Open **Server Manager → Local Server** and change the computer name.

Example:

`WIN-SERVER01`

**Screenshot:**  
`![Server name](../screenshots/06-server-name.png)`

## Step 2: Configure a static IP

Open the network adapter settings and configure the lab IP address.

Example:

- IP: `192.168.10.10`
- Subnet: `255.255.255.0`
- Gateway: `192.168.10.1`
- Preferred DNS: `192.168.10.10`

Use addresses appropriate for your own lab.

**Screenshot:**  
`![Static IP](../screenshots/07-static-ip.png)`

## Step 3: Update Windows

Run Windows Update and install available updates.

**Screenshot:**  
`![Windows Update](../screenshots/08-windows-update.png)`

## Step 4: Enable remote administration

Configure only the remote-management features required by the lab.

**Screenshot:**  
`![Remote administration](../screenshots/09-remote-administration.png)`

## Result

The server has a hostname, network configuration and current updates.
