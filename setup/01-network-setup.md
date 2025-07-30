# 🌐 Step 1: Virtual Network Setup

To simulate a real-world Active Directory lab environment using VirtualBox, we need to configure a proper virtual network that allows:

- Internal communication between virtual machines (VMs)  
- Internet access for updates and software installation  
- Isolation from external traffic for security  

This step will guide you through setting up **dual network interfaces** using **Host-Only** + **NAT** (recommended), or optionally **Bridged** if needed.

---

## 🧱 Network Architecture Overview

```text
+----------------------+
|    Host Machine      | (e.g. 192.168.56.1 - Host-Only)
+----------------------+
     |           |
     |           +---------------------> Internet (via NAT)
     |                             +-------------------------+
     v                             v                         v
+-----------+       +-----------+       +-----------+     +-----------+
|  DC01 VM  | <----> | Client01  | <-->  | (More...) |     | Internet  |
| Adapter 1: Host-Only Network    |                        |
| Adapter 2: NAT (Internet Access)                        |
+-----------+       +-----------+       +-----------+     +-----------+
```

---

## 🛠️ Create Host-Only Adapter & NAT

1. Go to File > Tools > Network Manager

2. Click Create to add a Host-Only Network

3. Configure the IP range if needed (default: 192.168.56.1/24)

![create-host-only-example](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/create-host-only-example.png)

4. Click the NAT Networks tab beside Host-Only Network

5. Click Create to add a NAT Network

![create-nat-network-example](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/create-nat-network-example.png)

## 🔌 Adapter 1 – Host-Only

- Internal, isolated network for VM-to-VM communication

- No internet access

- IPs like 192.168.56.x

## 🔌 Adapter 2 – NAT

- Internet access through host machine

- Used for downloading packages or Windows updates

