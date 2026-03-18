# Active Directory Structure

## Overview

This document describes the Active Directory structure used in the IT Help Desk Ticketing System Lab.

The directory structure simulates a simplified enterprise environment where users, computers, and access permissions are managed centrally through Active Directory.

The structure supports common IT support tasks including:

- user account management
- workstation management
- group-based access control
- shared resource permissions

The domain used in this lab is:

```
LAB.local
```

---

## Organizational Unit Structure

Organizational Units (OUs) are used to organize directory objects and allow administrative policies to be applied to specific groups of users or computers.

The following OU structure is present in the domain:

```
LAB.local
│
├── Builtin
├── Computers
├── Domain Controllers
├── Employees
├── ForeignSecurityPrincipals
├── Groups
├── IT
├── Managed Service Accounts
├── Users
└── Workstations
```

The OUs actively used for lab administration and ticket simulation are:

| OU | Purpose |
|----|---------|
| Employees | Standard domain user accounts |
| IT | IT administrator accounts |
| Groups | Security groups for access control |
| Workstations | Domain-joined client machines |

---

### Employees OU

The **Employees** OU contains standard domain user accounts representing employees within the organization.

This OU allows administrative policies to be applied to employee accounts.

Examples include:

- password policies
- account lockout policies
- desktop configuration policies

---

### IT OU

The **IT** OU contains administrative or privileged user accounts used by IT personnel.

Separating IT accounts from regular employee accounts allows different security policies or administrative permissions to be applied if needed.

Example account:

```
m.brown
```

---

### Groups OU

The **Groups** OU stores security groups used for role-based access control.

Security groups simplify permission management by allowing administrators to assign permissions to groups instead of individual users.

Example groups created in this lab:

| Group Name | Purpose |
|-----------|-----------|
| HR-Shared | Access to HR shared folder |
| Sales-Shared | Access to Sales shared folder |
| IT-Admins | Administrative privileges |

---

### Workstations OU

The **Workstations** OU stores domain-joined client machines.

Computers are moved into this OU after joining the domain to allow centralized management and Group Policy application.

Example workstation objects:

| Computer Name | Role | Status |
|--------------|------|--------|
| LAB-WIN10-01 | Employee workstation | Configured and verified |
| LAB-WIN10-02 | Employee workstation | Configuration pending |

---

## User Accounts

Example user accounts were created to simulate employees within an organization.

| Username | Department | Description |
|--------|--------|--------|
| j.smith | Sales | Employee workstation user |
| a.johnson | HR | Employee workstation user |
| m.brown | IT | IT administrator |

These accounts are used throughout the lab to simulate common service desk scenarios.

Examples include:

- password resets
- account lockouts
- access permission troubleshooting
- user onboarding

---

## Security Groups

Security groups are used to manage permissions for shared resources.

Using groups instead of assigning permissions directly to users simplifies access management and follows common enterprise best practices.

Example groups created in this lab:

| Group Name | Purpose |
|-----------|-----------|
| HR-Shared | Access to HR shared folder |
| Sales-Shared | Access to Sales shared folder |
| IT-Admins | Administrative privileges |

Users are assigned to groups based on their role or department.

Permissions are then applied to the groups.

This approach simplifies access control and reduces administrative overhead.

---

## Group Membership Example

Example group membership configuration:

| User | Group Membership |
|------|------------------|
| j.smith | Sales-Shared |
| a.johnson | HR-Shared |
| m.brown | IT-Admins |

This allows the file server to grant folder access based on group membership.

---

## Access Control Model

The lab uses a **group-based access control model**, which is standard practice in enterprise environments.

The access flow follows this structure:

```
User → Security Group → Resource Permission
```

Example:

```
a.johnson → HR-Shared → HR Folder Access
```

This design improves scalability and simplifies access management.

---

## Shared Resource Integration

Security groups are used to control access to shared folders.

Example shared folder structure:

```
D:\Shared
│
├── HR
├── Sales
└── Public
```

Permissions are assigned as follows:

| Folder | Access Group |
|------|------|
| HR | HR-Shared |
| Sales | Sales-Shared |
| Public | All Domain Users |

This structure allows service desk tickets involving:

- access denied errors
- missing mapped drives
- permission troubleshooting

---

## Group Policy Integration

Organizational Units allow Group Policy Objects (GPOs) to be applied to specific users or computers.

Example policies implemented in the lab include:

- password policy enforcement
- account lockout thresholds
- desktop configuration policies

Group Policy enables centralized management of domain systems.

---

## Verification

The following tools were used to verify the directory structure:

- Active Directory Users and Computers
- Group Policy Management
- DNS Manager

Objects were verified to exist in the correct Organizational Units and group memberships were confirmed.

---

## Screenshots

Example screenshots documenting the directory structure include:

- Active Directory Users and Computers console showing OU structure
- User account creation
- Group membership configuration
- Workstation objects in the Computers and Workstations OUs

Screenshots are located in the repository directory:

```
screenshots/
```

---

## Summary

The Active Directory structure in this lab provides a simplified but realistic enterprise directory environment.

The design supports:

- centralized user management
- group-based access control
- workstation authentication
- shared resource permissions

This structure enables simulation of common service desk tasks including account management, access troubleshooting, and workstation administration.
