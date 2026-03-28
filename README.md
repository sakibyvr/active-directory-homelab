# Active Directory Homelab (Windows Server 2022)

## 0. Table of Contents

- [1. Project Overview](#1-project-overview)
- [2. Lab Architecture](#2-lab-architecture)
- [3. Domain Controller Setup DC01](#3-domain-controller-setup-dc01)
- [4. Client Setup and Domain Join](#4-client-setup-and-domain-join)
- [5. Security Groups and Access Control](#5-security-groups-and-access-control)
- [6. Delegation of Control Password Reset](#6-delegation-of-control-password-reset)
- [7. Key Concepts and Real World Mapping](#7-key-concepts-and-real-world-mapping)
- [8. Notes for Future Expansion](#8-notes-for-future-expansion)

---

## 1. Project Overview

This project documents the step-by-step process of building an Active Directory environment using Windows Server 2022 in a virtualized lab.

The purpose of this lab is to simulate a real enterprise IT environment and develop practical, job-ready skills in:

- Active Directory deployment and configuration  
- Domain-based authentication and identity management  
- User, group, and Organizational Unit (OU) management  
- Access control using security groups  
- Delegation of administrative tasks using least privilege  
- Troubleshooting system-level and configuration issues  

This repository also serves as a structured reference for interview preparation and real-world troubleshooting scenarios.

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
- Domain: homelab.ca  
- Hypervisor: Oracle VirtualBox  
- Tools: Active Directory Domain Services (AD DS), DNS, RSAT  

---

## 3. Domain Controller Setup DC01

### Overview

In this step, the standalone server was converted into a Domain Controller to enable centralized identity and access management.

---

### Configuration Steps

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

Verified that AD DS and DNS services are running correctly.

---

### What This Demonstrates

- Understanding of domain infrastructure  
- Knowledge of AD DS and DNS integration  
- Ability to configure centralized authentication systems  

---

## 4. Client Setup and Domain Join

### Overview

A Windows 11 client machine was configured and joined to the domain to validate authentication and connectivity.

---

### Configuration

- Created client VM (WIN11-CL01)  
- Configured DNS to point to DC01  
- Verified network connectivity  

---

### Domain Join Process

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/05-domain-join.png" width="50%" />
</p>

Joined the client to the domain homelab.ca.

---

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/06-domain-joined.png" width="50%" />
</p>

Confirmed successful domain membership.

---

### Organizational Unit Structure

<p align="center">
  <img src="https://raw.githubusercontent.com/sakibyvr/active-directory-homelab/main/screenshots/07-ou-structure.png" width="50%" />
</p>

Created structured Organizational Units to organize users and computers.

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

Successful domain authentication confirmed.

---

### What This Demonstrates

- Understanding of domain join process  
- Importance of DNS in AD environments  
- Validation of authentication workflow  

---

## 5. Security Groups and Access Control

### Overview

Security groups were created to implement structured and scalable access control.

---

### Why This Matters

In enterprise environments, permissions are assigned to groups rather than individual users to improve scalability and reduce administrative overhead.

---

### Implementation Steps

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

### What This Demonstrates

- Understanding of role-based access control  
- Ability to design scalable permission structures  
- Verification of access from both group and user perspectives  

---

## 6. Delegation of Control Password Reset

### Overview

Delegation of Control was implemented to simulate real-world helpdesk operations.

---

### Objective

Allow IT support users to reset passwords without granting full administrative privileges.

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

### What This Demonstrates

- Implementation of least privilege principle  
- Understanding of delegation in Active Directory  
- Simulation of real IT support workflows  

---

## 7. Key Concepts and Real World Mapping

This lab reflects several real-world IT concepts:

- Domain Controllers → Central authentication servers  
- DNS → Core dependency for AD communication  
- Security Groups → Scalable access control mechanism  
- Delegation → Helpdesk-level privilege management  
- RSAT → Remote administrative tools used in enterprise environments  

---

## 8. Notes for Future Expansion

This section will be updated as the lab evolves.

Planned additions:

- Group Policy Objects (GPO)  
- Shared folder permissions  
- Active Directory auditing and logging  
- Security monitoring scenarios  

---

## Author

Najmus Sakib
