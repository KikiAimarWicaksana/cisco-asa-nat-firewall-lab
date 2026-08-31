# 🛡️ Cisco ASA NAT & Firewall Lab

> **Enterprise-style network security lab built with Cisco Packet Tracer**
>
> This project demonstrates the implementation of a segmented network architecture using **Cisco ASA 5506-X**, including **firewall policies, NAT/PAT, static NAT, DMZ segmentation, and access control using ACLs**.

---

## 📌 Project Overview

This lab simulates a small enterprise network where internal users, public-facing services, and external users are separated into different security zones.

The **Cisco ASA 5506-X** acts as the central security gateway between:

- 🔵 **Internal Network** — trusted user devices
- 🟢 **DMZ** — public-facing servers
- 🔷 **Outside Network** — simulated Internet / external users

The main objective is to control **who can access what service**, while allowing legitimate traffic and preventing unauthorized access.

---

## 🏗️ Network Architecture

![Network Topology](topology.png)

### Security Zones

| Zone | Purpose | Network |
|---|---|---|
| 🔵 INSIDE | Internal users | `192.168.10.0/24` |
| 🟢 DMZ | Public-facing servers | `192.168.30.0/24` |
| 🔷 OUTSIDE | External / Internet simulation | `200.100.20.0/24` |

The Cisco ASA sits between these zones and enforces the security policy.

---

# 🧩 Network Components

| Device | Role |
|---|---|
| **Cisco ASA 5506-X** | Firewall, NAT/PAT & traffic control |
| **Router2** | Internal network gateway |
| **Router7** | DMZ network gateway |
| **Router5** | Outside / Internet simulation |
| **PC1 / PC2** | Internal clients |
| **WEB Server** | HTTP service |
| **FTP Server** | FTP service |
| **PC3** | External client |

---

# 🌐 IP Addressing

### Internal Network

| Device | Interface | IP Address |
|---|---|---|
| ASA | Inside | `192.168.1.1/30` |
| Router2 | ASA-facing | `192.168.1.2/30` |
| PC1 | LAN | `192.168.10.2/24` |
| PC2 | LAN | `192.168.20.2/24` |

### DMZ Network

| Device | Interface | IP Address |
|---|---|---|
| ASA | DMZ | `192.168.2.1/30` |
| Router7 | ASA-facing | `192.168.2.2/30` |
| WEB Server | LAN | `192.168.30.2/24` |
| FTP Server | LAN | `192.168.40.2/24` |

### Outside Network

| Device | Interface | IP Address |
|---|---|---|
| ASA | Outside | `200.100.10.1/29` |
| Router5 | ASA-facing | `200.100.10.2/29` |
| PC3 | External LAN | `200.100.20.2/24` |

---

# 🔥 Firewall Security Policy

The firewall is configured according to the principle of **least privilege**.

Only required services are exposed.

| Source | Destination | Service | Result |
|---|---|---|---|
| 🔵 Internal | 🟢 WEB Server | HTTP / TCP 80 | ✅ ALLOW |
| 🔵 Internal | 🟢 FTP Server | FTP / TCP 21 | ✅ ALLOW |
| 🔷 Outside | 🟢 WEB Server | HTTP / TCP 80 | ✅ ALLOW |
| 🔷 Outside | 🟢 FTP Server | FTP / TCP 21 | ❌ DENY |

### Security Concept

The objective is not simply to make everything reachable.

Instead:

> **Allow legitimate business traffic while restricting unnecessary access.**

This simulates how a firewall can protect internal resources while still exposing selected services to external users.

---

# 🔄 NAT Implementation

## 1. PAT — Internal Users

Internal clients use **PAT (Port Address Translation)** when accessing the outside network.

```text
PC1
192.168.10.2
     │
     ▼
Router2
     │
     ▼
Cisco ASA
     │
     │ PAT
     ▼
200.100.10.1
     │
     ▼
Outside Network
