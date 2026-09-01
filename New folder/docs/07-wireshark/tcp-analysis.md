# TCP Analysis with Wireshark

## Goal

Understand a basic TCP connection in the lab.

## Capture

Generate traffic between two lab systems and use:

```text
tcp
```

**Screenshot:**  
`![TCP filter](../screenshots/42-tcp-filter.png)`

## Three-way handshake

Inspect:

1. SYN
2. SYN-ACK
3. ACK

**Screenshot:**  
`![TCP handshake](../screenshots/43-tcp-handshake.png)`

## Things to observe

- Source and destination ports
- Sequence numbers
- Acknowledgement numbers
- TCP flags
- Retransmissions
