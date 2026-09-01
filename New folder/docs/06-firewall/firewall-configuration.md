# Windows Firewall Configuration

## Goal

Understand and verify Windows Defender Firewall rules in the lab.

## Step 1: Open Windows Defender Firewall

Open:

**Windows Defender Firewall with Advanced Security**

**Screenshot:**  
`![Windows Firewall](../screenshots/32-windows-firewall.png)`

## Step 2: Review inbound rules

Review enabled inbound rules and understand which services they allow.

**Screenshot:**  
`![Inbound rules](../screenshots/33-inbound-rules.png)`

## Step 3: Review outbound rules

Check the outbound rule configuration.

**Screenshot:**  
`![Outbound rules](../screenshots/34-outbound-rules.png)`

## Step 4: Test connectivity

Test only the services required by the lab.

Example:

```powershell
Test-NetConnection 192.168.10.10 -Port 53
```

**Screenshot:**  
`![Firewall test](../screenshots/35-firewall-test.png)`

## Security notes

- Keep unnecessary ports closed.
- Use the Windows Firewall profiles appropriate to the environment.
- Avoid disabling the firewall as a troubleshooting shortcut.
- Document any custom rules.
