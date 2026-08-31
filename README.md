# 🛡️ Cisco ASA NAT & Firewall Lab

> **Network Security Lab using Cisco Packet Tracer**

A hands-on network security lab that simulates a small enterprise network using **Cisco ASA 5506-X** as the central firewall.

This project demonstrates practical implementation of:

- Network segmentation
- Firewall security zones
- Security levels
- Access Control Lists (ACL)
- Static NAT
- PAT
- DMZ architecture
- HTTP and FTP services
- Connectivity and firewall troubleshooting

---

## 🎯 Project Overview

The network is divided into three main security zones:

- 🔵 **INSIDE** — trusted internal users
- 🟢 **DMZ** — servers providing network services
- 🔴 **OUTSIDE / INTERNET** — simulated external users

The **Cisco ASA 5506-X** is positioned between these zones and controls which traffic is allowed to pass.

The main objective of this lab is to demonstrate how a firewall can:

> **Allow legitimate traffic while restricting unauthorized access.**

---

# 🏗️ Network Topology

![Cisco ASA NAT & Firewall Lab](topology_nat_firewall.png)

### Network Architecture

```text
                         🔴 OUTSIDE / INTERNET
                                  │
                                 PC3
                                  │
                              Router3
                                  │
                                  │
                           ┌──────▼──────┐
                           │ Cisco ASA   │
                           │   5506-X    │
                           │  FIREWALL   │
                           └──────┬──────┘
                                  │
                    ┌─────────────┴─────────────┐
                    │                           │
                    ▼                           ▼
              🔵 INSIDE                     🟢 DMZ
                    │                           │
                 Router1                    Router2
                    │                           │
                ┌───┴───┐                 ┌────┴────┐
                │       │                 │         │
               PC1     PC2              WEB       FTP
