# Active Directory Labs

## Overview

This repository documents a series of hands-on Active Directory labs built in a local VirtualBox environment. The labs start with a basic Windows Server Domain Controller and progressively build toward real-world identity and access management tasks, including domain joining, Group Policy, file share permissions, and delegated administration.

The purpose of this project is to practice Windows Server administration, Active Directory Domain Services, DNS, Group Policy, user and group management, access control, and least privilege administration in a safe local lab environment.

## Lab Environment

| Component | Details |
|---|---|
| Hypervisor | Oracle VirtualBox |
| Domain Controller | DC01 |
| Client Machine | CLIENT01 |
| Domain | lab.local |
| Server OS | Windows Server 2022 |
| Client OS | Windows 11 Pro |
| Network Mode | Bridged Adapter |
| Primary Tools | Active Directory Users and Computers, Group Policy Management, PowerShell, File Explorer |

## Lab Structure

```text
Active-Directory-Labs/
├── local-active-directory-virtualbox/
│   ├── 01-domain-controller-setup/
│   ├── 02-client-domain-join/
│   ├── 03-group-policy-management/
│   ├── 04-file-share-permissions/
│   └── 05-delegated-administration/
│
├── azure-active-directory/
│   └── README.md
│
└── README.md
```

## Labs Included

| Lab | Title | Description |
|---:|---|---|
| 01 | Domain Controller Setup | Builds the foundation of the lab by creating a Windows Server VM, assigning a static IP address, installing AD DS, promoting the server to a Domain Controller, configuring DNS, creating OUs, users, groups, and a password policy. |
| 02 | Client Domain Join | Creates a Windows client VM named CLIENT01, configures DNS to point to DC01, joins the client to the lab.local domain, and verifies domain login using Active Directory users. |
| 03 | Group Policy Management | Creates and applies a Group Policy Object to block Control Panel access, forces policy updates on CLIENT01, verifies the applied GPO with gpresult, and confirms the restriction works. |
| 04 | File Share Permissions | Creates an HR file share, assigns access through the HR-Team security group, confirms jdoe can access the share, and confirms asmith is denied access. |
| 05 | Delegated Administration | Creates a Helpdesk-Admins group, delegates password reset permissions over a user OU, confirms asmith is not a Domain Admin, and verifies asmith can reset jdoe’s password through delegated permissions. |

## Skills Demonstrated

This repository demonstrates practical experience with:

- Windows Server administration
- Active Directory Domain Services
- Domain Controller deployment
- DNS configuration for Active Directory
- Static IP configuration
- Domain joining Windows clients
- Organizational Unit design
- User and security group management
- Group Policy Object creation and enforcement
- Group Policy troubleshooting with `gpupdate` and `gpresult`
- SMB file sharing
- NTFS permissions
- Group-based access control
- Least privilege administration
- Delegation of Control
- PowerShell-based verification
- Screenshot-based technical documentation

## Key Concepts Practiced

### Active Directory Foundation

The first lab establishes the core domain infrastructure by building `DC01`, configuring networking, installing Active Directory Domain Services, and creating the `lab.local` domain.

### Domain-Joined Client Management

The second lab adds `CLIENT01` to the domain and proves that domain users can authenticate on a Windows client machine.

### Group Policy Enforcement

The third lab demonstrates centralized policy management by applying a Group Policy Object and verifying that it affects the domain user on the client machine.

### Group-Based File Access

The fourth lab demonstrates the access control model used in many organizations:

```text
Users → Groups → Permissions → Access
```

Permissions are assigned to groups instead of directly to individual users.

### Delegated Administration

The fifth lab demonstrates least privilege by giving a help desk user the ability to reset passwords without making that user a Domain Admin.

## Screenshots

Each lab contains its own `screenshots/` folder with proof of completion. Screenshots are used to document important milestones such as:

- Server and client configuration
- Domain join success
- GPO application
- Access allowed and access denied tests
- Delegated password reset success
- PowerShell verification output

## Requirements

General requirements for the local labs:

- Oracle VirtualBox
- Windows Server 2022 ISO
- Windows 10/11 Pro ISO
- At least 8 GB RAM
- 16 GB RAM recommended
- 50 GB+ free disk space
- Virtualization enabled in BIOS/UEFI
- Basic familiarity with Windows networking
- Local admin access on the host machine

Each individual lab folder includes its own `REQUIREMENTS.md` with more specific requirements.

## How to Use This Repository

Each lab is documented in its own folder. Start with Lab 01 and complete the labs in order:

```text
01-domain-controller-setup
02-client-domain-join
03-group-policy-management
04-file-share-permissions
05-delegated-administration
```

The labs build on each other, so skipping earlier labs may cause later labs to fail.

For example, the client domain join lab requires the Domain Controller from Lab 01, and the Group Policy, file share, and delegated administration labs require both the Domain Controller and domain-joined client to already exist.

## What I Learned

Through these labs, I learned how to build and manage a basic Active Directory environment from scratch. I practiced creating a Domain Controller, joining a client to the domain, managing users and groups, enforcing settings with Group Policy, controlling file share access with security groups, and delegating limited administrative permissions.

The biggest takeaway from this project is that Active Directory depends heavily on correct DNS, clean OU structure, group-based access control, and least privilege. Small misconfigurations, especially with DNS or permissions, can break authentication, policy application, or access control.

## Future Improvements

Planned future improvements include:

- Add an Azure-based Active Directory lab track
- Build a cloud-hosted Domain Controller in Azure
- Join an Azure Windows client VM to the domain
- Add hybrid identity concepts with Microsoft Entra ID
- Create a mapped drive GPO lab
- Create an account lockout policy lab
- Create a login banner GPO lab
- Add audit policy and Event Viewer monitoring
- Add PowerShell automation for user and group creation

## Security and Ethics Notice

These labs were created for educational use in a private local environment. They should not be exposed directly to the public internet.

Do not test administrative actions, permissions, scanning, or security configurations on systems you do not own or do not have explicit permission to manage. Do not use real personal data, production passwords, real credentials, or sensitive files in lab environments.
