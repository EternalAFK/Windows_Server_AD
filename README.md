# Windows Server & Active Directory Administration Lab

## Overview

This hands-on lab was built to develop practical experience with **Windows Server Active Directory Domain Services (AD DS)** and common administration tasks performed by IT Support, Service Desk, and System Analyst teams.

The environment uses the `thm.local` domain and demonstrates centralized identity administration, Organizational Unit design, delegated administration, security-group management, Group Policy, and group-based access to departmental file shares.

> **Status:** Core Active Directory, Group Policy, and file-permission tasks completed. Additional evidence can be added as the lab is expanded.

---

## Technologies & Tools

- Windows Server
- Active Directory Domain Services (AD DS)
- Active Directory Users and Computers (ADUC)
- Group Policy Management Console (GPMC)
- Group Policy Management Editor
- Windows PowerShell / Active Directory module
- Organizational Units (OUs)
- Active Directory security groups
- Delegation of Control
- Group Policy Objects (GPOs)
- Windows file sharing and NTFS permissions

---

## Lab Objectives

- Administer an Active Directory domain
- Design a departmental OU structure
- Work with accidental-deletion protection on OUs
- Delegate limited help-desk permissions using least privilege
- Create and validate security groups and group membership
- Create and link Group Policy Objects
- Configure workstation security settings with Group Policy
- Create departmental folders and apply group-based access
- Validate Active Directory configuration through both GUI tools and PowerShell

---

## 1. Active Directory Domain & OU Structure

I managed the `thm.local` domain through **Active Directory Users and Computers** and organized objects beneath a parent OU named `THM`.

Departmental OUs included:

- IT
- Management
- Marketing
- Research and Development
- Sales

This structure demonstrates how Active Directory can organize users, groups, computers, permissions, and policies around business functions.

### Evidence

![Active Directory domain overview](screenshots/01-aduc-domain-overview.png)

![Department OU structure](screenshots/03-department-ou-structure.png)

![OU and group structure](screenshots/26-ad-ou-and-groups-structure.png)

---

## 2. OU Protection & Object Administration

I reviewed the **Protect object from accidental deletion** setting on an Organizational Unit and tested the workflow required to remove that protection before performing a deletion action.

This demonstrates an important administrative safeguard because deleting an OU can affect the users, groups, computers, and policy structure beneath it.

### Evidence

![OU accidental deletion protection](screenshots/05-ou-accidental-deletion-protection.png)

![OU deletion protection disabled](screenshots/06-ou-deletion-protection-disabled.png)

![OU deletion confirmation](screenshots/07-ou-delete-confirmation.png)

---

## 3. Delegation of Control

I used the **Delegation of Control Wizard** on the Sales OU to assign a limited administrative responsibility to another user.

The delegated task selected was:

- **Reset user passwords and force password change at next logon**

This demonstrates **least-privilege administration** by providing a specific help-desk capability without granting full domain-administrator rights.

### Evidence

![Delegate Control on Sales OU](screenshots/08-sales-ou-delegate-control.png)

![Delegated user resolved](screenshots/10-delegation-user-resolved.png)

![Password reset delegation](screenshots/11-delegation-password-reset-rights.png)

---

## 4. Security Groups & Membership Validation

I created department-based security groups, including:

- `GG_IT`
- `GG_Marketing`
- `GG_Sales`

For the Sales department, I validated group membership using both **Active Directory Users and Computers** and **PowerShell**.

This demonstrates a practical group-based administration model where permissions can be assigned to a security group instead of directly to individual users.

### Evidence

![Active Directory security groups](screenshots/19-ad-security-groups.png)

![Sales group members in ADUC](screenshots/25-sales-group-members-gui.png)

![Sales group membership using PowerShell](screenshots/23-sales-group-membership-powershell.png)

### PowerShell Validation

```powershell
Get-ADGroupMember GG_Sales
```

This command was used to confirm membership of the Sales security group from the command line.

---

## 5. Departmental File Shares & Group-Based Access

I created departmental folders under `C:\CompanyShares`, including:

- IT
- Marketing
- Sales

The `GG_Sales` security group was then used to control access to the Sales folder.

At the share level, `GG_Sales` was assigned **Read/Write** access. At the NTFS level, the group was granted permissions including:

- Modify
- Read & execute
- List folder contents
- Read
- Write

This demonstrates the use of **group-based access control** for shared resources rather than assigning permissions individually to users.

### Evidence

![Department folders](screenshots/24-department-share-folders.png)

![Sales share permission](screenshots/21-sales-share-group-permission.png)

![Sales NTFS permissions](screenshots/22-sales-ntfs-permissions.png)

---

## 6. Group Policy Management

I used **Group Policy Management** to create and review Group Policy Objects for centralized Windows administration.

The lab included GPOs such as:

- `Restrict Control Panel Access`
- `Auto Lock Screen`
- `RDP policy`

The GPMC view also demonstrates policy objects and links applied within the domain structure.

### Evidence

![Create Restrict Control Panel Access GPO](screenshots/12-gpo-create-restrict-control-panel.png)

![GPO links and policy objects](screenshots/18-gpo-links-and-objects.png)

> Note: one screenshot shows the Control Panel policy location while it was still **Not configured**. It is included as evidence of policy navigation, not as proof of enforcement.

---

## 7. Workstation Security Policy

I configured the Windows security option:

**Interactive logon: Machine inactivity limit**

with a value of:

**300 seconds (5 minutes)**

This type of control automatically locks an inactive workstation and reduces the risk of an unattended authenticated session being used by another person.

### Evidence

![Machine inactivity limit configured](screenshots/16-machine-inactivity-limit-300s.png)

![Machine inactivity limit confirmed](screenshots/17-machine-inactivity-limit-confirmed.png)

---

## 8. Group Policy Administration & Navigation

I practised navigating both user and computer policy settings inside the Group Policy Management Editor, including:

- Administrative Templates
- Control Panel settings
- Windows Settings
- Security Settings
- Local Policies
- Security Options
- Audit Policy
- User Rights Assignment

This helped build familiarity with locating policy settings and understanding the difference between **Computer Configuration** and **User Configuration**.

### Evidence

![Group Policy editor overview](screenshots/13-group-policy-editor-overview.png)

![Control Panel policy location](screenshots/14-control-panel-policy-location.png)

![Security Options navigation](screenshots/15-security-options-navigation.png)

---

## Skills Demonstrated

- Active Directory domain administration
- Organizational Unit design and administration
- Security-group creation and membership management
- GUI and PowerShell validation
- Delegation of Control
- Least-privilege administration
- Group Policy creation and linking
- Windows security-policy configuration
- Windows file sharing
- NTFS permissions
- Group-based access control
- Centralized workstation administration
- Administrative troubleshooting and validation

---

## Practical IT Support Relevance

The tasks in this lab map directly to common entry-level infrastructure and support responsibilities, including:

- Resetting user passwords
- Managing users and groups
- Organizing directory objects
- Delegating help-desk permissions
- Applying department-specific policies
- Configuring workstation-security settings
- Creating shared departmental resources
- Assigning and validating group-based file permissions
- Checking group membership with PowerShell
- Troubleshooting Active Directory and Group Policy scope

---

## Key Takeaway

This lab strengthened my understanding of how **Active Directory centralizes identity and access management**, how **Group Policy centralizes Windows configuration**, and how **security groups can be used to control access to shared resources**.

It also provides a useful comparison point for my cloud-based **Microsoft Entra ID and Microsoft Intune** labs.

---

