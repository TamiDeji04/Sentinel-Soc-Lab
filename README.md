# Azure Sentinel SOC Lab

Microsoft Sentinel mini-lab for entry-level SOC / cybersecurity portfolio work.

This lab deploys a small Azure environment that:

1. Ingests Windows Security events into Log Analytics
2. Enables Microsoft Sentinel
3. Creates analytics rules for failed logons (**Event ID 4625**) and account lockouts (**Event ID 4740**)
4. Investigates a triggered incident and documents a short SOC-style runbook

**Scope:** Student Azure lab using a small Windows VM. Not a production SOC deployment.

## Environment

| Item | Value |
|---|---|
| Cloud | Microsoft Azure (student subscription) |
| Log source | Azure Windows VM + Azure Monitor Agent |
| SIEM | Microsoft Sentinel |
| Resource group | `rg-sentinel-soc-lab` |

## Architecture

```text
Windows Lab VM
  → Azure Monitor Agent / Data Collection Rule
    → Log Analytics Workspace
      → Microsoft Sentinel
        → Analytics rules (4625, 4740)
          → Incident → investigation notes
```

## Detections

| Rule | Event ID | Purpose |
|---|---|---|
| Failed logon burst | 4625 | Detect repeated failed authentications |
| Account lockout | 4740 | Detect account lockout events |

Query drafts: [`queries/`](queries/)  
Rule notes: [`detections/`](detections/)

## Evidence

Screenshots and proof live in [`Evidence/`](Evidence/). See [`Evidence/README.md`](Evidence/README.md) for status.

| Area | Status |
|---|---|
| Configuration | Pending |
| Detection | Pending |
| Investigation | Pending |

## Docs

- [Architecture](docs/architecture.md)
- [Setup guide](docs/setup-guide.md)
- [Incident runbook](docs/incident-runbook.md)

## Related projects

- [Enterprise Security Controls](https://github.com/TamiDeji04/Enterprise-Security-Controls) — Windows lockout policy + 4625/4740 evidence
- [Splunk SOC Detection Lab](https://github.com/TamiDeji04/Splunk-SOC-Detection-Lab) — Splunk/Sysmon detection practice

## Disclaimer

Educational lab only. Do not commit passwords, tenant secrets, or production data. Shut down the lab VM when idle and delete the resource group when finished documenting.
