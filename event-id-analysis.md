# Windows Event ID Analysis

## Purpose

This document summarizes the Windows Event IDs examined in the project.

| Event ID | Activity | Investigative Value |
|---|---|---|
| 4624 | Successful logon | Helps establish successful authentication activity and timing. |
| 4625 | Failed logon | Helps identify failed authentication activity and repeated attempts. |
| 4672 | Special privileges assigned to a new logon | Helps identify logons associated with special privileges. |
| 4688 | Process creation | Helps identify processes that were executed and supports process-level investigation. |
| 4720 | User account created | Helps identify creation of new accounts. |
| 4726 | User account deleted | Helps identify account deletion activity. |
| 4732 | Member added to a security-enabled local group | Helps identify local group-membership changes. |
| 104 | Event log cleared | Helps identify when an event log was cleared. |

## Forensic Consideration

Event IDs should be interpreted in context. A single event generally provides only part of an investigation. Correlation with timestamps, accounts, source information, process activity, and surrounding events can provide a more complete picture.

## Portfolio Takeaway

This analysis demonstrates the ability to move from individual Windows events toward broader behavioral analysis instead of treating log entries as isolated facts.
