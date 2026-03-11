# Domain Controller Setup

## Overview

This document describes the setup and configuration of the domain controller used in the IT Help Desk Ticketing System Lab.

The domain controller provides the following core services:

- Active Directory Domain Services (AD DS)
- Domain authentication
- DNS name resolution
- Centralized directory management
- Group Policy management

The server is deployed as a virtual machine using VMware Workstation.

---

## Server Specifications

| Property | Value |
|--------|--------|
| Hostname | LAB-DC01 |
| Operating System | Windows Server 2019 |
| Role | Domain Controller |
| Domain | lab.local |
| IP Address | 192.168.10.10 |
| DNS Server | Self-hosted (LAB-DC01) |

---

## Windows Server Installation

1. A new virtual machine was created in VMware Workstation.
2. The Windows Server 2019 ISO was mounted to the VM.
3. Windows Server 2019 was installed using default settings.
4. After installation, the server hostname was changed to:

```
LAB-DC01
```

5. The server was restarted to apply the hostname change.

---

## Static IP Configuration

A static IP address was configured to ensure the domain controller maintains a consistent network identity.

Configuration:

| Setting | Value |
|-------|-------|
| IP Address | 192.168.10.10 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 192.168.10.1 |
| Preferred DNS Server | 192.168.10.10 |

The DNS server is set to the domain controller itself because it hosts the domain DNS service.

Verification command:

```
ipconfig /all
```

---

## Installing Active Directory Domain Services

Active Directory Domain Services was installed using Server Manager.

Steps:

1. Open **Server Manager**
2. Select **Add Roles and Features**
3. Choose **Role-based or feature-based installation**
4. Select the local server
5. Enable the role:

```
Active Directory Domain Services
```

6. Accept the required features
7. Complete the installation

Once installation completed, the server was promoted to a domain controller.

---

## Promoting the Server to a Domain Controller

The server was promoted to a domain controller for a new forest.

Steps:

1. Open **Server Manager**
2. Click the notification flag
3. Select:

```
Promote this server to a domain controller
```

4. Choose:

```
Add a new forest
```

5. Domain name configured:

```
lab.local
```

6. Configure Directory Services Restore Mode (DSRM) password
7. Accept default DNS configuration
8. Complete the promotion process

The server automatically restarted after promotion.

---

## DNS Configuration

During domain controller promotion, the DNS Server role was installed automatically.

DNS provides name resolution for the domain environment.

Example DNS entries include:

| Record | Purpose |
|------|------|
| lab.local | Domain zone |
| LAB-DC01 | Domain controller hostname |

DNS verification command:

```
nslookup lab.local
```

Successful resolution confirms DNS is functioning correctly.

---

## Active Directory Verification

After installation, Active Directory management tools were verified.

Administrative tools available:

- Active Directory Users and Computers
- Active Directory Administrative Center
- DNS Manager
- Group Policy Management

Verification steps:

1. Open **Active Directory Users and Computers**
2. Confirm domain:

```
lab.local
```

3. Verify default containers:

- Users
- Computers
- Domain Controllers

---

## Domain Controller Role

The domain controller performs the following functions within the lab:

- authenticates domain users
- stores directory information
- manages domain computers
- hosts DNS for domain name resolution
- distributes Group Policy settings

Client machines must communicate with the domain controller to authenticate users and access domain resources.

---

## Verification

The following checks were performed to verify the domain controller is functioning correctly:

| Test | Expected Result |
|----|----|
| Ping domain controller | Successful response |
| DNS lookup | Domain resolves correctly |
| AD tools open successfully | Domain objects visible |

Example verification commands:

```
ping LAB-DC01
nslookup lab.local
```

---

## Screenshots

Example screenshots captured during setup include:

- Server Manager roles installation
- Domain controller promotion wizard
- Active Directory Users and Computers console
- DNS Manager showing domain zone

Screenshots are located in:

```
screenshots/
```

---

## Summary

The domain controller is the core component of the lab environment. It provides authentication, directory services, and DNS resolution for the domain `lab.local`.

This infrastructure enables simulation of common IT support scenarios including user management, workstation domain joining, access control, and troubleshooting of domain-related issues.
