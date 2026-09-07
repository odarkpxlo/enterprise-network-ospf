# Enterprise Network Routing with OSPF

## Project Overview

This project demonstrates the design and implementation of a routed enterprise network using Cisco Packet Tracer.

The main objective was to build a multi-router network, configure IP addressing and routing, implement OSPF as a dynamic routing protocol, and verify end-to-end connectivity.

## Network Topology

```text
PC1 ── SW1 ── R1 ── R2 ── SW2 ── PC2
               │
               R3 ── SW3 ── PC3
```

## IP Addressing

| Device | Interface | IP Address      | Network         |
| ------ | --------- | --------------- | --------------- |
| R1     | G0/0      | 192.168.10.1/24 | 192.168.10.0/24 |
| R1     | G0/1      | 192.168.1.1/30  | 192.168.1.0/30  |
| R2     | G0/0      | 192.168.1.2/30  | 192.168.1.0/30  |
| R2     | G0/1      | 192.168.20.1/24 | 192.168.20.0/24 |
| R2     | G0/2      | 192.168.2.1/30  | 192.168.2.0/30  |
| R3     | G0/0      | 192.168.2.2/30  | 192.168.2.0/30  |
| R3     | G0/1      | 192.168.30.1/24 | 192.168.30.0/24 |

### End Devices

| Device | IP Address       | Default Gateway |
| ------ | ---------------- | --------------- |
| PC1    | 192.168.10.10/24 | 192.168.10.1    |
| PC2    | 192.168.20.10/24 | 192.168.20.1    |
| PC3    | 192.168.30.10/24 | 192.168.30.1    |

## Routing Implementation

The project was first configured using static routes to verify basic Layer 3 connectivity.

After confirming connectivity, the static routes were removed and OSPF was implemented using:

* OSPF Process ID: `1`
* Area: `0`
* Manual Router IDs:

  * R1: `1.1.1.1`
  * R2: `2.2.2.2`
  * R3: `3.3.3.3`

OSPF was configured on all router-to-router links and LAN networks.

LAN-facing interfaces were configured as passive interfaces to prevent unnecessary OSPF neighbor formation toward end devices.

## OSPF Cost

OSPF interface cost was also tested to understand how path selection is affected by cost.

The default path costs were restored after testing.

This demonstrated how OSPF calculates the total path cost and selects the lowest-cost route.

## Verification and Troubleshooting

The following commands were used to verify the configuration and troubleshoot the network:

```text
show ip ospf neighbor
show ip ospf interface
show ip route ospf
show ip route
```

Connectivity was verified using end-to-end ICMP tests between all three LANs.

OSPF neighbor relationships were verified as `FULL`, and the expected OSPF routes were present in the routing tables.

## Failure Detection and Reconvergence

An OSPF link failure was simulated by shutting down the R1-R2 interface.

The OSPF neighbor relationship was removed and the affected routes were withdrawn from the routing table.

After restoring the interface, OSPF re-established the neighbor relationship and learned the routes again.

> Note: This topology contains a single path between R1 and R3, so the failure test demonstrates OSPF failure detection and route reconvergence rather than true redundant-path failover.

## Technologies Used

* Cisco Packet Tracer
* Cisco IOS
* OSPF
* IPv4
* Static Routing
* Dynamic Routing
* ICMP
* Layer 3 Troubleshooting

## Project Files

* `enterprise-network-ospf.pkt` — Cisco Packet Tracer project
* `topology` — Network topology
* `OSPF-nghb` — OSPF neighbor verification
* `OSPF-routing` — OSPF interface and routing verification
* `end-to-end` — End-to-end connectivity tests

## Key Learning Outcomes

This project strengthened practical understanding of:

* Static vs. dynamic routing
* OSPF neighbor relationships
* OSPF Router ID
* OSPF Area 0
* Passive interfaces
* OSPF cost and path selection
* Routing table verification
* OSPF failure detection and reconvergence
* Layer 3 troubleshooting
