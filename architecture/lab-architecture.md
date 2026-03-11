# Lab Architecture

## Overview

This lab simulates a small enterprise IT environment used to demonstrate common Service Desk and Help Desk workflows. The environment consists of a Windows Server domain controller and multiple Windows client workstations connected within a virtual network.

The lab supports typical support scenarios including:

- Active Directory user management
- workstation domain joining
- shared folder access management
- password resets and account lockouts
- basic network troubleshooting
- ticket-based incident resolution

The environment is built using virtual machines hosted in VMware Workstation.

---

## Infrastructure Topology

The lab contains three virtual machines connected to the same virtual network.

```
VMware Host
│
├── LAB-DC01
│   Operating System: Windows Server 2019
│   Roles:
│   - Active Directory Domain Services
│   - DNS Server
│
├── LAB-WIN10-01
│   Operating System: Windows 10
│   Role:
│   - Employee workstation
│
└── LAB-WIN10-02
    Operating System: Windows 10
    Role:
    - Employee workstation
```

The domain controller manages authentication, directory services, and DNS resolution for the domain.

---

## Network Configuration

All machines are connected to the same internal virtual network.

Network range:

```
192.168.10.0 /24
```

Example addressing configuration:

| System | Hostname | IP Address | Role |
|------|------|------|------|
| Domain Controller | LAB-DC01 | 192.168.10.10 | AD DS + DNS |
| Workstation | LAB-WIN10-01 | DHCP | Employee workstation |
| Workstation | LAB-WIN10-02 | DHCP | Employee workstation |

All client machines use the domain controller as their DNS server.

---

## Active Directory Domain

The lab domain is configured as:

```
lab.local
```

The domain controller provides the following services:

- user authentication
- directory services
- domain name resolution
- group policy management

Workstations authenticate using credentials stored in Active Directory.

---

## Active Directory Structure

The domain contains a simplified organizational structure used to simulate enterprise access management.

```
lab.local
│
├── Users
│   ├── Employees
│   └── IT
│
├── Computers
│
└── Groups
```

Example domain users:

| Username | Department |
|------|------|
| j.smith | Sales |
| a.johnson | HR |
| m.brown | IT |

Example security groups:

| Group Name | Purpose |
|------|------|
| HR-Shared | Access to HR shared folder |
| Sales-Shared | Access to Sales shared folder |
| IT-Admins | Administrative permissions |

Security groups are used to control access to shared resources.

---

## Shared Resources

The environment includes a shared file structure to simulate corporate file access.

Example folder structure:

```
D:\Shared
│
├── HR
├── Sales
└── Public
```

Permissions are assigned using Active Directory security groups.

| Folder | Access |
|------|------|
| HR | HR-Shared group |
| Sales | Sales-Shared group |
| Public | All domain users |

This configuration allows testing of access control and file share troubleshooting scenarios.

---

## Workstation Configuration

Two Windows 10 client machines simulate employee workstations.

Each workstation is:

- joined to the `lab.local` domain
- authenticated using Active Directory user accounts
- connected to shared network resources
- managed through Group Policy

Example login configuration:

| Machine | User |
|------|------|
| LAB-WIN10-01 | j.smith |
| LAB-WIN10-02 | a.johnson |

---

## Group Policy

Basic Group Policy settings are implemented to simulate centralized configuration management.

Example policies include:

- password complexity requirements
- account lockout thresholds
- desktop configuration policies

These policies enable troubleshooting scenarios where Group Policy may fail to apply to a workstation or user account.

---

## Supported Ticket Scenarios

The lab environment supports simulation of common Service Desk incidents.

Examples include:

- user account lockout
- password reset requests
- shared folder access issues
- workstation domain join failures
- printer connectivity problems
- new employee onboarding

Each scenario is documented within the `tickets` directory of the repository.

---

## Purpose of the Lab

The purpose of this lab is to demonstrate practical experience with common enterprise IT support tasks including:

- Active Directory administration
- access control management
- workstation domain configuration
- basic network troubleshooting
- structured incident documentation

The lab environment represents a simplified enterprise infrastructure designed for learning and portfolio demonstration.
