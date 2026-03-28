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

This project demonstrates a **hands-on Active Directory home lab** built using:

- **Windows Server 2022**
- **Oracle VirtualBox**

The objective is to simulate a real enterprise IT environment and gain practical experience in:

- Active Directory deployment  
- User and group management  
- Domain-based authentication  
- Access control using security groups  
- Delegation of administrative tasks  
- Troubleshooting system and configuration issues  

---

## 🏗️ 2. Lab Architecture

DC01 (Domain Controller)
│
├── Active Directory (homelab.ca)
├── DNS Server
│
└── Client Machine
└── WIN11-CL01 (Domain Joined)


### Components

- **DC01** → Windows Server 2022 (Domain Controller)
- **CL01** → Windows 11 Client Machine
- **Domain** → homelab.ca
- **Tools** → AD DS, DNS, RSAT

---

## ⚙️ 3. Windows Server Installation & Troubleshooting

### ❌ Issue Encountered

![License Error](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/01-license-error.png)

During installation, Windows Server failed with:

> "Windows cannot find the Microsoft Software License Terms"

---

### 🔍 Troubleshooting Steps

- Verified virtualization settings in BIOS  
- Adjusted VM RAM and CPU allocation  
- Checked Windows security features  

Despite these steps, the issue persisted.

---

### 🧠 Root Cause

The issue was caused by **VirtualBox Unattended Installation**, which interfered with the setup process by skipping required steps.

---

### ✅ Resolution

- Recreated the virtual machine  
- Disabled unattended installation  
- Restarted installation  

---

### ✔️ Result

![Server Installed](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/02-server-installed.png)

Windows Server installed successfully and Server Manager launched correctly.

---

### 🧠 Key Learning

- Always validate hypervisor configuration  
- Automation tools can introduce hidden issues  
- Structured troubleshooting is essential in IT  

---

## 🏢 4. Domain Controller Setup (DC01)

### ⚙️ Configuration Steps

- Installed **Active Directory Domain Services (AD DS)**  
- Installed **DNS Server**  
- Promoted server to Domain Controller  
- Created new forest: `homelab.ca`  
- Configured DSRM password  

---

### 🔐 Verification

![Domain Login](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/03-login-domain.png)

Successfully logged in using:

HOMELAB\Administrator  


---

![DC Ready](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/04-dc-ready.png)

Server Manager confirms:

- AD DS running  
- DNS running  
- System healthy  

---

### 🧠 Key Learning

- DNS is critical for Active Directory functionality  
- Domain Controllers centralize authentication  
- Always validate services after promotion  

---

## 💻 5. Client Setup & Domain Join

### ⚙️ Client Configuration

- Created VM: **WIN11-CL01**  
- Set DNS → DC01 IP address  
- Verified connectivity  

---

### 🔗 Domain Join

![Domain Join](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/05-domain-join.png)

Client joined domain: `homelab.ca`

---

![Domain Joined](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/06-domain-joined.png)

Confirmed:

- Computer name → WIN11-CL01.homelab.ca  
- Domain → homelab.ca  

---

### 🗂️ Organizational Units

![OU Structure](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/07-ou-structure.png)

Created OUs:

- Employees  
- IT  
- Computers  

---

### ✔️ Verification

![Computer Added](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/08-computer-added.png)

Client appears in Active Directory  

---

![Client Login](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/09-client-login.png)

Successfully logged in using domain user  

---

### 🧠 Key Learning

- DNS is essential for domain communication  
- Domain join validates infrastructure  
- Authentication confirms correct setup  

---

## 🔐 6. Security Groups & Access Control

### 🎯 Objective

- Create security groups  
- Assign users to groups  
- Verify group membership  

---

### 🛠️ Steps

#### 1. Open ADUC
![Step](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/10-open-active-directory-users-and-computers.png)

#### 2. Review Domain Structure
![Step](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/11-domain-structure-overview.png)

#### 3. Create New Group
![Step](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/12-create-new-group-menu.png)

#### 4. Create IT_Group
![Step](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/13-create-it-group.png)

#### 5. Create Employees_Group
![Step](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/14-create-employees-group.png)

#### 6. Verify OU Structure
![Step](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/15-employees-ou-structure.png)

#### 7. Add User to Group
![Step](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/16-add-user-to-group.png)

#### 8. Verify Membership (Group Side)
![Step](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/17-group-members-tab.png)

![Step](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/18-group-members-confirmation.png)

#### 9. Verify Membership (User Side)
![Step](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/19-user-member-of-tab.png)

---

### 🧠 Key Learning

- Security groups simplify permission management  
- OUs organize the environment logically  
- Always verify membership from both perspectives  

---

## 🔐 7. Delegation of Control (Password Reset)

### 🎯 Objective

Allow IT support users to reset passwords without full administrative privileges.

---

### ⚙️ Setup

- Created groups: **HR_Group**, **IT_Group**  
- Assigned users accordingly  

---

### 🛠️ Delegation Steps

#### 1. Start Delegation Wizard
![Step](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/20-delegation-start.png)

#### 2. Select IT_Group
![Step](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/21-select-itgroup.png)

#### 3. Assign Permissions
![Step](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/22-permission.png)

---

### 💻 RSAT Setup

Installed RSAT on client machine to manage AD remotely.

---

### ✅ Verification

#### Reset Password
![Step](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/23-reset-password.png)

#### Confirmation
![Step](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/24-success.png)

---

### 🔍 Validation

- Password reset successful  
- Unauthorized actions restricted  

---

### 🧠 Key Learning

- Delegation enforces least privilege  
- RBAC improves security and scalability  
- RSAT enables remote administration  

---

## 👨‍💻 Author

Najmus Sakib

---
