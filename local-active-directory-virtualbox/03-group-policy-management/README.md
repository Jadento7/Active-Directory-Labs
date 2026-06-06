# Group Policy Management Lab

## Overview

This lab documents how to create and apply a Group Policy Object in a local Active Directory environment. The goal was to apply a user-based Group Policy that blocks access to Control Panel and PC Settings for a domain user.

This lab builds on the previous Active Directory labs:

- `01-domain-controller-setup`
- `02-client-domain-join`

In this lab, the Domain Controller `DC01` manages policy settings for the `lab.local` domain, and the domain-joined client `CLIENT01` is used to verify that the policy applies correctly.

## Lab Objective

The objective of this lab was to prove that Group Policy can be created, linked, applied, and verified in an Active Directory domain.

This lab demonstrates:

- Opening Group Policy Management on the Domain Controller
- Creating a new Group Policy Object
- Linking the GPO to the correct Organizational Unit
- Configuring a user-based Administrative Template policy
- Updating Group Policy on a domain-joined client
- Verifying applied policy with `gpresult /r`
- Testing the policy by attempting to open Control Panel

## Lab Environment

| Component | Value |
|---|---|
| Hypervisor | Oracle VirtualBox |
| Domain Controller | DC01 |
| Domain | lab.local |
| Client Machine | CLIENT01 |
| Test User | LAB\jdoe |
| Policy Type | User Configuration |
| GPO Purpose | Block Control Panel and PC Settings |
| GPO Name | Disable Control Panel - Users |

## Requirements

See [`REQUIREMENTS.md`](REQUIREMENTS.md) for the full requirements.

## Project Structure

```text
03-group-policy-management/
├── README.md
├── REQUIREMENTS.md
├── requirements.txt
└── screenshots/
    ├── 01-users-ou-selected.png
    ├── 02-gpo-created-and-linked.png
    ├── 03-control-panel-policy-enabled.png
    ├── 04-gpupdate-force-success.png
    ├── 05-gpresult-applied-gpo.png
    └── 06-control-panel-blocked.png
```

## Important Note About User-Based GPOs

This lab uses a **User Configuration** policy.

That means the GPO needs to apply to the **user account**, not just the computer account. For this reason, the GPO should be linked to the Organizational Unit containing the test domain user `jdoe`.

If the GPO is linked only to a computer OU, the user policy may not apply unless loopback processing is configured. To keep this beginner lab clean and easy to verify, the policy should be linked to the user OU.

## Step 1: Open Group Policy Management

On `DC01`, open:

```text
Server Manager → Tools → Group Policy Management
```

Then expand:

```text
Forest: lab.local
→ Domains
→ lab.local
```

Select the OU that contains the test user account.

![Users OU selected](screenshots/01-users-ou-selected.png)

## Step 2: Create and Link a New GPO

Right-click the user OU and select:

```text
Create a GPO in this domain, and Link it here
```

Name the GPO:

```text
Disable Control Panel - Users
```

The GPO should appear linked under the selected OU.

![GPO created and linked](screenshots/02-gpo-created-and-linked.png)

## Step 3: Edit the GPO

Right-click the new GPO and select:

```text
Edit
```

Navigate to:

```text
User Configuration
→ Policies
→ Administrative Templates
→ Control Panel
```

Open the policy:

```text
Prohibit access to Control Panel and PC settings
```

Set it to:

```text
Enabled
```

![Control Panel policy enabled](screenshots/03-control-panel-policy-enabled.png)

## Step 4: Force Group Policy Update on CLIENT01

Log in to `CLIENT01` as the domain user:

```text
LAB\jdoe
```

Open PowerShell or Command Prompt and run:

```powershell
gpupdate /force
```

A successful result should show that both Computer Policy and User Policy updated successfully.

![gpupdate force success](screenshots/04-gpupdate-force-success.png)

## Step 5: Verify the GPO Applied

Still on `CLIENT01`, run:

```powershell
gpresult /r
```

Under **User Settings**, check **Applied Group Policy Objects**.

The GPO should appear as:

```text
Disable Control Panel - Users
```

![gpresult applied GPO](screenshots/05-gpresult-applied-gpo.png)

This is the strongest verification step because it proves the domain user received the policy from Active Directory.

## Step 6: Test Control Panel Access

On `CLIENT01`, while logged in as the domain user, try to open Control Panel or PC Settings.

The system should block access because of the applied Group Policy.

![Control Panel blocked](screenshots/06-control-panel-blocked.png)

## What I Learned

Through this lab, I learned how Group Policy is used to centrally manage user settings in an Active Directory domain. I also learned that GPO placement matters. A user-based policy must apply to the user account, and a computer-based policy must apply to the computer account.

This lab also reinforced the importance of verification. Creating a GPO is not enough. The correct way to prove that the policy applied is to use tools like:

```powershell
gpupdate /force
gpresult /r
```

## Troubleshooting Notes

| Problem | Likely Cause | Fix |
|---|---|---|
| GPO does not appear in `gpresult /r` | GPO linked to wrong OU | Link it to the OU containing the user |
| `Applied Group Policy Objects` shows `N/A` | Policy did not apply | Check OU placement and security filtering |
| Control Panel still opens | User policy not applied yet | Run `gpupdate /force`, log out, and log back in |
| DNS/domain communication issues | CLIENT01 not using DC01 for DNS | Set CLIENT01 DNS to DC01 IP |
| Policy shows as empty | Policy setting was not enabled | Reopen GPO and confirm the setting is Enabled |

## Future Improvements

Possible improvements for this lab include:

- Create a dedicated `Lab Users` OU
- Create a dedicated `Workstations` OU
- Move `CLIENT01` into the Workstations OU
- Configure computer-based GPO settings
- Enable loopback processing for workstation-targeted user policies
- Create a password/account lockout policy lab
- Create a mapped network drive GPO
- Create a desktop wallpaper GPO
- Verify policies with `gpresult /h report.html`

## Security and Ethics Notice

This lab was created for educational use in a private local Active Directory environment. Do not test administrative policies on systems you do not own or manage. Avoid using real passwords, real production credentials, or sensitive personal information in lab environments. 
