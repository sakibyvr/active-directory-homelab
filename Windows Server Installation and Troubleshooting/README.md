Windows Server Installation & Troubleshooting

## 📖 Overview

As part of building my Active Directory homelab, I started by installing **Windows Server 2022** on **Oracle VM VirtualBox**.

During the installation process, I encountered an unexpected issue that required troubleshooting before I could proceed.

---

## ❌ Issue Encountered

![License Error](../screenshots/01-license-error.png)

**Figure 1:** Windows setup error — "Microsoft Software License Terms not found"

While installing Windows Server, the setup abruptly stopped with an error indicating that the license terms could not be found. This was unexpected because the ISO file was valid.

---

## 🔍 Troubleshooting Process

To identify the root cause, I systematically checked multiple possible issues:

- Verified BIOS virtualization settings  
- Adjusted VM resource allocation (RAM and CPU)  
- Reviewed Windows security features (e.g., Core Isolation)  

Despite these checks, the issue continued.

---

## 🧠 Root Cause

After deeper investigation, I discovered that **VirtualBox Unattended Installation** was enabled.

This feature attempts to automate parts of the setup process — including skipping the license agreement — which caused the installation to fail.

---

## ✅ Resolution

To resolve the issue:

- Recreated the virtual machine  
- Disabled **Unattended Installation**  
- Restarted the installation process  

---

## ✔️ Result

![Server Installed](../screenshots/02-server-installed.png)

**Figure 2:** Windows Server 2022 successfully installed with Server Manager dashboard visible

The installation completed successfully after disabling unattended installation, confirming that the issue was configuration-related rather than a system or ISO problem.

---

## 🧠 Key Takeaways

- Installation issues are not always caused by corrupted files  
- Automation features can introduce unexpected errors  
- A structured troubleshooting approach is essential in IT environments  

---

## 💡 Reflection

This experience highlights the value of hands-on labs. Beyond understanding system setup, it builds real-world problem-solving skills — which are critical for IT support and system administration roles.
