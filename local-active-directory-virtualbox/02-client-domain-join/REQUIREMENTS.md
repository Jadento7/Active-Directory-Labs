# Requirements

## Prerequisites

This lab assumes Part 1 of the Active Directory home lab is already complete.

Before starting this lab, you should already have:

- A working Windows Server 2022 Domain Controller named `DC01`
- A working domain named `lab.local`
- Active Directory Domain Services installed
- DNS running on DC01
- At least one domain user account created, such as `jdoe` or `asmith`
- DC01 configured with a static IP address
- DC01 powered on during the client domain join process

## Hardware Requirements

Recommended minimum host computer specs:

- 8 GB RAM minimum
- 16 GB RAM preferred if running DC01 and CLIENT01 at the same time
- 50 GB free disk space for CLIENT01
- Additional disk space for DC01
- 64-bit processor
- Virtualization enabled in BIOS/UEFI
- Internet connection for downloads and updates

## Software Requirements

- Oracle VirtualBox
- Windows 11 ISO
- Windows Server 2022 VM from Part 1
- PowerShell
- Windows Command Prompt
- Screenshot tool

## Windows Edition Requirement

CLIENT01 must use a Windows edition that supports domain joining.

Valid editions include:

- Windows 10 Pro
- Windows 10 Enterprise
- Windows 10 Education
- Windows 11 Pro
- Windows 11 Enterprise
- Windows 11 Education

Do not use Windows Home. Windows Home cannot join an Active Directory domain.

## Network Requirements

Both VMs should use Bridged Adapter mode:

```text
DC01 Network Mode: Bridged Adapter
CLIENT01 Network Mode: Bridged Adapter
```

Both systems should be on the same local network.

Example network values used in this lab:

```text
Router/Gateway: 192.168.86.1
DC01 Static IP: 192.168.86.10
CLIENT01 IP: 192.168.86.24
CLIENT01 DNS Server: 192.168.86.10
Domain: lab.local
```

## DNS Requirement

CLIENT01 must use DC01 as its DNS server.

Correct:

```text
Preferred DNS server: 192.168.86.10
```

Incorrect:

```text
Preferred DNS server: 192.168.86.1
Preferred DNS server: 8.8.8.8
Preferred DNS server: 1.1.1.1
```

The router and public DNS servers do not know where `lab.local` is. The Domain Controller does.

## Local Account Requirement

During Windows setup, create a temporary local account such as:

```text
localadmin
```

Do not use a personal Microsoft account for the lab setup unless absolutely necessary.

The local account is only used to finish setup and configure the machine before joining the domain.

## Domain Login Format

After the domain join, log in using:

```text
LAB\jdoe
```

or:

```text
LAB\asmith
```

The `LAB\` prefix tells Windows to authenticate against the Active Directory domain instead of the local machine.
