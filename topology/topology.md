# Topology and interface map

## WAN / routing chain

```text
DSW1 Gi0/1 10.0.0.2/30
    |
    | 10.0.0.0/30 — OSPF area 0
    |
R4 Gi0/0 10.0.0.1/30
R4 Gi0/1 10.0.0.5/30
    |
    | 10.0.0.4/30 — EIGRP AS 100
    |
R2 Gi0/0 10.0.0.6/30
R2 Gi0/1 10.0.0.9/30
    |
    | 10.0.0.8/30 — RIP v2
    |
R3 Gi0/0 10.0.0.10/30
R3 Gi0/1 10.0.0.13/30
    |
    | 10.0.0.12/30 — eBGP AS 65003 ↔ 65005
    |
R5/ISP Gi0/0 10.0.0.14/30
```

## Campus switching

- SW2 Fa0/1: PC1 access port, VLAN 10.
- SW2 Fa0/2: PC2 access port, VLAN 20.
- SW2 Fa0/24 ↔ DSW1 Fa0/1: trunk; observed as primary/root path for the affected VLANs.
- SW2 Fa0/23 ↔ DSW2 Fa0/1: redundant trunk; STP blocked it where needed to prevent a loop.
- DSW1 Fa0/2 ↔ DSW2 Fa0/2: trunk.
- DSW1 Fa0/3-4 ↔ DSW2 Fa0/3-4: LACP EtherChannel, Port-channel1.
- Server: connected to DSW2 Fa0/10 in VLAN 30.

## Notes

- DSW1 and DSW2 are Catalyst 3560-24TS Layer 3 switches.
- SW2 is a Catalyst 2960-24TT-L access switch.
- R4 is an ISR4331.
- The lab includes redundant campus Layer 2 links. Keep STP enabled and verify the active/blocked ports after any topology changes.
- Interface numbering and endpoint attachment should be checked against the saved PMN-OS project before using this document as an exact physical wiring guide.
