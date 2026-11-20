# Evidence Index

Screenshots captured during the Azure Sentinel SOC mini-lab. Mark items **Present** only after real screenshots are added. Do not fabricate evidence.

## Configuration

| File | Status | Description |
|---|---|---|
| `Configuration/01-resource-group.png` | Pending | Resource group `rg-sentinel-soc-lab` |
| `Configuration/02-sentinel-overview.png` | Pending | Sentinel enabled on Log Analytics workspace |
| `Configuration/03-windows-vm.png` | Pending | Lab Windows VM |
| `Configuration/04-data-collection-rule.png` | Pending | DCR / AMA Security Events collection |
| `Configuration/05-securityevent-query.png` | Pending | SecurityEvent query returning data |

## Detection

| File | Status | Description |
|---|---|---|
| `Detection/01-rule-4625.png` | Pending | Failed logon analytics rule |
| `Detection/02-rule-4740.png` | Pending | Account lockout analytics rule |
| `Detection/03-incident-fired.png` | Pending | Incident created by a rule |

## Investigation

| File | Status | Description |
|---|---|---|
| `Investigation/01-incident-details.png` | Pending | Incident details / entities |
| `Investigation/02-event-query.png` | Pending | Supporting 4625/4740 query during investigation |

## Privacy notes

Before publishing screenshots, review for:

- Subscription IDs / tenant IDs (crop if needed)
- Public IPs you do not want public
- Usernames beyond lab test accounts
- Any secrets or connection strings
