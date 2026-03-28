# Active Directory Homelab (Windows Server 2022)

## 0. Table of Contents

- [1. Project Overview](#1-project-overview)
- [2. Lab Architecture](#2-lab-architecture)
- [3. Windows Server Installation and Troubleshooting](#3-windows-server-installation-and-troubleshooting)
- [4. Domain Controller Setup DC01](#4-domain-controller-setup-dc01)
- [5. Client Setup and Domain Join](#5-client-setup-and-domain-join)
- [6. Security Groups and Access Control](#6-security-groups-and-access-control)
- [7. Delegation of Control Password Reset](#7-delegation-of-control-password-reset)
- [8. Notes for Future Expansion](#8-notes-for-future-expansion)

---

## 1. Project Overview

This project documents the process of building a functional Active Directory environment using Windows Server 2022 and VirtualBox.

The objective of this lab is to simulate a real-world IT environment and develop hands-on experience in:

- Deploying Active Directory Domain Services (AD DS)  
- Configuring DNS for domain environments  
- Managing users, groups, and organizational units  
- Implementing access control using security groups  
- Delegating administrative responsibilities  
- Troubleshooting system and configuration issues  

This lab also serves as a structured reference for interview preparation and real-world IT scenarios.

---

## 2. Lab Architecture
DC01 (Domain Controller)
│
├── Active Directory (homelab.ca)
├── DNS Server
│
└── Client Machine (WIN11-CL01)


### Environment Details

- Domain Controller: Windows Server 2022 (DC01)  
- Client Machine: Windows 11 (CL01)  
- Domain Name: homelab.ca  
- Tools Used: AD DS, DNS, RSAT  
- Hypervisor: Oracle VirtualBox  

---

## 3. Windows Server Installation and Troubleshooting

### Problem

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/01-license-error.png" width="50%" />
</p>

During installation, Windows Server setup failed with a license-related error despite using a valid ISO.

---

### Investigation

- Verified virtualization support in BIOS  
- Adjusted CPU and RAM allocation  
- Reviewed system security configurations  

These checks did not resolve the issue.

---

### Root Cause

The failure was caused by VirtualBox unattended installation, which interfered with the Windows setup process.

---

### Resolution

- Recreated the virtual machine  
- Disabled unattended installation  
- Restarted the installation  

---

### Result

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/02-server-installed.png" width="50%" />
</p>

The server installed successfully and booted into Server Manager.

---

### What I Learned

- Installation issues are not always caused by corrupted media  
- Hypervisor configurations can impact OS behavior  
- A structured troubleshooting approach is essential  

---

## 4. Domain Controller Setup DC01

### Configuration

- Installed Active Directory Domain Services (AD DS)  
- Installed DNS Server  
- Promoted the server to Domain Controller  
- Created a new forest: homelab.ca  
- Configured DSRM password  

---

### Verification

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/03-login-domain.png" width="50%" />
</p>

Successfully logged in using the domain administrator account.

---

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/04-dc-ready.png" width="50%" />
</p>

Verified AD DS and DNS services are running correctly.

---

### What I Learned

- DNS is essential for Active Directory functionality  
- Domain Controllers centralize authentication  
- Service validation is critical after configuration  

---

## 5. Client Setup and Domain Join

### Configuration

- Created Windows 11 client VM (CL01)  
- Configured DNS to point to the Domain Controller  
- Verified connectivity  

---

### Domain Join

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/05-domain-join.png" width="50%" />
</p>

Joined the client machine to the domain.

---

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/06-domain-joined.png" width="50%" />
</p>

Confirmed domain membership after restart.

---

### Organizational Units

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/07-ou-structure.png" width="50%" />
</p>

Created structured OUs for better organization.

---

### Verification

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/08-computer-added.png" width="50%" />
</p>

Client appears in Active Directory.

---

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/09-client-login.png" width="50%" />
</p>

Successfully authenticated using a domain account.

---

### What I Learned

- DNS configuration is critical for domain communication  
- Domain join validates infrastructure setup  
- Authentication confirms correct system integration  

---

## 6. Security Groups and Access Control

### Objective

To implement structured access control using security groups.

---

### Steps Performed

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/10-open-active-directory-users-and-computers.png" width="50%" />
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/11-domain-structure-overview.png" width="50%" />
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/12-create-new-group-menu.png" width="50%" />
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/13-create-it-group.png" width="50%" />
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/14-create-employees-group.png" width="50%" />
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/15-employees-ou-structure.png" width="50%" />
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/16-add-user-to-group.png" width="50%" />
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/17-group-members-tab.png" width="50%" />
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/18-group-members-confirmation.png" width="50%" />
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/19-user-member-of-tab.png" width="50%" />
</p>

---

### What I Learned

- Security groups simplify permission management  
- Organizational Units provide logical structure  
- Membership validation should be done from both perspectives  

---

## 7. Delegation of Control Password Reset

### Objective

To delegate password reset permissions without granting full administrative access.

---

### Configuration

- Created IT_Group and HR_Group  
- Assigned users to appropriate groups  

---

### Delegation Steps

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/20-delegation-start.png" width="50%" />
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/21-select-itgroup.png" width="50%" />
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/22-permission.png" width="50%" />
</p>

---

### Verification

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/23-reset-password.png" width="50%" />
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/24-success.png" width="50%" />
</p>

---

### What I Learned

- Delegation enforces least privilege  
- RBAC improves security and scalability  
- Administrative tasks can be distributed safely  

---

## 8. Notes for Future Expansion

This section will be updated as the lab evolves.

Planned additions:

- Group Policy Objects (GPO)  
- Shared folders and permissions  
- Active Directory auditing  
- Security monitoring scenarios  

---

## Author

Najmus Sakib
