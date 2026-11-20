# Detection: Failed Logons (Event ID 4625)

## Purpose

Detect repeated failed Windows logon attempts that may indicate password guessing or brute force.

## MITRE ATT&CK

- Tactic: Credential Access
- Technique: Brute Force (T1110) — lab mapping

## Data source

- Table: `SecurityEvent`
- Event ID: `4625`

## Suggested rule settings

| Setting | Lab value |
|---|---|
| Rule type | Scheduled |
| Frequency | 5 minutes |
| Period | 5–15 minutes |
| Threshold idea | >= 5 failures by account/host in the window |
| Severity | Medium |

## KQL

See [`queries/securityevent-4625.kql`](../queries/securityevent-4625.kql).

Tune thresholds after you confirm event volume in your lab.

## Validation

1. Generate multiple failed logons on the lab VM
2. Confirm events in Log Analytics
3. Confirm analytics rule creates an incident
4. Screenshot rule + incident → `Evidence/Detection/`

## Status

Pending implementation in Azure.
