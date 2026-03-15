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

The environment is built using virtual machines hosted in VMware Workstation with Host-Only networking.

---

## Infrastructure Topology

The lab contains three virtual machines connected to the same Host-Only virtual network (VMnet1).

```
VMware Host (Host-Only Network - VMnet1)
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

The domain controller manages authentication, directory services, and DNS resolution for the domain. All machines are isolated within the Host-Only network and have no internet access.

---

## Network Configuration

All machines are connected to the same Host-Only virtual network (VMnet1).

Network range:

```
192.168.56.0 /24
```

Addressing configuration:

| System | Hostname | IP Address | Subnet Mask | DNS Server |
|------|------|------|------|------|
| Domain Controller | LAB-DC01 | 192.168.56.10 | 255.255.255.0 | 192.168.56.10 (self) |
| Workstation 1 | LAB-WIN10-01 | 192.168.56.20 | 255.255.255.0 | 192.168.56.10 |
| Workstation 2 | LAB-WIN10-02 | 192.168.56.21 | 255.255.255.0 | 192.168.56.10 |

All machines use static IP addresses. Client machines point to the domain controller as their DNS server. Because all machines are on the same subnet within a Host-Only network, no default gateway is required for intra-lab communication.

---

## Network Design Notes

The lab uses VMware Host-Only networking (VMnet1), which creates a fully isolated private network between the virtual machines and the host machine. This means:

- VMs can communicate with each other and the host machine only
- There is no internet access or external routing
- The domain controller serves as the sole DNS server for the `LAB.local` domain
- Static IP addressing is used throughout to ensure stable domain controller resolution

---

## Active Directory Domain

The lab domain is configured as:

```
LAB.local
```

The domain controller provides the following services:

- user authentication
- directory services
- domain name resolution
- group policy management

Workstations authenticate using credentials stored in Active Directory.

---

## Active Directory Structure

The domain contains a simplified organisational structure used to simulate enterprise access management.

```
LAB.local
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

- joined to the `LAB.local` domain
- configured with a static IP address
- pointed to the domain controller (`192.168.56.10`) for DNS
- authenticated using Active Directory user accounts
- connected to shared network resources
- managed through Group Policy

Example login configuration:

| Machine | IP Address | User |
|------|------|------|
| LAB-WIN10-01 | 192.168.56.20 | j.smith |
| LAB-WIN10-02 | 192.168.56.21 | a.johnson |

---

## Group Policy

Basic Group Policy settings are implemented to simulate centralised configuration management.

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
