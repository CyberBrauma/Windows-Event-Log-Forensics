# MITRE ATT&CK Mapping

## Mapping Method

The project uses the following investigation pattern:

```text
Event Evidence
      ↓
Observed Behavior
      ↓
MITRE ATT&CK Technique
      ↓
ATT&CK Tactic
```

## Alert 1

| Evidence | Behavior | Technique | Tactic |
|---|---|---|---|
| 4625 + 4624 | Repeated failed authentication followed by successful authentication | T1110 — Brute Force | Credential Access |

## Alert 2

| Evidence | Behavior | Technique | Tactic |
|---|---|---|---|
| 4688 | PowerShell execution using suspicious command-line parameters | T1059.001 — PowerShell | Execution |
| 4720 | Local account creation | T1136.001 — Local Account | Persistence |
| 4732 | Account added to local Administrators group | T1098.007 — Additional Local or Domain Groups | Persistence / Privilege Escalation |

## Why Correlation Matters

MITRE ATT&CK mapping describes observed behavior; it does not independently establish that an attack occurred. The surrounding context, timing, user identity, process lineage, and other telemetry should be considered during an investigation.

## References

- https://attack.mitre.org/techniques/T1059/001/
- https://attack.mitre.org/techniques/T1136/001/
- https://attack.mitre.org/techniques/T1098/007/
