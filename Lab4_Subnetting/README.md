# Lab 4 – Subnetting

## Objective
Subnet a Class C network into two subnets and configure IP addresses, subnet masks, and default gateways on a router and four PCs across two separate network segments.

## Subnetting

Starting network: **192.168.10.0 /24**

To create a maximum of two subnets, borrow 1 bit from the host portion, giving a **/25** prefix. This produces two subnets of 126 usable hosts each.

| Subnet | Network Address | Usable Range | Broadcast | Used On |
|--------|----------------|--------------|-----------|---------|
| Subnet 1 | 192.168.10.0 /25 | 192.168.10.1 – 192.168.10.126 | 192.168.10.127 | R1 g0/0/0 |
| Subnet 2 | 192.168.10.128 /25 | 192.168.10.129 – 192.168.10.254 | 192.168.10.255 | R1 g0/0/1 |

**Subnet mask for both:** 255.255.255.128

---

## Device Configuration

### Subnet 1 – R1 g0/0/0 side

| Device | IP Address | Subnet Mask | Default Gateway |
|--------|------------|-------------|-----------------|
| R1 g0/0/0 | 192.168.10.1 | 255.255.255.128 | — |
| PC-A | 192.168.10.2 | 255.255.255.128 | 192.168.10.1 |
| PC-B | 192.168.10.126 | 255.255.255.128 | 192.168.10.1 |

### Subnet 2 – R1 g0/0/1 side

| Device | IP Address | Subnet Mask | Default Gateway |
|--------|------------|-------------|-----------------|
| R1 g0/0/1 | 192.168.10.129 | 255.255.255.128 | — |
| PC-C | 192.168.10.130 | 255.255.255.128 | 192.168.10.129 |
| PC-D | 192.168.10.254 | 255.255.255.128 | 192.168.10.129 |

---

## Key Concepts

- **Borrowing 1 bit** from a /24 creates 2 subnets (/25), each with 126 usable host addresses
- The **router interface** on each subnet acts as the default gateway for all devices on that segment
- PC-A and PC-B can communicate directly (same subnet); to reach PC-C or PC-D they must go through the router
- PC-B gets the **last usable address** (.126) and PC-D gets the **last usable address** on its subnet (.254) — one below the broadcast address

---

## Project File

[`subnetting_quiz.pka`](./subnetting_quiz.pka) — open with Cisco Packet Tracer to view the completed topology.
