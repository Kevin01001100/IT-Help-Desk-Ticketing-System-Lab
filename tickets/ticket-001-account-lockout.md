# Ticket 001 — Account Lockout

## Ticket Details

| Field | Value |
|-------|-------|
| Ticket ID | 001 |
| Date | 2025-01-20 |
| Submitted By | j.smith |
| Assigned To | m.brown |
| Priority | Medium |
| Status | Resolved |
| Category | User Account Support |

---

## User Report

> "I tried logging into my computer this morning and it says my account is locked. I haven't changed my password or done anything different."

---

## Environment

| Detail | Value |
|--------|-------|
| Domain | LAB.local |
| Domain Controller | LAB-DC01 (192.168.56.10) |
| Affected User | j.smith |
| Affected Workstation | LAB-WIN10-01 (192.168.56.20) |
| Department | Sales |

---

## Troubleshooting Steps

### Step 1 — Verify the Account Is Locked

Logged into LAB-DC01 and opened **Active Directory Users and Computers**.

Navigated to:

```
LAB.local > Employees
```

Located the user account:

```
j.smith
```

Right-clicked the account and selected **Properties**, then opened the **Account** tab.

Confirmed that the checkbox was ticked:

```
Unlock account. This account is currently locked out on this Active Directory Domain Controller.
```

This confirmed the account was locked.

---

### Step 2 — Check the Account Lockout Policy

Opened **Group Policy Management** on LAB-DC01.

Reviewed the Default Domain Policy to confirm the lockout threshold configured for the domain:

```
Account lockout threshold: 5 invalid logon attempts
Account lockout duration: 30 minutes
Observation window: 30 minutes
```

This confirmed the account was locked automatically after exceeding failed logon attempts.

---

### Step 3 — Review Event Logs for Lockout Source

Opened **Event Viewer** on LAB-DC01.

Navigated to:

```
Windows Logs > Security
```

Filtered for Event ID **4740** (account lockout event).

Identified repeated failed logon attempts originating from:

```
LAB-WIN10-01
```

This indicated the lockout was triggered from the user's own workstation, most likely due to a saved credential or a previous session holding an outdated password.

---

### Step 4 — Unlock the Account

In **Active Directory Users and Computers**, right-clicked the `j.smith` account and selected **Properties**.

On the **Account** tab, unticked:

```
Unlock account
```

Clicked **Apply** then **OK**.

The account was successfully unlocked.

---

### Step 5 — Communicate Resolution to User

Contacted j.smith and advised:

- The account has been unlocked and is ready to use.
- Recommended checking for any saved credentials in **Windows Credential Manager** that may have been using an old password.
- Advised the user to update any saved credentials if a recent password change had occurred.

---

## Root Cause

The account lockout was triggered by repeated failed authentication attempts originating from LAB-WIN10-01. This is consistent with a saved or cached credential that no longer matched the current domain password. The domain lockout policy locked the account after five consecutive failures.

---

## Resolution

The `j.smith` account was unlocked via Active Directory Users and Computers on LAB-DC01. The user was advised to check Windows Credential Manager for any outdated saved credentials.

---

## Prevention Recommendations

- Users should be reminded to update saved credentials in Windows Credential Manager after any password change.
- The helpdesk team can use the **Account Lockout and Management Tools** (Microsoft) to identify lockout sources more efficiently in production environments.
- Consider enabling a self-service password reset solution to reduce ticket volume for routine lockouts.

---

## Screenshots

Screenshots documenting this ticket are located in:

```
screenshots/tickets/ticket-001/
```

Expected screenshots include:

- ADUC showing the locked account (Account tab)
- Event Viewer filtered for Event ID 4740
- ADUC showing the account after unlock
