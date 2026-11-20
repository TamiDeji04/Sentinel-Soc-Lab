# Architecture

## Overview

This lab uses a single Azure resource group to host:

- One small Windows virtual machine (log source)
- One Log Analytics workspace
- Microsoft Sentinel enabled on that workspace
- A Data Collection Rule (DCR) that sends Security Events via Azure Monitor Agent (AMA)

## Data flow

```text
1. User generates failed logons / lockout on Windows VM
2. Windows writes Security events locally
3. AMA collects configured Security Events through DCR
4. Events land in Log Analytics (SecurityEvent table)
5. Sentinel analytics rules evaluate scheduled KQL
6. Matching activity creates an incident for investigation
```

## Components

| Component | Name (lab default) | Role |
|---|---|---|
| Resource group | `rg-sentinel-soc-lab` | Boundary for all lab resources |
| Windows VM | `vm-sentinel-lab` (suggested) | Generates Security events |
| Log Analytics | `law-sentinel-soc-lab` (suggested) | Log storage/query |
| Sentinel | Enabled on LAW | Detection + incident management |
| DCR / AMA | Security Events collection | Shipping path |

## Trust / identity notes

- Lab uses a dedicated local or Entra-joined test account for failed-logon testing where practical
- No production identities
- Least privilege for any custom roles created during setup

## Cost controls

- B-series VM size
- Stop/deallocate VM when not collecting evidence
- Short retention (about 30 days)
- Delete entire resource group after documentation is complete
