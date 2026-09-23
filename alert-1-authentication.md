# Alert 1 — Suspicious Authentication Pattern

## Scenario

A simulated SIEM alert reported:

- 25 Event ID 4625 failures within three minutes
- Source IP: `192.168.1.75`
- Target user: `admin`
- Event ID 4624 success from the same source and account
- Logon Type 3 (Network)

## Analysis

The activity represents repeated failed authentication attempts followed by a successful authentication from the same source and target.

This pattern warrants investigation because repeated authentication failures can be associated with credential-guessing activity. The successful logon should be investigated to determine whether it was legitimate or represents unauthorized access.

## MITRE ATT&CK

- **Event Evidence:** 4625 + 4624
- **Observed Behavior:** Repeated failed authentication attempts followed by successful authentication
- **Technique:** T1110 — Brute Force
- **Tactic:** Credential Access

## Follow-Up Investigation

1. Review additional authentication events around the same time.
2. Review Event ID 4672 for special-privilege logons.
3. Examine account-management events.
4. Investigate the source IP and related network activity.
5. Review endpoint telemetry for additional suspicious behavior.
6. Determine whether the successful authentication was expected.

## Investigation Principle

Do not treat the sequence as automatic proof of compromise. Correlate the authentication pattern with additional evidence before reaching a conclusion.
