# Active Directory Structure

## Overview

This document describes the Active Directory structure used in the IT Help Desk Ticketing System Lab.

The directory structure is designed to simulate a simplified enterprise environment where users, computers, and access permissions are managed centrally through Active Directory.

The structure supports common IT support tasks including:

- user account management
- workstation management
- group-based access control
- shared resource permissions

The domain used in this lab is:

```
lab.local
```

---

## Organizational Unit Structure

Organizational Units (OUs) are used to organize directory objects and allow administrative policies to be applied to specific groups of users or computers.

The following OU structure was implemented:

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

### Users OU

The **Users** OU contains all domain user accounts.

Sub-OUs are used to separate users by role or department.

```
Users
│
├── Employees
└── IT
```

This structure allows administrative policies to be applied selectively.

For example:

- password policies
- desktop restrictions
- software policies

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

## Computer Objects

Domain-joined machines are stored in the **Computers** OU.

Example computer objects:

| Computer Name | Role |
|--------------|------|
| LAB-WIN10-01 | Employee workstation |
| LAB-WIN10-02 | Employee workstation |

These machines authenticate to the domain and receive configuration through Group Policy.

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

Organizational Units also allow Group Policy Objects (GPOs) to be applied to specific users or computers.

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

- Active Directory Users and Computers console
- User account creation
- Group membership configuration
- Organizational Unit structure

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
