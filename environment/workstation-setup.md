# Workstation Setup

## Overview

This document describes the setup and configuration of Windows client machines used in the IT Help Desk Ticketing System Lab.

The workstations simulate employee computers in a corporate environment. Each workstation is joined to the Active Directory domain and authenticates using domain user accounts.

The workstations allow simulation of common IT support tasks such as:

- domain login troubleshooting
- workstation management
- shared resource access
- user account authentication
- network diagnostics

---

## Workstation Environment

Two Windows 10 virtual machines were created to simulate employee workstations.

| Computer Name | Role | Status |
|---------------|------|--------|
| LAB-WIN10-01 | Employee workstation | Configured and verified |
| LAB-WIN10-02 | Employee workstation | Configuration pending |

Both machines are connected to the same virtual network as the domain controller.

---

## Network Configuration

Workstations are configured with a static IP address and use the domain controller as their DNS server and default gateway.

### LAB-WIN10-01 (Verified)

| Setting | Value |
|--------|------|
| IP Address | 192.168.56.20 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 192.168.56.10 |
| DNS Server | 192.168.56.10 |
| Network Adapter | Ethernet0 |

The default gateway is set to the domain controller (`192.168.56.10`), which handles routing within the lab network.

### LAB-WIN10-02 (Pending)

Configuration for LAB-WIN10-02 will follow the same settings as LAB-WIN10-01 once verified.

Verification command:

```
ipconfig /all
```

---

## Joining the Domain

Each workstation was joined to the domain `LAB.local`.

Steps:

1. Open **System Properties**
2. Select **Change settings** under computer name
3. Click **Change**
4. Select:

```
Domain
```

5. Enter the domain name:

```
LAB.local
```

6. Enter domain administrator credentials when prompted
7. Restart the workstation

After restart, the machine becomes part of the domain environment.

---

## Domain Login

Once joined to the domain, users can authenticate using domain credentials.

Example domain users:

| User | Workstation |
|------|-------------|
| j.smith | LAB-WIN10-01 |
| a.johnson | LAB-WIN10-02 |

Login format:

```
LAB\username
```

or

```
username@LAB.local
```

---

## Moving Computers to the Workstations OU

When a computer joins the domain, it initially appears in the default **Computers** container.

For organizational purposes, workstations are moved into the **Workstations OU**.

Steps:

1. Open **Active Directory Users and Computers**
2. Navigate to:

```
Computers
```

3. Locate the workstation object:

```
LAB-WIN10-01
```

4. Right-click the computer
5. Select:

```
Move
```

6. Choose the destination OU:

```
Workstations
```

Repeat for all domain workstations once each machine has been configured and verified.

This allows Group Policy and administrative management to be applied to workstation objects.

---

## Verification

The following checks were used to confirm proper domain configuration on LAB-WIN10-01.

### Verify Domain Membership

Open **System Information** and confirm:

```
Domain: LAB.local
```

---

### Test Domain Controller Connectivity

Run:

```
ping LAB-DC01
```

Expected result: successful response.

---

### Verify DNS Resolution

Run:

```
nslookup LAB.local
```

Expected result: domain resolves to the domain controller.

---

### Verify Group Policy

Run:

```
gpresult /r
```

This confirms that domain policies are being applied to the workstation.

---

## Screenshots

Example screenshots captured during workstation setup include:

- IPv4 properties showing static IP configuration
- ipconfig /all output confirming network settings
- Active Directory Users and Computers showing domain membership
- Workstation objects inside the Workstations OU

Screenshots are stored in the repository directory:

```
screenshots/
```

---

## Summary

The workstation setup provides a realistic client environment within the lab domain.

By joining workstations to the domain and authenticating with Active Directory accounts, the environment supports simulation of common service desk scenarios such as:

- domain login issues
- network connectivity problems
- group policy troubleshooting
- shared resource access

LAB-WIN10-01 has been fully configured and verified. LAB-WIN10-02 will be configured using the same methodology once LAB-WIN10-01 is confirmed stable.
