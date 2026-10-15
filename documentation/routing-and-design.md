# Routing and design notes

## Routing domains

1. **OSPF process 1, area 0:** DSW1 and R4 exchange campus and WAN-edge routes. Router IDs recorded: DSW1 `1.1.1.1`, R4 `4.4.4.4`.
2. **EIGRP AS 100:** R4 and R2 exchange routes over `10.0.0.4/30`.
3. **RIP v2:** R2 and R3 exchange routes over `10.0.0.8/30`; loopbacks are also included in the lab's RIP routing.
4. **eBGP:** R3 (`AS 65003`) peers with R5 (`AS 65005`) across `10.0.0.12/30`.

## Redistribution learned during the lab

- R4 redistributed OSPF into EIGRP and EIGRP into OSPF.
- R2 redistributed RIP into EIGRP so routes learned from R3 could propagate toward R4.
- R3 redistributed BGP into RIP, allowing the ISP loopback route to propagate into the internal routing chain.
- R3 originated `192.168.30.0/24` into BGP so R5 had a return route to the server subnet.

Redistribution between multiple protocols can create feedback loops or suboptimal paths if used without route tagging, filtering, or carefully designed policies. This topology is for learning. For production networks, define explicit route maps/policies, tags, prefix filters, and a documented routing policy.

## HSRP and VLANs

The HSRP virtual gateway is `.1` in each VLAN subnet. DSW1 was configured with priority 110 and preemption; DSW2 with priority 100 and preemption. DSW1 was observed active for the four groups when the SVIs were up.

## Layer 2 redundancy

- LACP EtherChannel uses Fa0/3-4 on each distribution switch, as Port-channel1.
- The distribution/access uplinks use 802.1Q trunks with VLANs 10, 20, 30, and 99 allowed.
- Spanning Tree blocks a redundant trunk where needed. Do not force a blocked port into forwarding without checking for a Layer 2 loop.

## Addressing

See the address tables in the root README and `../topology/topology.md`.
