# Network Topology

## Lab topology

```text
                 Internet
                     |
              [Home Router]
                     |
              [Virtual Network]
                     |
          +----------+----------+
          |                     |
 [Windows Server 2022]     [Windows Client]
          |
   +------+------+ 
   |             |
 [AD DS]        [DNS/DHCP]
```

## Suggested lab network

| Device | Example address |
|---|---|
| Router | 192.168.10.1 |
| Windows Server | 192.168.10.10 |
| Client | DHCP |

Use addresses that match your own virtualization and home network.

## Screenshot

Add a screenshot or diagram of your actual virtualization network:

`![Network topology](../screenshots/30-network-topology.png)`

## Connectivity test

From the client:

```powershell
ping 192.168.10.10
nslookup corp.example.test
```

**Screenshot:**  
`![Connectivity test](../screenshots/31-connectivity-test.png)`
