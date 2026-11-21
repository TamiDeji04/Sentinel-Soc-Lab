# Evidence Index

Screenshots from the Azure Sentinel SOC mini-lab (copied from Desktop `Sentinel Project/`; originals preserved there).

## Configuration

| File | Status | Description |
|---|---|---|
| `Configuration/01-resource-group.png` | Present | Resource groups list showing `nrg-sentinel-soc-lab` and `rg-sentinel-soc-lab` (North Central US) |
| `Configuration/02-sentinel-overview.png` | Present | Sentinel overview for `law-sentinel-soc-lab` showing incident activity |
| `Configuration/03-windows-vm.png` | Present | RDP session to `vm-sentinel-lab` (Windows 11 lab desktop); Azure VM blade screenshot optional upgrade |
| `Configuration/04-data-collection-rule.png` | Present | Windows Security Events via AMA DCR with `vm-sentinel-lab` selected (`dcr-soc-ab`) |
| `Configuration/05-securityevent-query.png` | Present | `SecurityEvent` query by Computer/EventID including many 4625 events from `vm-sentinel-lab` |

## Detection

| File | Status | Description |
|---|---|---|
| `Detection/01-rule-4625.png` | Present | Review + create for `Lab - Failed Logons 4625` (validation passed) |
| `Detection/02-rule-4740.png` | Present | Review + create for `Lab - Account Lockout 4740` (validation passed) |
| `Detection/03-incident-fired.png` | Present | Defender/Sentinel Cases list showing multiple `Lab - Failed Logons 4625` incidents |

## Investigation

| File | Status | Description |
|---|---|---|
| `Investigation/01-incident-details.png` | Present | Incident/cases list for failed-logon rule (same capture as incident-fired; open a single incident detail pane if you want a stronger shot) |
| `Investigation/02-event-query.png` | Present | Query of Event IDs 4625/4740 from `vm-sentinel-lab` |

## Supporting (optional)

Stored under `Evidence/_supporting/` (DCR create flow, rule logic panes, analytics rules list).

## Lab notes from evidence

- Resource group appears as `nrg-sentinel-soc-lab` / `rg-sentinel-soc-lab` in portal tabs; workspace `law-sentinel-soc-lab`; VM `vm-sentinel-lab`; region **North Central US**
- DCR name: `dcr-soc-ab`
- Failed logons are clearly flowing; many 4625 incidents were generated
- 4740 rule exists; investigation query shown was dominated by 4625 (lockout may not have fired yet)

## Privacy review before GitHub

Screenshots show:
- Student account identity (`W218505713@student...`, Houston City College)
- Azure portal tenant/workspace context
- Public IP of the lab VM in the RDP window title

Crop or redact account/email/public IP before making the repo public if you do not want that visible.

## Security note

Public RDP on a student VM can attract internet password spraying. Evidence shows failed logons against multiple account names (`ADMINISTRATOR`, `ADMIN`, `USER`, etc.). Consider:
- Restrict NSG RDP to your IP only, or
- Stop/deallocate the VM when idle, or remove public IP when documentation is done
