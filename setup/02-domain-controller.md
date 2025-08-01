# 🧩 Step 2: Install and Configure Domain Controller

This step will guide you through installing Active Directory Domain Services (AD DS) and promoting the Windows Server to a Domain Controller (DC).

## ✅ Prerequisites
- Windows Server VM already installed and running

- Static IP assigned (e.g., 192.168.56.10)

- Can ping and communicate with client VM

## 🧱 2. Install Active Directory Domain Services (AD DS)

Open Server Manager > Manage > Add Roles and Features

  ➡ Role-based or feature-based installation
  
  ➡ Select local server
  
  ➡ Check: Active Directory Domain Services
  
  ➡ Install

  ![dc-install-ADDS-example](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/dc-install-ADDS-example.png)

  ![dc-install-ADDS-example2](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/dc-install-ADDS-example-2.png)
  
## 🧭 3. Promote to Domain Controller

After AD DS is installed, you will see a yellow warning at the top of Server Manager.

1. Click "Promote this server to a domain controller"

![promote-server-to-DC](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/promote-server-to-DC.png)

2. Select "Add a new forest"

    - Root domain name: lab.local (you can choose your own)
  
![add-new-forest](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/add-new-forest.png)

3. Set a Directory Services Restore Mode (DSRM) password

![set-password](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/set-password.png)

4. Leave defaults for DNS and NetBIOS name

5. Click Next and then Install

6. Server will reboot automatically after installation

## 🧪 4. Verify Domain Controller Setup

After reboot:

- Log in as: lab\Administrator

![reboot](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/reboot.png)

- Open Server Manager > Tools > Active Directory Users and Computers

![AD-users-computers](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/AD-users-computers.png)

- Your domain (e.g. lab.local) should appear on the left

![domain-lab-local](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/domain-lab-local.png)





