# Azure Active Directory Labs

## Overview

This folder is reserved for future Azure-based Active Directory and hybrid identity labs.

The local VirtualBox labs in this repository build the foundation first: Domain Controller setup, client domain join, Group Policy, file share permissions, and delegated administration. The Azure labs will expand on those skills by rebuilding and extending similar identity concepts in a cloud environment.

## Planned Labs

| Lab | Planned Topic | Description |
|---:|---|---|
| 01 | Azure Domain Controller Setup | Deploy a Windows Server VM in Azure and promote it to a Domain Controller. |
| 02 | Azure Client Domain Join | Deploy a Windows client VM and join it to the Azure-hosted domain. |
| 03 | Azure Networking for AD DS | Configure virtual networks, DNS settings, and connectivity for domain services. |
| 04 | Group Policy in Azure-Hosted AD | Apply and verify Group Policy settings on Azure-hosted domain clients. |
| 05 | Hybrid Identity with Microsoft Entra ID | Explore syncing on-premises-style Active Directory identities with Microsoft Entra ID. |

## Future Skills to Demonstrate

Planned Azure labs will focus on:

- Azure virtual machines
- Azure virtual networks
- Azure DNS configuration for domain services
- Windows Server Domain Controller deployment in Azure
- Domain-joined Azure Windows clients
- Hybrid identity concepts
- Microsoft Entra ID integration
- Cloud-hosted identity infrastructure
- Security and access control in Azure environments

## Status

```text
Status: Planned
```

This section is intentionally separate from the local VirtualBox labs so the repository stays organized:

```text
local-active-directory-virtualbox/  → local AD DS labs
azure-active-directory/             → future Azure and hybrid identity labs
```

## Note

The Azure labs are not complete yet. They will be added after the local Active Directory lab track is finished and documented.
