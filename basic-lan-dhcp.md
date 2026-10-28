# Project 01 - Basic LAN with DHCP configuration

**Tools:** Cisco Packet Tracer

**Network:** MY_LAN

**Date:** October 2026


## Objective

Design and implement a basic Local Area Network (LAN) with a dedicated DHCP server to automatically assign IP addresses to all connected hosts. The goal is to eliminate manual IP configuration by centralizing address assignments through a DHCP server, simulating how IP addressing works in a real office environment.


## Network Topology

[Topology]

<img width="567" height="484" alt="DHCP Topology" src="https://github.com/user-attachments/assets/518f1cbe-dd42-44c8-90c8-6fd94bb1ca1b" />

**Devices used:**
1 x Server-PT(DHCP server) - static IP, outside LAN boundary
1 x Cisco 2960-24TT Switch(Switch0)
3 x PC-PT (PC0, PC1, PC2)
1 x Laptop-PT (Laptop0)

All end devices were connected to Switch0 via FastEthernet interfaces. The DHCP server was connected directly to Switch0, serving the entire MY_LAN network.

## IP Addressing Scheme

|Device: DHCP Server | IP Address: 192.168.1.2 |Assignment Method: Static | Subnet Mask: 255.255.255.0 |Default Gateway: - |Default DNS: - |

|Device: PC0 | IP Address: 192.168.1.11 |Assignment Method: DHCP | Subnet Mask: 255.255.255.0 |Default Gateway: 192.168.1.1 |Default DNS: 192.168.1.2 |

|Device: PC1 | IP Address: 192.168.1.12 |Assignment Method: DHCP | Subnet Mask: 255.255.255.0 |Default Gateway: 192.168.1.1 |Default DNS: 192.168.1.2|

|Device: PC2 | IP Address: 192.168.1.13 |Assignment Method: DHCP | Subnet Mask: 255.255.255.0 |Default Gateway: 192.168.1.1|Default DNS: 192.168.1.2 |

|Device: Laptop0 | IP Address: 192.168.1.14 |Assignment Method: DHCP | Subnet Mask: 255.255.255.0 |Default Gateway: 192.168.1.1 |Default DNS: 192.168.1.2 |


The DHCP server was assigned a static IP address (192.168.1.2) to ensure its address never changes, which is standard practice in real networks where servers require a consistent, known address.

[DHCP Server Static IP]

<img width="698" height="701" alt="Screenshot 2026-08-17 at 12 39 40 AM" src="https://github.com/user-attachments/assets/b28f8b78-acf6-42dc-b242-eb59c780d63c" />


## DHCP Server Configuration

[DHCP Config]

<img width="697" height="694" alt="Screenshot 2026-10-27 at 5 36 23 PM" src="https://github.com/user-attachments/assets/bd0a6e7c-d522-440f-895d-983012230fa2" />

- **Pool Name:** serverDHCPPool
- **Default Gateway:** 192.168.1.1
- **DNS Server:** 192.168.1.2
- **Start IP Address:** 192.168.1.10
- **Subnet Mask:** 255.255.255.0
- **Maximum Users:** 246
- **Service:** On (FastEthernet0)


The DHCP service was enabled on the server and configured with a pool named serverPool. All hosts on the network were set to receive their IP configuration automatically via DHCP rather than being manually configured.


## Host Configuration - DHCP Enabled

All four end devices were configured to obtain their IP addresses automatically via DHCP. Each host released its previous lease (`ipconfig /release`), requested a new one (`ipconfig /renew`), and was then checked with `ipconfig`.

[PC0 Config]

<img width="698" height="701" alt="Screenshot 2026-08-17 at 12 42 29 AM" src="https://github.com/user-attachments/assets/8f52d8f3-df0d-4c9a-80ea-a6a410dbbfb5" />

PC0 - DHCP enabled, receiving Default Gateway 192.168.1.1 and DNS server 192.168.1.2.

[PC0 ipconfig]

<img width="697" height="694" alt="Screenshot 2026-10-27 at 5 40 21 PM" src="https://github.com/user-attachments/assets/88d80775-61af-4ce5-9578-f33ae15e887f" />

PC0 - `ipconfig` showing DHCP-assigned IPv4 address 192.168.1.11, subnet mask 255.255.255.0, and default gateway 192.168.1.1.


[PC1 Config]

<img width="698" height="701" alt="Screenshot 2026-08-17 at 12 43 14 AM" src="https://github.com/user-attachments/assets/f9cdba4f-5141-4759-be09-bfb40a7dfde6" />

PC1 - DHCP enabled, receiving correct gateway and DNS settings.

[PC1 ipconfig]

<img width="697" height="694" alt="Screenshot 2026-10-27 at 5 41 36 PM" src="https://github.com/user-attachments/assets/26484dfb-c3fc-4b1f-a2e2-80d0842f91b4" />

PC1 - `ipconfig` showing DHCP-assigned IPv4 address 192.168.1.12, subnet mask 255.255.255.0, and default gateway 192.168.1.1.


[PC2 Config]

<img width="698" height="701" alt="Screenshot 2026-08-17 at 12 44 13 AM" src="https://github.com/user-attachments/assets/09450acd-cc6e-43fb-ae52-6b5f2c18331d" />

PC2 - DHCP enabled, confirmed receiving network settings.

[PC2 ipconfig]

<img width="697" height="694" alt="Screenshot 2026-10-27 at 5 43 57 PM" src="https://github.com/user-attachments/assets/cc540164-b274-45dd-a2b4-c374cabde39f" />

PC2 - `ipconfig` showing DHCP-assigned IPv4 address 192.168.1.13, subnet mask 255.255.255.0, and default gateway 192.168.1.1.


[Laptop0 Config]

<img width="698" height="701" alt="Screenshot 2026-08-17 at 12 44 40 AM" src="https://github.com/user-attachments/assets/729d4787-e5a0-4541-a125-5098daad3ad8" />

Laptop0 - DHCP enabled, confirmed receiving network settings.

[Laptop0 ipconfig]

<img width="697" height="694" alt="Screenshot 2026-10-27 at 5 45 01 PM" src="https://github.com/user-attachments/assets/08d021ce-a62a-4eb0-b140-4df98deaf036" />

Laptop0 - `ipconfig` showing DHCP-assigned IPv4 address 192.168.1.14, subnet mask 255.255.255.0, and default gateway 192.168.1.1.

## Verification - Connectivity Testing

Ping tests were conducted between hosts to confirm successful DHCP assignment and network connectivity. Each host pinged a different host's DHCP-assigned address, so no test was a self-ping.

**PC0 -> 192.168.1.12 (PC1)**


[PC0 Ping]

<img width="697" height="694" alt="Screenshot 2026-10-27 at 5 46 24 PM" src="https://github.com/user-attachments/assets/68b96cd1-97d1-401b-a186-4bc8e5bddfc6" />


- Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
- Minimum = 0ms, Maximum = 1ms, Average = 0ms


**PC1 -> 192.168.1.11 (PC0)**

[PC1 Ping]

<img width="697" height="694" alt="Screenshot 2026-10-27 at 5 47 39 PM" src="https://github.com/user-attachments/assets/178358a4-8886-4650-b21f-3c1b12729ba1" />


- Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
- Minimum = 0ms, Maximum = 0ms, Average = 0ms


**Laptop0 -> 192.168.1.13 (PC2)**

[Laptop0 Ping]

<img width="697" height="694" alt="Screenshot 2026-10-27 at 5 49 06 PM" src="https://github.com/user-attachments/assets/a82da0a1-c825-4130-8080-06bc02ba1f54" />


- Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
- Minimum = 0ms, Maximum = 0ms, Average = 0ms

**PC2 -> 192.168.1.14 (Laptop0)**

[PC2 Ping]

<img width="697" height="694" alt="Screenshot 2026-10-27 at 5 50 41 PM" src="https://github.com/user-attachments/assets/f4b00c57-315f-40bd-ab54-16b9b6adf88e" />


- Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
- Minimum = 0ms, Maximum = 0ms, Average = 0ms


All ping tests returned 0% packet loss, confirming full connectivity across the network with DHCP-assigned addresses.



## What I learned

I successfully configured a DHCP server to automatically distribute IP addresses, subnet masks, default gateways, and DNS server information to all hosts on the network. This project reinforced my understanding of the DORA process (Discover, Offer, Request, Acknowledge) that underlies DHCP and demonstrated why centralized IP management is essential in real networks, where manually configuring every device would be impractical at scale.


**Issue Found and Fixed:** 

During my first round of testing, `ipconfig` showed that PC2 was assigned 192.168.1.1, the same address as the default gateway. This happened because the DHCP pool started at 192.168.1.0, so the first host to request an address received .1. I changed the pool's start address to 192.168.1.10 (246 maximum users), which keeps the gateway (.1) and server (.2) addresses out of the assignable range. I then released and renewed each host's lease and re-ran the connectivity tests. All four hosts now receive unique addresses (192.168.1.11 to 192.168.1.14) with no overlap.


