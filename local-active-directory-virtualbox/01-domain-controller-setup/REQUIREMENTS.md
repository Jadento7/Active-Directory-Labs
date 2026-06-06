# Requirements

## Hardware Requirements

Any Windows, macOS, or Linux computer capable of running VirtualBox and Windows Server 2022.

Recommended minimum:

- 8 GB RAM total
  - 4 GB for the Windows Server VM
  - 4 GB or more for the host operating system
- 50 GB free disk space
- 2 CPU cores assigned to the VM
- 64-bit processor with virtualization support
- Internet connection for downloading software and resolving DNS

## BIOS/UEFI Requirement

Virtualization must be enabled in BIOS/UEFI.

Depending on the system, this may appear as:

- Intel VT-x
- Intel Virtualization Technology
- AMD-V
- SVM Mode

If VirtualBox fails to start the VM or does not allow 64-bit guests, virtualization is probably disabled.

## Software Requirements

- Oracle VirtualBox
- Windows Server 2022 Evaluation ISO
- Web browser
- PowerShell
- Windows Command Prompt
- Screenshot tool

## Network Requirements

The VM should use:

```text
Attached to: Bridged Adapter
```

Bridged mode allows the Domain Controller to receive an IP address on the same network as the host computer. This makes the lab more realistic and prepares the environment for adding a domain-joined client later.

## Example Network Values

These values are examples only. Use values that match your own network.

```text
Gateway/Router: 192.168.86.1
Domain Controller Static IP: 192.168.86.10
Subnet Mask: 255.255.255.0
Preferred DNS Server: 192.168.86.10
Domain Name: lab.local
```

## Important Notes

- Do not use real passwords from personal accounts.
- Do not expose this lab directly to the internet.
- Do not use production networks unless you have permission.
- The Domain Controller should use itself as the preferred DNS server.
- The DNS forwarder can point to the router or another trusted external resolver.
