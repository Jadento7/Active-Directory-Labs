# Requirements

## Prerequisites

Before starting this lab, the following labs should already be complete:

- `01-domain-controller-setup`
- `02-client-domain-join`
- `03-group-policy-management`
- `04-file-share-permissions`

You should already have:

- A working Domain Controller named `DC01`
- A domain named `lab.local`
- A Windows client named `CLIENT01`
- CLIENT01 joined to the `lab.local` domain
- Domain users such as `jdoe` and `asmith`
- A `Users Accounts` OU containing the user accounts
- A `Groups` OU containing security groups
- Working DNS between CLIENT01 and DC01

## Hardware Requirements

Recommended host system:

- 8 GB RAM minimum
- 16 GB RAM preferred
- Enough CPU/RAM to run DC01 and CLIENT01 at the same time
- 50 GB or more free disk space
- Virtualization enabled in BIOS/UEFI

## Software Requirements

- Oracle VirtualBox
- Windows Server 2022 VM for DC01
- Windows 10/11 Pro VM for CLIENT01
- Active Directory Domain Services
- Active Directory Users and Computers
- PowerShell
- Screenshot tool

## Optional Software Requirement

If testing delegated password resets from CLIENT01, RSAT tools may be needed.

Install:

```text
RSAT: Active Directory Domain Services and Lightweight Directory Tools
```

On Windows 10/11, this can usually be installed from:

```text
Settings → Apps → Optional Features → View features
```

Search for:

```text
RSAT
```

## Network Requirements

Both VMs should be on the same local network.

Recommended VirtualBox network mode:

```text
Bridged Adapter
```

CLIENT01 should use DC01 as its DNS server.

Example:

```text
DC01 IP: 192.168.86.10
CLIENT01 DNS Server: 192.168.86.10
Domain: lab.local
```

## Account Requirements

You need:

- Domain Administrator access to configure delegation
- A delegated user such as `LAB\asmith`
- A target user such as `LAB\jdoe`
- A security group named `Helpdesk-Admins`

## Delegation Model Used

```text
Helpdesk-Admins
└── asmith

Users Accounts OU
└── Delegated permission:
    Reset user passwords and force password change at next logon
```

## Verification Commands

Run these on DC01:

```powershell
Get-ADGroupMember "Helpdesk-Admins"
Get-ADUser asmith -Properties MemberOf | Select-Object -ExpandProperty MemberOf
Get-ADGroupMember "Domain Admins"
```

Run this after logging in as `jdoe`:

```powershell
whoami
```

Expected output:

```text
lab\jdoe
```
