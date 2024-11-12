---
title: "#4. VLSM, Dynamic Routing, Wildcard Mask"
excerpt: ""

categories:
  - Networking
tags:
  - [Network, VLSM, Dynamic Routing]

permalink: /networking/post-4-230831/

toc: true
toc_sticky: true

date: 2023-08-31
last_modified_at: 2023-08-31
---

# [Day 4] VLSM, Dynamic Routing, Wildcard Mask

## VLSM (Variable Length Subnet Mask)

: Dividing a subnet into unequal ranges.

> **Method**
> 
1. Arrange networks in order of size.
2. Consider the required size (think of the host count + 2).
3. Calculate each network (if you know the size, you can also calculate the prefix).
4. The representative address of the next network is naturally determined.

> **Example 1)** **10.20.30.0 /24**
> 
1. 60 hosts
2. 120 hosts
3. 33 hosts

✍🏻 Solution) Arrange in order of size: 2 > 1 > 3

   Required size: 2 (128) > 1 (64) > 3 (64) *When thinking about the size, add +2 to the number of hosts.

![Untitled](Untitled.png)

> **Problem 1)** **10.20.30.0 /24**
> 

Subnet using VLSM to minimize IP waste.

- Network A = 31 hosts
- Network B = 100 hosts
- Network C = 14 hosts

✍🏻 Solution)

1. Arrange in order of size: B (100) - A (31) - C (14)
2. Determine the network size and calculate the prefix.
   B: 128 /25  
   A: 64 /26  
   C: 16 /28
3. Representative address determined:
   B: 10.20.30.0 /25  
   A: 10.20.30.128 /26  
   C: 10.20.30.192 /28

> **Problem 2)**
> 

(Not saved…)

---

## Dynamic Routing

Dynamic Routing: Automatic + Flexible

Downloaded GNS3 program.

- **Distance Vector**
    - RIP (Routing Information Protocol)
    - Provides processed information (e.g., "R2 is to the right").
    - Looks at distance and direction.
    - Transfers the routing table itself (e.g., if R2's routing table is passed to R1, R1 understands there is R2 to the right +1, and R3 to the right +2).
    - R1 ↔ R2 ↔ R3
- **Link-state: OSPF (Most Commonly Used)**
    - Protocol that automatically adopts the optimal path.
    - Unprocessed information → builds the routing table directly.
    - Shares status (e.g., "There is R3 on my right").
    - Does not exchange routing table information.
    - OSPF (Open Shortest Path First)
        - Area 0 must always exist (backbone area).
        - Advertises the network it belongs to.
        - Routers close to each other form a "neighbor" relationship.
    - Determines problematic paths and communicates via alternate routes.

*Use static routing if you want to prioritize a specific path.

## OSPF Configuration <Advertisement>

After powering on the router, double-click to open the CLI window.

![Untitled](Untitled%201.png)

#R1

![Untitled](Untitled%202.png)

1. Declare IP address (f0/0)
2. **#router ospf 10**
    - #router = routing protocol
    - #ospf = ospf protocol
    - #10 = <process ID> (it can vary for each router, but it can be standardized)
3. **#router(-id) 1.1.1.1 [Router ID] // (-id is optional)**
    - # identifies each router.
4. **#network 1.1.1.10  0.0.0.0  area 0  
[Interface Address] [Wildcard Mask] [Area]**
    - network = advertisement
    - 1.1.1.10 = interface address
    - 0.0.0.0 = wildcard mask (reverse of 255.255.255.255, which defines the host itself)
    - area 0
        - a: area
        - 0: backbone area, must exist in OSPF configuration.

⇒ Nbr 2.2.2.2

#R2

![Untitled](Untitled%203.png)

1. Declare IP address twice (f0/0, f0/1) // Not strictly necessary
2. #router ospf 10
3. #router -id 2.2.2.2
4. #network 1.1.1.20  0.0.0.0  area 0

    ⇒ Nbr 1.1.1.1

5. #network 2.2.2.10  0.0.0.0  area 0

    ⇒ Nbr 3.3.3.3

#R3

![Untitled](Untitled%204.png)

1. Declare IP address (f0/1)
2. #router ospf 10
3. #router-id 3.3.3.3
4. #network 2.2.2.20  0.0.0.0  area 0

    ⇒ Nbr 2.2.2.2

    ⇒ ping 1.1.1.10 (R1’s f0/0) successful.

---

> **How to Advertise**
> 
1. Advertise the interface address itself (preferably this method).

   network                   1.1.1.10                                0.0.0.0                     area 0

   network <interface IP> <fixed wildcard mask> <area number>

2. Directly advertise the network segment.

   network                     1.1.1.0                                      0.0.0.255                     area 0

   network <connected network’s representative address> <wildcard mask> <area number>

**Backbone area**
    : Area 0 must be central as it acts as the backbone.
      Area 1, 2 act as arms on the left and right.
      If the order of the area is 1, 0, 2 instead of 1, 2, 0, communication issues arise.

Virtual link

- Used to link areas when they do not connect as required.

---

## Wildcard Mask

Inverting the subnet mask, e.g., 255.255.255.0 → 0.0.0.255.

- 1 in subnet mask = Fixed, 0 = Don’t care.
- Wildcard mask **0 = Fixed**, **1 = Don’t care**.

<aside>
💡 1.1.1.0's WM = 0.0.0.1

0 in wildcard mask is fixed → Fixes up to IP 1.1.1**l.**0 (red line).

.1 = **00000001** (binary)

⇒ Meaning? Only the $2^0$ position is unfixed in the binary of the 4th octet.

⇒ Range? 1.1.1.0 ~ 1.1.1.3

⇒ Scope?

</aside>

1.1.1.0, 1.1.1.1

<aside>
💡 1.1.1.0 WM = 0.0.0.**254**

254 in binary = **11111110**

</aside>

   00000000

0 00000000

1 00000001

2 00000010

3 00000011

4 00000100

   11111110

1.1.1.1

0000001

0000011

00000000 0

00000010 2

00000100 4

11111110

---

### Assignment

![Untitled](Untitled%205.png)

✍🏻 Solution)

1. Subnetting of 2 private networks (VLSM) **10.10.10.128 /25**
    - Network A (40 hosts)
        - 10.10.10.128 ~ 10.10.10.191 /26
        - SM: 255.255.255.192
    - Network B (10 hosts) **128.30.20.16 /29**
        - 10.10.10.192 ~ 10.10.10.217 /28
        - SM: 255.255.255.240
2. Subnetting of 2 public networks
    - 128.30.20.16~.19 /30
    - 128.30.20.20 ~.23 /30
3. OSFP Configuration
   - Router ID
   - Use `do sh ip int br` command to view and enter network.
4. Test communication with Ping
    - R3(config-router)#do ping 10.10.10.130 source 10.10.10.195
