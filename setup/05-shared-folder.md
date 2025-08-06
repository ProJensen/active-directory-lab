# 📁 Step 5: Create a Shared Folder with AD Permissions

👨‍💻 **Goal**: Create a shared folder on the Domain Controller and manage access using Active Directory groups.

---

## 🛠️ Prerequisites

- A functioning Domain Controller (e.g. `DC01`) with domain `lab.local`
- At least one AD user (e.g. `colep`) and client joined to the domain
- Client VM can connect to the server via internal network

---

## 🗃️ 1️⃣ Create the Shared Folder

1. On the Domain Controller, create a folder: `C:\Shared\LabDocs`

![create-shared-folder](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/(5)create-shared-folder.png)

2. Right-click the folder → **Properties**

3. Go to the **Sharing** tab → Click **Advanced Sharing**

![advanced-sharing](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/(5)advanced-sharing.png)

4. Tick **Share this folder**
5. Set **Share Name**: `LabDocs`

![share-this-folder](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/(5)share-this-folder.png)

6. Click **Permissions**:
  - Remove `Everyone`
  - Click **Add** `LabShareAccess` (we’ll create this group in Step 2)

![Add Permission](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/(5)add-LabShareAccess-permission.png)

Click **Apply** & **OK** to finish sharing the folder.

---

## 👥 2️⃣ Create an AD Group for Access

1. Open **Active Directory Users and Computers** (`dsa.msc`)

2. Right-click your OU (e.g. `LabUsers`) → **New → Group**

![Create Group](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/(5)create-group.png)

3. Name it: `LabShareAccess`

4. Group scope: **Global**; Group type: **Security**

![Name Group](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/(5)name-group-LSA.png)

5. Click **OK**

---

## 👤 3️⃣ Add Users to the Group

1. Double-click the `LabShareAccess` group → **Members** tab

2. Click **Add**

![Member Tab](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/(5)labshareaccess-members-tab.png)

3. Type the username (e.g. `colep`) → Click **Apply** & **OK**

![Add colep](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/(5)add-colep.png)

4. The user should now appear in the list

---

## 🔐 4️⃣ Set NTFS Permissions

1. On the Domain Controller, right-click `C:\Shared\LabDocs` → **Properties**

2. Go to **Security** tab → Click **Edit**

![Edit in Security tab](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/(5)LabDoxs-Security.png)

3. Click **Add** → Type `LabShareAccess` → Click **Apply** & **OK**

![Add Group to Security](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/(5)add-LabShareAccess.png)

4. Assign permissions:
- ✅ Read & Execute
- ✅ List folder contents
- ✅ Read
> Optional: Add **Modify** if write access is needed

![Permission for Group](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/(5)permission-for-group.png)

---

## 🖥️ 5️⃣ Access the Folder from Client VM

From your **Windows 10/11 client**:

1. Press `Win + R` → Type:  
`\\lab.local\LabDocs`

![Access from Server Name](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/(5)lab.local%5CLabDocs.png)

or use server IP:  
`\\192.168.56.10\LabDocs`

![Access from Server IP](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/(5)192.168.56.10%5CLabDocs.png)

2. Press Enter — you should see the shared folder contents

![Shared Folder](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/(5)shared-folder.png)

3. If prompted for login, enter:  
`LAB\colep`

✅ Only users in the `LabShareAccess` group should be able to access this folder.

---

## 🆘 Troubleshooting

| Problem                      | Solution                                                        |
|------------------------------|-----------------------------------------------------------------|
| “Access Denied”              | Check both Share + NTFS permissions                             |
| Can't find folder path       | Use correct UNC path (`\\server\sharename`)                     |
| Still asking for credentials | Make sure client is joined to the domain and using domain user  |
| Firewall blocking sharing    | Temporarily disable Windows Defender Firewall on server         |

---

## ✅ TL;DR

- Create shared folder `C:\Shared\LabDocs` on DC
- Share it and assign permissions
- Create AD group `LabShareAccess`
- Add domain users to the group
- Set NTFS access
- Connect from client using `\\lab.local\LabDocs`
