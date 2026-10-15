# Verification results

These are results reported during the interactive PMN-OS lab session. Retest them after importing or rebuilding the topology.

| Source | Destination | Result recorded |
|---|---|---|
| Server `192.168.30.10` | `192.168.30.1` | Successful |
| Server `192.168.30.10` | `192.168.30.2`, `.3` | Successful |
| Server `192.168.30.10` | `192.168.99.1`, `.2`, `.3`, `.10` | Successful |
| Server `192.168.30.10` | R2 Lo0 `172.16.2.2` | Successful |
| R4 | R3 Lo0 `172.16.3.3` | 5/5 replies |
| Server `192.168.30.10` | R3 Lo0 `172.16.3.3` | 4/4 replies, 0% loss |
| Server `192.168.30.10` | R5 Lo0 `203.0.113.1` | Initially failed; later 4/4 replies, 0% loss after return route was advertised |

## Routing evidence observed

- R2 route to `172.16.3.3/32`: RIP via `10.0.0.10`; advertised by EIGRP AS 100.
- R2 route to `203.0.113.1/32`: RIP via `10.0.0.10`; advertised by EIGRP AS 100.
- R4 route to `203.0.113.1/32`: EIGRP external via `10.0.0.6`.
- R3 route to `203.0.113.1/32`: BGP AS 65003, next hop `10.0.0.14`.
- R3 route to `192.168.30.0/24`: RIP via `10.0.0.9`.
- R5 BGP table included `192.168.30.0/24` via `10.0.0.13`.

## Suggested retest commands

```text
show ip route
show ip protocols
show ip ospf neighbor
show ip eigrp neighbors
show ip rip database
show ip bgp summary
show ip bgp
show etherchannel summary
show interfaces trunk
show spanning-tree
show standby brief
```

Run only commands supported by the particular PMN-OS device model. Save clean CLI screenshots to this folder if desired; remove any sensitive values before publishing.
