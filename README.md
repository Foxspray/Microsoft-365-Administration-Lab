# Microsoft 365 Administration Lab

Hands-on Microsoft 365 lab focused on common Helpdesk / Junior Administrator tasks.

Environment: **Microsoft 365 Business Premium trial tenant**

## What I built

### Microsoft 365 Admin Center

- created test users
- assigned Microsoft 365 Business Premium licenses
- reset user passwords
- required password change at next sign-in
- verified that licensed users could sign in and use Microsoft 365 services

### Exchange Online

I created and tested user mailboxes in Exchange Online.

A test message was sent between users and then checked with **Message Trace** in the Exchange Admin Center.

![Exchange Message Trace](exchange-message-trace-delivered.png)

I also created a shared mailbox:

```text
Helpdesk
```

and configured mailbox delegation, including:

- **Full Access**
- **Send As**

![Shared mailbox Send As](exchange-shared-mailbox-send-as.png)

### Microsoft Entra ID

I created a Security group:

```text
IT-Users
```

and added test users to it.

![Entra ID security group](entra-security-group-it-users.png)

The group is used later as the assignment target for Intune policies.

### Microsoft Intune

I created an Android Enterprise BYOD compliance policy:

```text
Android-BYOD-Compliance
```

The policy is assigned to the `IT-Users` group.

Configured requirements include:

- device storage encryption
- blocking apps from unknown sources
- device password / screen lock
- work profile password protection

![Intune Android BYOD compliance policy](intune-android-byod-compliance-policy.png)

## Troubleshooting

### Outlook account had no mailbox

I initially tried to open Outlook with the administrator account.

The account was not licensed, so Exchange had not provisioned a mailbox and Outlook returned a mailbox/license error.

I verified the difference between the unlicensed administrator account and the licensed test users, then used a licensed account for Outlook and Exchange testing.

### Verifying mail delivery

Instead of only checking the recipient inbox, I used **Exchange Message Trace** to confirm that the test message had been delivered successfully.

This is useful when troubleshooting reports such as:

```text
"The email was sent, but the recipient says it did not arrive."
```

### Shared mailbox permissions

The Helpdesk shared mailbox was configured with separate permissions instead of sharing one user account:

```text
Full Access = open and manage the mailbox
Send As     = send mail as Helpdesk
```

## Next steps

The lab is still in progress.

Planned additions:

- connect Managed Google Play to Intune
- enroll a real Android phone as a BYOD device
- create and test an Android Enterprise work profile
- verify `Compliant` / `Noncompliant` device status
- configure MFA for test users
- test a basic Conditional Access scenario
- add basic Teams / SharePoint administration

Planned Android workflow:

```text
Android phone
     ↓
Intune enrollment
     ↓
Android Enterprise Work Profile
     ↓
IT-Users
     ↓
Android-BYOD-Compliance
     ↓
Compliant / Noncompliant
```

## Current scope

Technologies used so far:

- Microsoft 365 Admin Center
- Exchange Online
- Exchange Message Trace
- Shared Mailboxes
- Microsoft Entra ID
- Security Groups
- Microsoft Intune
- Android Enterprise BYOD compliance policies

**Status: in progress**
