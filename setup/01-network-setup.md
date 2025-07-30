# 🌐 Step 1: Virtual Network Setup

## 🪜 Steps:

1. Open VirtualBox > Network Manager

2. Create a host-only network & a NAT network

3. In each VM's settings:

     - Network Adapter 1 > Attach to: Host-only Adapter
     - Network Adapter 2 > Attach to: NAT

4. Boot both VMs

5. Set static IP on the Server VM

6. Run 'ipconfig' and 'ping' to test connectivity

---

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

## ✅ VirtualBox Configuration (per VM)

1. Open VirtualBox Manager

2. Select VM → Settings → Network

### 🔌 Adapter 1: Host-Only

1. Enable Network Adapter ✅

2. Attached to: Host-Only Adapter

- Name: e.g., vboxnet0

     - Internal, isolated network for VM-to-VM communication

     - No internet access

     - IPs like 192.168.56.x


### 🔌 Adapter 2: NAT

1. Enable Network Adapter ✅

2. Attached to: NAT

     - Internet access through host machine

     - Used for downloading packages or Windows updates

---

## 🌐 IP Configuration Example

### In Windows Server VM (e.g., DC01):

1. Open Control Panel > Network and Sharing Center > Change Adapter Settings

2. Identify the Host-Only Adapter

3. Double click Internet Protocol Version 4

4. Set static IP:

```
IP Address:      192.168.56.10
Subnet Mask:     255.255.255.0
Default Gateway: (leave blank)
Preferred DNS:   127.0.0.1 (for domain controller)
```

💡 Leave NAT adapter as DHCP (auto IP).

---

## 🖥️ ipconfig & ping testing

✅ 1️⃣ On the Domain Controller (DC)

🔹 Boot the VM

🔹 Open Command Prompt and run:

```bash
ipconfig
```

![ipconfig-dc-example](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/ipconfig-dc-example.png)

🔹  Test connectivity to the Client VM:

```bash
ping 192.168.56.20
```

![dc-ping-fail-example](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/dc-ping-fail-example.png)

### 🧯 Troubleshooting

If any ping fails

- 🔒 Check Firewall: Temporarily disable Windows Firewall (Control Panel → Windows Defender Firewall → Turn off)

- 🧩 Check VM Network Adapters: Ensure they are enabled

- 📝 Check Static IP settings: Make sure no typos or misconfigurations

### In this case, we try to turn off the firewall first

![dc-turn-off-firework](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/dc-turn-off-firework.png)

### ping the Client VM again

![dc-ping-success-example](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/dc-ping-success-example%20(1).png)

### Now you may try to ping the Domain Controller in the same way.
