# DHCP Analysis with Wireshark

## Capture

Renew the client DHCP lease while capturing traffic.

Useful display filter:

```text
dhcp
```

or:

```text
bootp
```

**Screenshot:**  
`![DHCP filter](../screenshots/40-dhcp-filter.png)`

## DHCP process

Look for the normal DHCP exchange:

1. Discover
2. Offer
3. Request
4. Acknowledgement

**Screenshot:**  
`![DHCP exchange](../screenshots/41-dhcp-exchange.png)`
