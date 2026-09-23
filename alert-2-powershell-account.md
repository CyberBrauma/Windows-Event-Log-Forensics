# Alert 2 — PowerShell Execution & Account Creation

## Scenario

A simulated SIEM alert reported:

- Event ID 4688: `powershell.exe` executed with `-nop -w hidden -enc`
- Event ID 4720: local account `backup_support` created
- Event ID 4732: `backup_support` added to Administrators

## Behavioral Analysis

### 1. PowerShell Execution

The process-creation event shows PowerShell being launched with parameters associated with hidden and encoded command execution.

**MITRE ATT&CK:** T1059.001 — PowerShell  
**Tactic:** Execution

### 2. Local Account Creation

The alert reports creation of a new local account.

**MITRE ATT&CK:** T1136.001 — Local Account  
**Tactic:** Persistence

### 3. Administrative Group Membership

The new account was added to the local Administrators group.

**MITRE ATT&CK:** T1098.007 — Additional Local or Domain Groups  
**Tactics:** Persistence, Privilege Escalation

## Attack Progression

The simulated sequence can be represented as:

```text
PowerShell Execution
        ↓
Local Account Creation
        ↓
Administrative Group Membership
```

The combination of events is more meaningful than any single event in isolation. The sequence should be correlated with process lineage, user context, timestamps, and additional endpoint telemetry.

## Recommended Response

- Contain or disable the suspicious account according to incident-response procedures.
- Remove unauthorized administrative membership.
- Investigate the PowerShell process and command line.
- Review surrounding Security, PowerShell, and System events.
- Reset potentially affected credentials as appropriate.
- Preserve evidence before making changes that could destroy investigative data.
