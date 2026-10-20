# Project 01 - Basic LAN with DHCP configuration

**Tools:** Cisco Packet Tracer
**Network:** MY_LAN
**Date:** October 2026


## Objective

Design and implement a basic Local Area Network (LAN) with a dedicated DHCP server to automatically assign an IP address to all connected hosts. The goal is to eliminate manually IP configuration by centralizing address assignments through a DHCP server, simulating how IP addresses work in a real office environment.


## Network Topology

[Topology]
<img width="567" height="484" alt="DHCP Topology" src="https://github.com/user-attachments/assets/518f1cbe-dd42-44c8-90c8-6fd94bb1ca1b" />
**Device used:**
1 x Server-PT(DHCP server) - static IP, outside LAN boundary
1 x Cisco 2960-24TT Switch(Switch0)
3 x PC-PT (PC0, PC1, PC2)
1 x Laptop PT (Laptop0)

All end devices connected to Switch0 via Fastethernet interfaces.
The DHCP server connected directly to Switch0, serving the entire MY_LAN network


## IP Addressing Scheme

|Device: DHCP Server | IP Address: 192.168.1.2 |Assignment Method: Static | Subnet Mask: 255.255.255.0 |Default Gateway: - |Default DNS: - |

|Device: PC0 | IP Address: 192.168.1.x |Assignment Method: DHCP | Subnet Mask: 255.255.255.0 |Default Gateway: 192.168.1.1 |Default DNS: 192.168.1.2 |

|Device: PC1 | IP Address: 192.168.1.x |Assignment Method: DHCP | Subnet Mask: 255.255.255.0 |Default Gateway: 192.168.1.1 |Default DNS: 192.168.1.2|

|Device: PC2 | IP Address: 192.168.1.x |Assignment Method: DHCP | Subnet Mask: 255.255.255.0 |Default Gateway: 192.168.1.1|Default DNS: 192.168.1.2 |

|Device: Laptop0 | IP Address: 192.168.1.x |Assignment Method: DHCP | Subnet Mask: 255.255.255.0 |Default Gateway: 192.168.1.1 |Default DNS: 192.168.1.2 |

The DHCP server was assigned a static IP address (192.168.1.2) to ensure its address never changes, which is a standard practice in real networks where servers require a consistent, known address.

## DHCP Server Configuration

[DHCP Config]
<img width="698" height="701" alt="Screenshot 2026-08-17 at 12 41 10 AM" src="https://github.com/user-attachments/assets/21f438ce-bad8-4778-99c2-5555a77de823" />
**Pool Name:** serverPool
**Default Gateway:** 192.168.1.1
**DNS Server:** 192.168.1.2
**Start IP address:** 192.168.1.0
**Subnet Mask:** 255.255.255.0
**Maximum Users:** 256
**Service:** On (FastEthernet0)

The DHCP service was enabled on the server and configured with a pool named serverPool. All hosts on the network were set to receive their IP configuration automatically via DHCP rather than being manually configured.


## Host Configuration - DHCP Enabled

All four end devices were configured to obtain their IP address automatically via DHCP

[PC0 Config]
<img width="698" height="701" alt="Screenshot 2026-08-17 at 12 42 29 AM" src="https://github.com/user-attachments/assets/8f52d8f3-df0d-4c9a-80ea-a6a410dbbfb5" />
*PC0 - DHCP enabled, receiving Default Gateway 192.168.1.1 and DNS server 192.168.1.2

[PC 1 Config]
<img width="698" height="701" alt="Screenshot 2026-08-17 at 12 43 14 AM" src="https://github.com/user-attachments/assets/f9cdba4f-5141-4759-be09-bfb40a7dfde6" />
PC1 - DHCP enabled, receiving correct gateway and DNS settings

[PC2 Config]
<img width="698" height="701" alt="Screenshot 2026-08-17 at 12 44 13 AM" src="https://github.com/user-attachments/assets/09450acd-cc6e-43fb-ae52-6b5f2c18331d" />
PC2 - DHCP enabled, confirmed receiving network settings

[Laptop0 Config]
<img width="698" height="701" alt="Screenshot 2026-08-17 at 12 44 40 AM" src="https://github.com/user-attachments/assets/729d4787-e5a0-4541-a125-5098daad3ad8" />
Laptop0 - DHCP enabled, confirmed receiving network settings


## Verification - Connectivity Testing

Ping tests were conducted between hosts to confirm successful DHCP assignment and network connectivity across all devices.

**PC0 -> 192.168.1.3 (PC2)**

[PC0 Ping]
<img width="681" height="589" alt="Screenshot 2026-08-17 at 1 00 54 AM" src="https://github.com/user-attachments/assets/29edb5df-3dc4-4de9-b42b-8aaaaa884ab9" />
Packets:Sent = 4, Received = 4, Lost = 0 (0% loss)
Minimum = 0ms, Maximum = 0ms, Average = 0ms

**PC1 -> 192.168.1.3**

[PC1 Ping]

Packets:Sent = 4, Received = 4, Lost = 0 (0% loss)
Minimum = 0ms, Maximum = 0ms, Average = 0ms


**Laptop0 -> 192.168.1.4**

[Laptop0 Ping]
<img width="681" height="567" alt="Screenshot 2026-08-17 at 1 00 11 AM" src="https://github.com/user-attachments/assets/c2c917cc-2a5b-490f-bea1-796c0490ab87" />
Packets:Sent = 4, Received = 4, Lost = 0 (0% loss)
Minimum = 0ms, Maximum = 0ms, Average = 0ms

**PC2 -> 192.168.1.3**

[PC2 Ping]
<img width="675" height="435" alt="Screenshot 2026-08-17 at 12 58 36 AM" src="https://github.com/user-attachments/assets/d67bdc66-bcf7-493b-b71c-3e71255703c1" />

Packets:Sent = 4, Received = 4, Lost = 0 (0% loss)
Minimum = 0ms, Maximum = 0ms, Average = 0ms


All ping tests return 0% packet loss confirming full connectivity across the network with DHCP assigned addresses


## What I learned

Successfully assign a DHCP server to automatically distribute IP addresses, subnet masks, default gateway, and DNS server information to all hosts on the network. This project reinforced understanding of the DORA process (Discover, Offer, Request, Acknowledge) that underlies DHCP and demonstrated why centralised IP management is essential in real networks which is manually configuring every device and would be impractical at scale.

**Note for improvement:** 
In a production environment the DHCP pool start address should begin at 192.168.1.3 or higher to exclude the gateway (.1) and server (.2) addresses from the assignable range, preventing potential conflicts. This is something I would implement in future projects.

