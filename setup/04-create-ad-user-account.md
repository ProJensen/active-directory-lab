# 👥 Step 4: Create Active Directory User Account

👨‍💻 **Goal**: Create a new user account in Active Directory so it can log in from a client device.

---

## 🛠️ Prerequisites

- You have a working Domain Controller (e.g. `DC01`)
- You have access to the **Active Directory Users and Computers** console (`dsa.msc`)
- You are logged in as a Domain Administrator (e.g. `LAB\Administrator`)

---

## 🧭 1️⃣ Open ADUC (Active Directory Users and Computers)

1. On your **Windows Server (DC)**  
2. Press `Win + R` → Type `dsa.msc` → Press Enter

![dsa.msc](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/dsa.msc.png)

3. This opens the **Active Directory Users and Computers** console

![AD-users-and-computers](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/AD-users-and-computers.png)

---

## 🗂️ 2️⃣ (Optional) Create an Organizational Unit (OU)

Organizational Units (OUs) help you organize users, computers, and groups for easier management and applying Group Policies.

### 📌 Why use an OU?

- Apply different **Group Policy Objects (GPOs)** to different departments or groups
- Better organization (e.g. `LabUsers`, `HR`, `IT`, `Students`)
- Simplifies administration in large environments

### ➕ How to create an OU:

1. In ADUC, right-click your domain (e.g. `lab.local`) → **New** → **Organizational Unit**

![create-OU](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/create-OU.png)

2. Name it something like:
   - `LabUsers` (for testing users)
   - `ClientComputers` (for joining workstations)
  
![lab-users](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/lab-users.png)

3. Click **OK**

![created-2-OU](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/created-2-ou.png)

Once created, you can place users or computers into this OU by dragging and dropping or during object creation.

---

## 👤 3️⃣ Create a New User

1. Right-click the `Users` folder or your custom OU (e.g. `LabUsers`) → **New** → **User**

![create-user-in-OU](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/create-user-in-OU.png)

2. Fill in the user details:
   - **First name**: Cole
   - **Last name**: Palmer
   - **User logon name**: `colep` → will become `colep@lab.local`
  
![cole-palmer](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/(4)cole-palmer.png)

3. Click **Next**
4. Set a password:
   - ✅ Uncheck "User must change password at next login" (for lab)
   - ✅ Check "Password never expires" (optional for labs)
  
![cole-palmer-pw](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/(4)cole-palmer-pw.png)

5. Click **Finish**

---

## 🧪 4️⃣ Verify the User

- You should now see the user `Cole CP. Palmer` under `LabUsers` or `Users`

![cole-palmer-created](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/(4)cole-palmer-created.png)

- Double-click the user to review:
   - Group Membership
   - Login Name
   - Profile and Account settings

📌 You may also right-click → **Move...** to place the user into another OU if needed.

---

## 💻 5️⃣ Log In from Client Device

From your Windows 10/11 Client VM:

1. Restart the VM if needed
2. On login screen → Click **Other User**
3. Log in with:
   - **Username**: `LAB\colep`
   - **Password**: the one you set earlier
  
![sigin-to-cole-palmer](https://raw.githubusercontent.com/ProJensen/active-directory-lab/refs/heads/main/screenshot/(4)login-to-cole-palmer.png)

🎉 You should now be logged in as a Domain user!

---

## 🆘 Troubleshooting

| Issue                            | Solution                                                 |
|----------------------------------|----------------------------------------------------------|
| "User not found" at login        | ✅ Check domain name spelling (e.g. `BREDHON\jensen`)     |
| Can't login                      | ✅ Make sure DNS points to the Domain Controller          |
| User forced to change password   | ✅ Edit user properties to disable that option            |

---

## ✅ TL;DR

- Use `dsa.msc` to open ADUC
- Create an OU (e.g. `LabUsers`) to organize your users
- Add new user to the OU
- Login from client using `DOMAIN\username`
