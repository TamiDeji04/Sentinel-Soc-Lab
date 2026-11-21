# Sentinel SOC Lab

I built this lab to get hands-on with **Microsoft Sentinel** the way a junior SOC analyst would: pull in Windows Security logs, write detections, and actually investigate an alert.

I used my Azure for Students subscription and kept the setup small on purpose. This is a learning lab, not a production SOC.

## What I did

1. Stood up a Log Analytics workspace and turned on Microsoft Sentinel
2. Deployed a Windows VM and shipped Security events with Azure Monitor Agent + a Data Collection Rule
3. Confirmed logs were landing in the `SecurityEvent` table
4. Created analytics rules for failed logons (**4625**) and account lockouts (**4740**)
5. Triggered failed logons, watched incidents show up, and documented how I’d triage them

## Environment

| Piece | What I used |
|---|---|
| Cloud | Azure for Students |
| Region | North Central US (the region my student sub allowed) |
| Resource group | `rg-sentinel-soc-lab` / `nrg-sentinel-soc-lab` |
| Workspace | `law-sentinel-soc-lab` |
| VM | `vm-sentinel-lab` |
| SIEM | Microsoft Sentinel |

## How the pieces fit together

```text
My Windows lab VM
  → Azure Monitor Agent / Data Collection Rule
    → Log Analytics workspace
      → Microsoft Sentinel
        → My analytics rules (4625, 4740)
          → Incidents I investigated
```

## Detections I wrote

| Rule | Event ID | Why I cared |
|---|---|---|
| Lab - Failed Logons 4625 | 4625 | Catch repeated failed sign-ins |
| Lab - Account Lockout 4740 | 4740 | Catch lockouts after those failures |

KQL lives in [`queries/`](queries/).  
Rule notes are in [`detections/`](detections/).

## Evidence

I saved screenshots under [`Evidence/`](Evidence/).  
Index: [`Evidence/README.md`](Evidence/README.md)

You’ll see the full path there: resource group → Sentinel → VM → DCR → log query → rules → incidents.

## Docs I wrote for myself (and anyone following along)

- [Architecture](docs/architecture.md)
- [Setup guide](docs/setup-guide.md)
- [Incident runbook](docs/incident-runbook.md)

## Related work

- [Enterprise Security Controls](https://github.com/TamiDeji04/Enterprise-Security-Controls) — I configured Windows account lockout and reviewed 4625/4740 on the endpoint side
- [Splunk SOC Detection Lab](https://github.com/TamiDeji04/Splunk-SOC-Detection-Lab) — similar detection practice in Splunk

## Honest notes

- Student lab only. No real production tenants or customer data.
- I don’t store passwords or secrets in this repo.
- Opening RDP to the internet got noisy fast (password spray traffic). I’d lock RDP down or shut the VM off when I’m not testing.
- When I’m done documenting, I stop/deallocate the VM so I don’t burn student credit.
