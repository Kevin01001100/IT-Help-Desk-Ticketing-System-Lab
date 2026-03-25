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

| Computer Name | Role |
|---------------|------|
| LAB-WIN10-01 | Employee workstation |
| LAB-WIN10-02 | Employee workstation |

Both machines are connected to the same Host-Only virtual network (VMnet1) as the domain controller.

---

## Network Configuration

Workstations are configured with static IP addresses and use the domain controller as their DNS server.

| Machine | IP Address | Subnet Mask | DNS Server |
|--------|------------|-------------|------------|
| LAB-WIN10-01 | 192.168.56.20 | 255.255.255.0 | 192.168.56.10 |
| LAB-WIN10-02 | 192.168.56.21 | 255.255.255.0 | 192.168.56.10 |

All machines are on the same `192.168.56.0/24` subnet within the Host-Only network. No default gateway is required for intra-lab communication.

This allows the workstation to locate and communicate with the domain controller.

Verification command:

```
ipconfig /all
```

---

## Joining the Domain

Each workstation was joined to the domain `lab.local`.

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
lab.local
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
username@lab.local
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

3. Locate the workstation object (e.g. `LAB-WIN10-01`)
4. Right-click the computer
5. Select:

```
Move
```

6. Choose the destination OU:

```
Workstations
```

Repeat for all domain workstations.

This allows Group Policy and administrative management to be applied to workstation objects.

---

## Verification

The following checks were used to confirm proper domain configuration.

### Verify Domain Membership

Open **System Information** and confirm:

```
Domain: lab.local
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
nslookup lab.local
```

Expected result: domain resolves to the domain controller at `192.168.56.10`.

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

- Windows system properties showing domain membership
- domain join confirmation
- workstation objects inside the Workstations OU
- command prompt output for network verification

Screenshots are stored in the repository directory:

```
screenshots/workstations/
```

---

## Summary

The workstation setup provides a realistic client environment within the lab domain.

By joining workstations to the domain and authenticating with Active Directory accounts, the environment supports simulation of common service desk scenarios such as:

- domain login issues
- network connectivity problems
- group policy troubleshooting
- shared resource access
