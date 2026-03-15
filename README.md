# IT Help Desk Ticketing System Lab

## Overview

This project simulates a real-world IT help desk environment focused on ticket intake, user support, troubleshooting, resolution, and documentation.

The goal is to demonstrate hands-on experience with common service desk responsibilities such as account support, workstation troubleshooting, access issues, software requests, and standard operating documentation.

---

## Objectives

- Simulate common IT support tickets
- Practice structured troubleshooting workflows
- Document incidents and service requests clearly
- Demonstrate knowledge of Windows, Active Directory, networking, and user support

---

## Technologies Used

- Windows Server 2019
- Windows 10
- Active Directory Domain Services
- DNS
- Group Policy
- VMware Workstation (Host-Only Networking)
- Shared folders and file permissions
- Ticket templates

---

## Lab Environment

- 1x Domain Controller (LAB-DC01) — Windows Server 2019, running AD DS and DNS
- 2x Windows 10 client workstations (LAB-WIN10-01, LAB-WIN10-02)
- Simulated end users authenticated via Active Directory accounts
- Shared folder structure hosted on the domain controller
- All machines connected via a VMware Host-Only network (192.168.56.0/24)

For full infrastructure details see [lab-architecture.md](lab-architecture.md).

---

## Skills Demonstrated

- Ticket triage
- Incident documentation
- User account administration
- Password resets and account unlocks
- Basic network troubleshooting
- File share permission troubleshooting
- Domain join troubleshooting
- Group Policy troubleshooting
- Professional technical documentation

---

## Ticket Scenarios

1. Locked Active Directory account
2. User cannot access shared drive
3. Domain join failure on workstation
4. Printer connectivity issue
5. New employee onboarding request
6. Group Policy not applying correctly

---

## Repository Structure

```
/
├── README.md
├── lab-architecture.md
└── tickets/
    ├── ticket-001-account-lockout.md
    ├── ticket-002-shared-drive-access.md
    ├── ticket-003-domain-join-failure.md
    ├── ticket-004-printer-connectivity.md
    ├── ticket-005-new-employee-onboarding.md
    └── ticket-006-group-policy-not-applying.md
```
