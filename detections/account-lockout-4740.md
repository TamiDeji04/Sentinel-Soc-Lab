# Detection: Account Lockout (Event ID 4740)

## Purpose

Detect Windows account lockout events, which often follow repeated failed authentications and can indicate brute-force impact or lockout abuse.

## MITRE ATT&CK

- Tactic: Credential Access / Impact (context-dependent)
- Related technique notes: Brute Force (T1110) — lab mapping

## Data source

- Table: `SecurityEvent`
- Event ID: `4740`

## Suggested rule settings

| Setting | Lab value |
|---|---|
| Rule type | Scheduled |
| Frequency | 5 minutes |
| Period | 5–15 minutes |
| Threshold idea | Any 4740 in lab, or >= 1 per account |
| Severity | Medium/High |

## KQL

See [`queries/securityevent-4740.kql`](../queries/securityevent-4740.kql).

## Validation

1. Trigger lockout on a test account (if local policy allows), or ensure 4740 appears from lab testing
2. Confirm event in Log Analytics
3. Confirm analytics rule creates an incident
4. Screenshot rule + incident → `Evidence/Detection/`

## Relationship to other projects

Pairs with [Enterprise Security Controls](https://github.com/TamiDeji04/Enterprise-Security-Controls), which configured local lockout threshold/duration and captured 4625/4740 evidence on Windows.

## Status

Pending implementation in Azure.
