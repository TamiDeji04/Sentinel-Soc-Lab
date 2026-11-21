# Setup Guide

This is how I built the lab in Azure. If you’re following along, use your student subscription and stick to one allowed region the whole time. Mine ended up in **North Central US**.

## 1. Resource group

I created a resource group so everything for this lab stayed in one place.

1. Create resource group: `rg-sentinel-soc-lab` (I also ended up with `nrg-sentinel-soc-lab` during retries)
2. Pick one region and reuse it for every resource
3. Screenshot → `Evidence/Configuration/01-resource-group.png`

## 2. Log Analytics + Sentinel

I needed a place for logs to land before Sentinel could do anything useful.

1. Create a Log Analytics workspace (`law-sentinel-soc-lab`)
2. Open **Microsoft Sentinel** → connect that workspace
3. Make sure Sentinel opens cleanly on it
4. Screenshot → `Evidence/Configuration/02-sentinel-overview.png`

## 3. Windows VM

I used a small Windows VM as the machine that would generate Security events.

1. Create a small Windows VM (B-series if you can)
2. Name I used: `vm-sentinel-lab`
3. Use a strong admin password and keep it out of GitHub
4. Screenshot → `Evidence/Configuration/03-windows-vm.png`

Student tip: if deploy fails with a region policy error, switch to a region your subscription actually allows.

## 4. AMA + Security Events collection

Heartbeat alone isn’t enough. I had to explicitly collect Windows Security events.

1. Make sure **Azure Monitor Agent** is on the VM
2. Create / configure a **Data Collection Rule** for Windows Security events  
   (I used the **Windows Security Events via AMA** connector and named my rule `dcr-soc-ab`)
3. Point it at `vm-sentinel-lab` and `law-sentinel-soc-lab`
4. Wait a bit — first events can take several minutes
5. Screenshot → `Evidence/Configuration/04-data-collection-rule.png`

## 5. Validate ingestion

I ran this in Sentinel **Logs** until I saw real rows from my VM:

```kusto
SecurityEvent
| where TimeGenerated > ago(1h)
| summarize count() by EventID
| sort by count_ desc
```

And this to focus on failed logons:

```kusto
SecurityEvent
| where EventID == 4625
| take 20
```

Screenshot → `Evidence/Configuration/05-securityevent-query.png`

## 6. Create analytics rules

I created two scheduled rules:

- [`detections/failed-logons-4625.md`](../detections/failed-logons-4625.md)
- [`detections/account-lockout-4740.md`](../detections/account-lockout-4740.md)

Screenshots go in `Evidence/Detection/`.

## 7. Generate test activity

On the VM sign-in screen I intentionally failed logons a few times so the 4625 rule had something real to fire on. If lockout is enabled, that can also produce 4740.

Then I checked:

1. Events in `SecurityEvent`
2. Incidents created by my rules

## 8. Investigate

1. Open the incident
2. Grab screenshots
3. Walk through [`incident-runbook.md`](incident-runbook.md)
4. Save proof under `Evidence/Investigation/`

## Cleanup

When I’m done documenting:

1. Stop/deallocate the VM
2. Delete the lab resource group if I don’t need it anymore
