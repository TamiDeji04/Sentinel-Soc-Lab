# Detection: Failed Logons (Event ID 4625)

## Why I built this

I wanted a straightforward rule that catches repeated failed Windows logons. That’s one of the first things I’d expect to look for in a SOC.

## MITRE ATT&CK mapping (lab)

- Tactic: Credential Access
- Technique: Brute Force (T1110)

## Data I used

- Table: `SecurityEvent`
- Event ID: `4625`

## How I configured the rule

| Setting | What I used |
|---|---|
| Name | Lab - Failed Logons 4625 |
| Type | Scheduled |
| Severity | Medium |
| Run every | 5 minutes |
| Look back | 15 minutes |
| Threshold | >= 5 failures by account/host, then alert if results > 0 |

## KQL

See [`queries/securityevent-4625.kql`](../queries/securityevent-4625.kql).

## How I validated it

1. Failed logons on `vm-sentinel-lab`
2. Confirmed 4625 events in Log Analytics
3. Confirmed Sentinel created incidents from this rule
4. Saved screenshots under `Evidence/Detection/`

## Status

Done in my lab.
