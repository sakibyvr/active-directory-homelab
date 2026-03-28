# 🧪 Active Directory Homelab (Windows Server 2022)

<p align="center">
  <img src="https://img.shields.io/badge/Project-Active%20Directory%20Lab-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Platform-Windows%20Server%202022-0078D6?style=for-the-badge&logo=windows" />
  <img src="https://img.shields.io/badge/Hypervisor-VirtualBox-183A61?style=for-the-badge&logo=virtualbox" />
  <img src="https://img.shields.io/badge/Focus-IT%20Support%20%7C%20SysAdmin-green?style=for-the-badge" />
</p>

---

## 📌 0. Table of Contents

- [1. Project Overview](#1-project-overview)
- [2. Lab Architecture](#2-lab-architecture)
- [3. Windows Server Installation & Troubleshooting](#3-windows-server-installation--troubleshooting)
- [4. Domain Controller Setup (DC01)](#4-domain-controller-setup-dc01)
- [5. Client Setup & Domain Join](#5-client-setup--domain-join)
- [6. Security Groups & Access Control](#6-security-groups--access-control)
- [7. Delegation of Control (Password Reset)](#7-delegation-of-control-password-reset)
  
---

## 📌 1. Project Overview

This project documents my hands-on experience building an **Active Directory home lab** using **Windows Server 2022** and **VirtualBox**.

The lab simulates a real-world IT environment and focuses on:

- System administration  
- Active Directory management  
- User and access control  
- Troubleshooting  

---

## 🏗️ 2. Lab Architecture
DC01 (Domain Controller)
│
├── Active Directory (homelab.ca)
├── DNS Server
│
└── Client Machine
└── WIN11-CL01 (Domain Joined)


---

## ⚙️ 3. Windows Server Installation & Troubleshooting

### ❌ Issue Encountered

![License Error](../screenshots/01-license-error.png)

**Figure 1:** License error during installation

---

### 🔍 Troubleshooting

- Checked virtualization settings  
- Adjusted VM resources  
- Reviewed system security  

---

### 🧠 Root Cause

VirtualBox **Unattended Installation** caused the failure.

---

### ✅ Resolution

- Recreated VM  
- Disabled unattended setup  

---

### ✔️ Result

![Server Installed](../screenshots/02-server-installed.png)

**Figure 2:** Successful installation

---

## 🏢 4. Domain Controller Setup (DC01)

### ⚙️ Configuration

- Installed AD DS  
- Installed DNS  
- Promoted to Domain Controller  
- Created domain: `homelab.ca`  

---

### 🔐 Verification

![Domain Login](../screenshots/03-login-domain.png)

**Figure 3:** Domain login success  

![DC Ready](../screenshots/04-dc-ready.png)

**Figure 4:** Services running  

---

## 💻 5. Client Setup & Domain Join

### 🔗 Domain Join

![Domain Join](../screenshots/05-domain-join.png)

![Domain Joined](../screenshots/06-domain-joined.png)

---

### 🗂️ OU Structure

![OU Structure](../screenshots/07-ou-structure.png)

---

### ✔️ Verification

![Computer Added](../screenshots/08-computer-added.png)

![Client Login](../screenshots/09-client-login.png)

---

## 🔐 6. Security Groups & Access Control

### 🛠️ Steps

1. Open ADUC  
![Step](../screenshots/10-open-active-directory-users-and-computers.png)

2. Review structure  
![Step](../screenshots/11-domain-structure-overview.png)

3. Create group  
![Step](../screenshots/12-create-new-group-menu.png)

4. IT group  
![Step](../screenshots/13-create-it-group.png)

5. Employees group  
![Step](../screenshots/14-create-employees-group.png)

6. Verify OU  
![Step](../screenshots/15-employees-ou-structure.png)

7. Add user  
![Step](../screenshots/16-add-user-to-group.png)

8. Verify members  
![Step](../screenshots/17-group-members-tab.png)  
![Step](../screenshots/18-group-members-confirmation.png)

9. User side verification  
![Step](../screenshots/19-user-member-of-tab.png)

---

## 🔐 7. Delegation of Control (Password Reset)

### 🎯 Objective

Enable IT support to reset passwords without admin privileges.

---

### 🛠️ Steps

1. Start delegation  
![Step](../screenshots/20-delegation-start.png)

2. Select IT_Group  
![Step](../screenshots/21-select-itgroup.png)

3. Assign permissions  
![Step](../screenshots/22-permission.png)

---

### 💻 Verification

4. Reset password  
![Step](../screenshots/23-reset-password.png)

5. Success confirmation  
![Step](../screenshots/24-success.png)

---

### 🔍 Validation

- Password reset allowed  
- Other actions restricted  

---

### 📊 Supporting Evidence

![Step](../screenshots/17-group-members-tab.png)  
![Step](../screenshots/18-group-members-confirmation.png)  
![Step](../screenshots/19-user-member-of-tab.png)

---
