# Windows Event Log Forensics & MITRE ATT&CK Analysis

## Overview

This project demonstrates a hands-on Windows event-log investigation performed in a controlled environment. The project focuses on authentication activity, account and privilege changes, event-log clearing, suspicious PowerShell execution, SIEM-style alert analysis, and MITRE ATT&CK mapping.

> **Project note:** The SIEM alerts in this project are simulated scenarios used to demonstrate investigation and analysis techniques. They do not represent a confirmed real-world intrusion.

## Objectives

- Identify Windows logs used in forensic investigations
- Analyze authentication, audit, and system events
- Recognize potentially suspicious security activity
- Correlate related Windows Event IDs
- Map observed behaviors to MITRE ATT&CK
- Reconstruct activity sequences and timelines
- Document investigation findings using a structured approach

## Tools & Technologies

- Windows Event Viewer
- Windows Security Event Logs
- Windows System Event Logs
- PowerShell
- MITRE ATT&CK
- Windows virtual machine
- SIEM-style alert analysis

## Windows Event IDs Examined

| Event ID | Activity |
|---|---|
| 4624 | Successful logon |
| 4625 | Failed logon |
| 4672 | Special privileges assigned to a new logon |
| 4688 | Process creation |
| 4720 | User account created |
| 4726 | User account deleted |
| 4732 | Member added to a security-enabled local group |
| 104 | Event log cleared |

## Investigation 1: Event Log Clearing

Windows Event Viewer was used to examine system activity and identify Event ID 104. The captured evidence shows a log-clear event associated with the Windows PowerShell log.

### Evidence

![Event ID 104 - Log Cleared](screenshots/event-id-104-log-cleared.png)

### Finding

Event-log clearing is security-relevant because removing logs can reduce the evidence available to investigators. A log-clear event by itself does not establish malicious activity; investigators should correlate it with the user, timestamp, surrounding events, administrative activity, and other endpoint telemetry.

## Investigation 2: Suspicious Authentication Pattern

### Simulated SIEM Alert

- Event ID 4625: 25 failed logon attempts within three minutes
- Source IP: `192.168.1.75`
- Target account: `admin`
- Event ID 4624: successful logon from the same source IP and account
- Logon Type: 3 (Network)

### Observed Behavior

The sequence shows repeated authentication failures followed by successful authentication from the same source and target account.

This pattern can be consistent with credential-guessing activity and warrants additional investigation. The sequence alone does not prove that an attacker successfully compromised the account.

### MITRE ATT&CK Mapping

**Event Evidence:** 4625 + 4624

**Observed Behavior:** Repeated failed authentication attempts followed by successful authentication

**Technique:** T1110 — Brute Force

**Tactic:** Credential Access

### Next Investigation Steps

- Review additional 4624 and 4625 events around the same time
- Examine the source IP and other authentication activity
- Review Event ID 4672 for special-privilege logons
- Review account-management events
- Check endpoint and network telemetry for related activity
- Determine whether the successful authentication was expected

## Investigation 3: Suspicious PowerShell Execution & Account Creation

### Simulated SIEM Alert

The second scenario contains three related events:

1. Event ID 4688 — `powershell.exe` executed with `-nop`, `-w hidden`, and `-enc`
2. Event ID 4720 — local account `backup_support` created
3. Event ID 4732 — `backup_support` added to the local Administrators group

### Observed Behaviors

**PowerShell execution:** The alert contains PowerShell command-line parameters associated with hidden and encoded execution.

**Account creation:** A new local account named `backup_support` was created.

**Group membership change:** The new account was added to the Administrators group.

### MITRE ATT&CK Mapping

| Evidence | Observed Behavior | Technique | Tactic |
|---|---|---|---|
| Event ID 4688 | Suspicious PowerShell execution | T1059.001 — PowerShell | Execution |
| Event ID 4720 | New local account created | T1136.001 — Local Account | Persistence |
| Event ID 4732 | Account added to Administrators group | T1098.007 — Additional Local or Domain Groups | Persistence / Privilege Escalation |

## Attack Progression

The simulated events demonstrate a possible progression from command execution to account creation and elevated group membership:

```text
PowerShell Execution
        ↓
Local Account Created
        ↓
Account Added to Administrators
        ↓
Potential Persistence / Elevated Access
```

The significance comes from correlating the events and their timing rather than treating any single event as proof of compromise.

## Recommended Response Actions

For a real investigation, initial response actions could include:

- Disable or contain the suspicious account according to incident-response procedures
- Remove unauthorized administrative group membership
- Review authentication activity
- Investigate PowerShell execution and process lineage
- Examine surrounding Security and System logs
- Reset potentially compromised credentials when appropriate
- Preserve relevant evidence
- Determine whether other systems or accounts were affected

## Skills Demonstrated

- Windows Event Log Analysis
- Digital Forensics
- Authentication Analysis
- Account and Privilege Investigation
- PowerShell Security Analysis
- SIEM Alert Investigation
- MITRE ATT&CK Mapping
- Incident Response Fundamentals
- Forensic Timeline Reconstruction
- Security Documentation

## Project Structure

```text
windows-event-log-forensics/
├── README.md
├── screenshots/
│   ├── event-viewer-openssh.png
│   └── event-id-104-log-cleared.png
├── analysis/
│   ├── event-id-analysis.md
│   ├── alert-1-authentication.md
│   └── alert-2-powershell-account.md
├── mitre-mapping/
│   └── attack-mapping.md
└── documentation/
    └── forensic-timeline.md
```

## References

- MITRE ATT&CK — PowerShell (T1059.001): https://attack.mitre.org/techniques/T1059/001/
- MITRE ATT&CK — Create Account (T1136): https://attack.mitre.org/techniques/T1136/
- MITRE ATT&CK — Local Account (T1136.001): https://attack.mitre.org/techniques/T1136/001/
- MITRE ATT&CK — Account Manipulation (T1098): https://attack.mitre.org/techniques/T1098/
- MITRE ATT&CK — Additional Local or Domain Groups (T1098.007): https://attack.mitre.org/techniques/T1098/007/

## Disclaimer

This project uses simulated security scenarios in a controlled environment for cybersecurity analysis and demonstration purposes.
