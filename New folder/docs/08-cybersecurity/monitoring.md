# Monitoring

## Goal

Monitor the Windows Server environment and identify unusual activity.

## Event Viewer

Review:

- Security logs
- System logs
- Application logs

**Screenshot:**  
`![Security logs](../screenshots/47-security-logs.png)`

## Useful PowerShell commands

```powershell
Get-WinEvent -LogName System -MaxEvents 20
Get-WinEvent -LogName Security -MaxEvents 20
```

Use appropriate permissions when accessing security logs.

## What to monitor

- Failed logins
- Account changes
- Service changes
- Firewall events
- Unexpected system errors
