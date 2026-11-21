# Evidence Index

These are the screenshots I kept from the lab. I copied them from my Desktop `Sentinel Project` folder into here and renamed them so the repo stays organized.

## Configuration

| File | Status | What it shows |
|---|---|---|
| `Configuration/01-resource-group.png` | Present | My resource groups list, including the Sentinel lab RGs in North Central US |
| `Configuration/02-sentinel-overview.png` | Present | Sentinel overview for `law-sentinel-soc-lab` |
| `Configuration/03-windows-vm.png` | Present | Me RDP’d into `vm-sentinel-lab` |
| `Configuration/04-data-collection-rule.png` | Present | Windows Security Events via AMA DCR tied to the VM |
| `Configuration/05-securityevent-query.png` | Present | SecurityEvent query proving logs from `vm-sentinel-lab` |

## Detection

| File | Status | What it shows |
|---|---|---|
| `Detection/01-rule-4625.png` | Present | My Failed Logons 4625 rule ready to save |
| `Detection/02-rule-4740.png` | Present | My Account Lockout 4740 rule ready to save |
| `Detection/03-incident-fired.png` | Present | Incidents created by the failed logons rule |

## Investigation

| File | Status | What it shows |
|---|---|---|
| `Investigation/01-incident-details.png` | Present | Incident/cases list from the failed logons activity |
| `Investigation/02-event-query.png` | Present | 4625/4740 query results during investigation |

## Extra supporting shots

I also kept a few in-progress screens under `Evidence/_supporting/` (DCR create flow, rule logic panes, analytics list).

## What I noticed in the evidence

- Workspace: `law-sentinel-soc-lab`
- VM: `vm-sentinel-lab`
- DCR: `dcr-soc-ab`
- Failed logons clearly flowed and created incidents
- Opening RDP publicly got noisy with spray attempts against common usernames

## Before making this public

I should review screenshots for:
- student email / school branding
- public IP in the RDP window title

I’d crop those if I don’t want them on GitHub.
