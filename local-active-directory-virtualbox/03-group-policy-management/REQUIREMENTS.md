# Requirements

## Prerequisites

Before starting this lab, the following labs should already be complete:

- `01-domain-controller-setup`
- `02-client-domain-join`

You should already have:

- A working Domain Controller named `DC01`
- A domain named `lab.local`
- A Windows client named `CLIENT01`
- CLIENT01 joined to the `lab.local` domain
- A domain user account, such as `LAB\jdoe`
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
- Group Policy Management Console
- PowerShell or Command Prompt
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
```

## Account Requirements

You need:

- Domain Administrator access on DC01 to create and edit GPOs
- A domain user account for testing, such as `LAB\jdoe`

## Policy Used in This Lab

This lab uses:

```text
User Configuration
→ Policies
→ Administrative Templates
→ Control Panel
→ Prohibit access to Control Panel and PC settings
```

Policy state:

```text
Enabled
```

## Verification Commands

Run these on CLIENT01 as the domain user:

```powershell
gpupdate /force
gpresult /r
```

Successful verification should show the GPO under:

```text
User Settings
→ Applied Group Policy Objects
```
