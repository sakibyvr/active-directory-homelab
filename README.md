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

The goal of this lab is to simulate real-world IT infrastructure and gain hands-on experience in:

- Deploying Active Directory Domain Services (AD DS)
- Configuring DNS for domain environments
- Managing users, groups, and organizational units
- Implementing access control using security groups
- Delegating administrative responsibilities
- Troubleshooting system and configuration issues

This lab is designed as both a learning project and a reference for future interview preparation.

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

![License Error](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/01-license-error.png)

During installation, Windows Server setup failed with a license-related error, even though the ISO file was valid.

---

### Investigation

The following checks were performed:

- Verified virtualization support in BIOS
- Adjusted CPU and RAM allocation for the VM
- Reviewed system security settings

These steps did not resolve the issue.

---

### Root Cause

The issue was caused by VirtualBox's unattended installation feature, which interfered with the normal setup process.

---

### Resolution

- Recreated the virtual machine
- Disabled unattended installation
- Reinstalled Windows Server

---

### Result

![Server Installed](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/02-server-installed.png)

The installation completed successfully and the server booted into Server Manager.

---

### What I Learned

- Installation failures are not always caused by corrupted media
- Hypervisor settings can directly impact OS behavior
- A structured troubleshooting approach helps isolate issues effectively

---

## 4. Domain Controller Setup DC01

### Configuration

The server was configured as a Domain Controller using the following steps:

- Installed Active Directory Domain Services (AD DS)
- Installed DNS Server role
- Promoted the server to a Domain Controller
- Created a new forest: homelab.ca
- Configured Directory Services Restore Mode (DSRM) password

---

### Verification

![Domain Login](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/03-login-domain.png)

Logged in using the domain administrator account to confirm successful promotion.

---

![DC Ready](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/04-dc-ready.png)

Verified that AD DS and DNS services are running correctly.

---

### What I Learned

- DNS is essential for Active Directory functionality
- Domain Controllers centralize authentication and management
- Service validation is critical after configuration

---

## 5. Client Setup and Domain Join

### Configuration

- Created Windows 11 client VM (CL01)
- Configured DNS to point to the Domain Controller
- Verified network connectivity

---

### Domain Join

![Domain Join](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/05-domain-join.png)

Joined the client machine to the domain homelab.ca.

---

![Domain Joined](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/06-domain-joined.png)

Confirmed domain membership after system restart.

---

### Organizational Structure

![OU Structure](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/07-ou-structure.png)

Created Organizational Units:

- Employees
- IT
- Computers

---

### Verification

![Computer Added](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/08-computer-added.png)

Client machine appears in Active Directory.

---

![Client Login](https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/09-client-login.png)

Successfully authenticated using a domain user account.

---

### What I Learned

- DNS configuration is critical for domain communication
- Domain join validates infrastructure setup
- Authentication confirms proper integration between systems

---

## 6. Security Groups and Access Control

### Objective

To implement structured access control using security groups.

---

### Steps Performed

#### Open Active Directory Users and Computers
<img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/10-open-active-directory-users-and-computers.png" width="700"/>

#### Review Domain Structure
<img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/11-domain-structure-overview.png" width="700"/>

#### Create Security Groups
<img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/12-create-new-group-menu.png" width="700"/>
<img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/13-create-it-group.png" width="700"/>
<img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/14-create-employees-group.png" width="700"/>

#### Verify Organizational Units
<img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/15-employees-ou-structure.png" width="700"/>

#### Add User to Group
<img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/16-add-user-to-group.png" width="700"/>

#### Verify Membership
<img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/17-group-members-tab.png" width="700"/>
<img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/18-group-members-confirmation.png" width="700"/>
<img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/19-user-member-of-tab.png" width="700"/>

---

### What I Learned

- Security groups simplify permission management
- Organizational Units help structure environments logically
- Membership should be verified from both group and user perspectives

---

## 7. Delegation of Control Password Reset

### Objective

To allow a non-administrative user to reset passwords without granting full administrative privileges.

---

### Configuration

- Created IT_Group and HR_Group
- Assigned users to respective groups

---

### Delegation Steps

<img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/20-delegation-start.png" width="700"/>
<img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/21-select-itgroup.png" width="700"/>
<img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/22-permission.png" width="700"/>

---

### Verification

<img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/23-reset-password.png" width="700"/>
<img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/24-success.png" width="700"/>

---

### What I Learned

- Delegation supports the principle of least privilege
- Role-Based Access Control improves security
- Administrative tasks can be distributed without exposing critical permissions

---

## 8. Notes for Future Expansion

This section is intentionally left open for future updates.

Planned additions:

- Group Policy Objects (GPO)
- Shared folders and permissions
- Active Directory auditing and logging
- Security monitoring scenarios

---
### Verification

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/23-reset-password.png" width="50%" />
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/24-success.png" width="50%" />
</p>

---

## Author

Najmus Sakib
