# Detection: Account Lockout (Event ID 4740)

## Why I built this

Failed logons are useful, but lockouts tell me the failures actually impacted an account. I wanted a second rule specifically for Event ID 4740.

## MITRE ATT&CK mapping (lab)

- Tactic: Credential Access (and sometimes Impact, depending on context)
- Related technique: Brute Force (T1110)

## Data I used

- Table: `SecurityEvent`
- Event ID: `4740`

## How I configured the rule

| Setting | What I used |
|---|---|
| Name | Lab - Account Lockout 4740 |
| Type | Scheduled |
| Severity | High |
| Run every | 5 minutes |
| Look back | 15 minutes |
| Threshold | Alert if the query returns any rows |

## KQL

See [`queries/securityevent-4740.kql`](../queries/securityevent-4740.kql).

## How this ties to my other lab

I also did a Windows lockout policy lab here:  
[Enterprise Security Controls](https://github.com/TamiDeji04/Enterprise-Security-Controls)

That one was about configuring lockout on the endpoint. This one is about detecting it in Sentinel.

## Status

Rule created and enabled in my lab. My investigation screenshots were heavier on 4625 activity; 4740 is ready whenever lockout events show up.
