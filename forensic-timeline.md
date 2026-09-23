# Forensic Timeline Reconstruction

## Purpose

A forensic timeline organizes security-relevant events chronologically so investigators can understand how activity developed over time.

## Simulated Authentication Timeline

| Sequence | Event | Interpretation |
|---|---|---|
| 1 | Event ID 4625 × 25 | Repeated failed authentication attempts |
| 2 | Event ID 4624 | Successful authentication from the same source/account |
| 3 | Follow-up investigation | Determine whether the successful authentication was legitimate |

## Simulated PowerShell / Account Timeline

| Sequence | Event | Interpretation |
|---|---|---|
| 1 | Event ID 4688 | PowerShell process execution |
| 2 | Event ID 4720 | New local account created |
| 3 | Event ID 4732 | New account added to Administrators |
| 4 | Follow-up investigation | Determine whether the sequence represents authorized administration or malicious activity |

## Timeline Principle

Timestamps help establish relationships between events. Investigators should correlate the timeline with user accounts, source addresses, process lineage, authentication details, and other available telemetry.
