# 🧩 Step 3: Join Client to Domain

👨‍💻 **Goal**: Connect your Windows Client VM to the Active Directory Domain (e.g. `bredhon.lab`)

---

## 🛠️ Prerequisites

Make sure the following are complete:

- ✅ Server VM has been promoted to a Domain Controller
- ✅ Server and Client VMs can ping each other via Host-Only network
- ✅ Client VM has static IP and DNS pointing to the Server

---

## 🔧 1️⃣ Rename the Client Computer (Optional)

1. Right-click **Start** → **System**
2. Click **Rename this PC**
3. Name it something like `Client01`
4. Restart the VM

![rename-client-machine](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/rename-client-machine.png)

---

## 🌐 2️⃣ Set Static IP & DNS

If not done already, configure the network:

1. Right-click the **network icon** → **Open Network & Internet settings**
2. Click **Change adapter options**
3. Right-click the **Host-Only Adapter** → **Properties**
4. Select `Internet Protocol Version 4 (TCP/IPv4)` → Click **Properties**
5. Set the following:

| Setting              | Value               |
|----------------------|---------------------|
| IP address           | `192.168.56.20`    |
| Subnet mask          | `255.255.255.0`     |
| Default gateway      | `192.168.56.1` (or leave blank) |
| Preferred DNS server | `192.168.56.10` (your DC's IP) |

![client-machine-dns-ip](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/client-machine-dns-ip.png)

---

## 🏁 3️⃣ Join the Domain

1. Open **Accounts** settings

![settings-accounts](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/settings-accounts.png)

2. Click **Access work or school**

3. Click **Connect**

![connect](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/connect.png)

4. Click **Join this device to a local Active Directory domain**

![join-device-to-ad-domain](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/join-device-to-ad-domain.png)

5. Enter your domain name: `lab.local`

![enter-domain-name](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/enter-domain-name.png)

6. Provide credentials:

   - Username: `Administrator`
   - Password: the DC’s password

![enter-credentials](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/enter-credentials.png)

7. Restart when prompted

---

## 🧪 4️⃣ Verify Domain Join

After reboot:

1. At the login screen, select **Other User**
2. Log in using:

   - `LAB\Administrator` or `LAB\your_domain_user`
  
![sign-in-domain](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/sign-in-domain.png)

3. If successful, you’re now on the domain 🎉

---

## 🆘 Troubleshooting

| Problem                  | Solution                                                  |
|--------------------------|-----------------------------------------------------------|
| Cannot find domain       | ✅ Ensure DNS points to DC IP (`192.168.56.10`)          |
| Ping to DC fails         | ✅ Check VM network adapters and firewall settings         |
| Login failed             | ✅ Use correct domain account format: `DOMAIN\Username`    |

---

## ✅ TL;DR

- Set Client IP and DNS correctly
- Make sure both VMs can communicate
- Join domain using DC credentials
- Log in with domain account

