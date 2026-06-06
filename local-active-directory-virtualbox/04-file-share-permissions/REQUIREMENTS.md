# Requirements

## Prerequisites

Before starting this lab, the following labs should already be complete:

- `01-domain-controller-setup`
- `02-client-domain-join`
- `03-group-policy-management`

You should already have:

- A working Domain Controller named `DC01`
- A domain named `lab.local`
- A Windows client named `CLIENT01`
- CLIENT01 joined to the `lab.local` domain
- Domain users such as `jdoe` and `asmith`
- Security groups such as `HR-Team` and `IT-Helpdesk`
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
- File Explorer
- Screenshot tool

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
Share path: \\DC01\HR-Share
```

## Account Requirements

You need:

- Domain Administrator access on DC01
- A domain user who should have access, such as `LAB\jdoe`
- A domain user who should not have access, such as `LAB\asmith`
- An Active Directory security group named `HR-Team`

## Permission Model Used

Recommended permission model:

```text
Folder: C:\Shares\HR-Share

Allowed:
- SYSTEM
- Administrators
- HR-Team

Not allowed:
- asmith
- IT-Helpdesk
- broad Domain Users access
```

## Verification Commands

Run these on DC01:

```powershell
Get-SmbShare
Get-SmbShareAccess -Name "HR-Share"
icacls "C:\Shares\HR-Share"
```

Run this from CLIENT01 File Explorer:

```text
\\DC01\HR-Share
```
