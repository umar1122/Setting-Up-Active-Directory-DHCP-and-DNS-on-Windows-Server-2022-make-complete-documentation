# DNS Analysis with Wireshark

## Capture

Generate a DNS query from a lab client and capture the traffic.

Example filter:

```text
dns
```

**Screenshot:**  
`![DNS filter](../screenshots/38-dns-filter.png)`

## What to inspect

Look at:

- Source and destination IP
- DNS query name
- Query type
- Response code
- Answer records

**Screenshot:**  
`![DNS packet](../screenshots/39-dns-packet.png)`
