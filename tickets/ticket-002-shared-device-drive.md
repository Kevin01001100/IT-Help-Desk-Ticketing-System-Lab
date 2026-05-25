# Ticket 002 — Shared Drive Access Denied

## Ticket Details

| Field | Value |
|-------|-------|
| Ticket ID | 002 |
| Date | 2025-01-21 |
| Submitted By | a.johnson |
| Assigned To | m.brown |
| Priority | Medium |
| Status | Resolved |
| Category | Access and Permissions |

---

## User Report

> "I'm trying to open the HR folder on the shared drive but I keep getting an 'Access Denied' error. I need to get into some files for a new starter. I haven't changed anything on my end."

---

## Environment

| Detail | Value |
|--------|-------|
| Domain | LAB.local |
| Domain Controller | LAB-DC01 (192.168.56.10) |
| Affected User | a.johnson |
| Affected Workstation | LAB-WIN10-02 (192.168.56.21) |
| Department | HR |
| Shared Resource | \\LAB-DC01\Shared\HR |

---

## Troubleshooting Steps

### Step 1 — Reproduce the Error

Remotely confirmed the issue by having a.johnson attempt to browse to the HR shared folder:

```
\\LAB-DC01\Shared\HR
```

The following error was returned:

```
You do not have permission to access \\LAB-DC01\Shared\HR. Contact your network administrator to request access.
```

This confirmed an access control issue rather than a network or connectivity problem.

---

### Step 2 — Check Shared Folder Permissions

Logged into LAB-DC01 and navigated to:

```
D:\Shared\HR
```

Right-clicked the folder and selected **Properties**, then opened the **Security** tab.

Confirmed that permissions on the HR folder are assigned to the **HR-Shared** security group, not to individual users. The HR-Shared group has the following permissions:

| Permission | HR-Shared Group |
|------------|-----------------|
| Read | Allow |
| Write | Allow |
| Full Control | Deny |

Permissions were correctly configured. The issue was not with the folder permissions themselves.

---

### Step 3 — Check User Group Membership

Opened **Active Directory Users and Computers** on LAB-DC01.

Navigated to:

```
LAB.local > Employees
```

Located the user account:

```
a.johnson
```

Right-clicked the account and selected **Properties**, then opened the **Member Of** tab.

Confirmed that **a.johnson** was not a member of the **HR-Shared** security group. The account had no group memberships beyond the default **Domain Users** group.

This was the root cause of the access denied error.

---

### Step 4 — Add User to the HR-Shared Group

In **Active Directory Users and Computers**, navigated to:

```
LAB.local > Groups
```

Located the group:

```
HR-Shared
```

Right-clicked and selected **Properties**, then opened the **Members** tab.

Clicked **Add** and entered:

```
a.johnson
```

Clicked **Check Names** to confirm the account resolved correctly, then clicked **OK** and **Apply**.

The user was successfully added to the HR-Shared group.

---

### Step 5 — Force Group Policy and Token Refresh

Advised a.johnson to log off and log back on to LAB-WIN10-02 to refresh the Kerberos token and pick up the new group membership.

After logging back in, a.johnson was able to access the HR shared folder without error:

```
\\LAB-DC01\Shared\HR
```

Access was confirmed.

---

### Step 6 — Communicate Resolution to User

Contacted a.johnson and advised:

- Access to the HR shared folder has been restored.
- The issue was caused by a missing group membership — the account had not been added to the HR-Shared security group.
- Recommended logging off and back on in future if access issues occur shortly after a permission change, as group membership changes require a new login session to take effect.

---

## Root Cause

The user account `a.johnson` was not a member of the **HR-Shared** security group. Access to the HR shared folder on LAB-DC01 is controlled by group membership — without being in the HR-Shared group, the user had no permissions on the folder and received an Access Denied error.

This appears to have been an oversight during the original account setup, where the user was created in the Employees OU but not assigned to the appropriate security group.

---

## Resolution

The `a.johnson` account was added to the **HR-Shared** security group via Active Directory Users and Computers on LAB-DC01. The user logged off and back on to refresh their security token. Access to `\\LAB-DC01\Shared\HR` was verified and confirmed working.

---

## Prevention Recommendations

- User onboarding procedures should include a checklist step to assign new accounts to the appropriate security groups based on department.
- A standard group membership template per department would reduce the likelihood of access being missed at account creation.
- Periodic access reviews can identify accounts with missing or incorrect group memberships before users encounter issues.

---

## Screenshots

Screenshots documenting this ticket are located in:

```
screenshots/tickets/ticket-002/
```

Expected screenshots include:

- Access Denied error on LAB-WIN10-02
- HR folder Security tab showing HR-Shared group permissions
- ADUC showing a.johnson's Member Of tab before the fix
- ADUC showing HR-Shared group Members tab after adding a.johnson
- Successful folder access after group membership update
