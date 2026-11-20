# Setup Guide

Follow these steps in the Azure portal with your student subscription.

## 1. Resource group

1. Create resource group: `rg-sentinel-soc-lab`
2. Pick one region and stick to it
3. Screenshot → `Evidence/Configuration/01-resource-group.png`

## 2. Log Analytics + Sentinel

1. Create a Log Analytics workspace (example name: `law-sentinel-soc-lab`)
2. Open **Microsoft Sentinel** → **Add** → connect the workspace
3. Confirm Sentinel opens on the workspace
4. Screenshot → `Evidence/Configuration/02-sentinel-overview.png`

## 3. Windows VM

1. Create a small Windows VM (B1s/B2s if available)
2. Suggested name: `vm-sentinel-lab`
3. Use a strong admin password (do **not** store it in this repo)
4. Screenshot → `Evidence/Configuration/03-windows-vm.png`

## 4. AMA + Security Events collection

1. Install / enable **Azure Monitor Agent** on the VM
2. Create a **Data Collection Rule** that collects Windows **Security** events
3. Associate the DCR with the VM and the Log Analytics workspace
4. Wait for events to appear (can take several minutes)
5. Screenshot → `Evidence/Configuration/04-data-collection-rule.png`

## 5. Validate ingestion

In Sentinel / Log Analytics **Logs**, run:

```kusto
SecurityEvent
| where TimeGenerated > ago(1h)
| summarize count() by EventID
| sort by count_ desc
```

Then specifically:

```kusto
SecurityEvent
| where EventID == 4625
| take 20
```

Screenshot → `Evidence/Configuration/05-securityevent-query.png`

## 6. Create analytics rules

Use the notes in:

- [`detections/failed-logons-4625.md`](../detections/failed-logons-4625.md)
- [`detections/account-lockout-4740.md`](../detections/account-lockout-4740.md)

Save screenshots under `Evidence/Detection/`.

## 7. Generate test activity

On the VM sign-in screen (or via controlled local auth testing):

1. Attempt several failed logons against a test account
2. Optionally trigger lockout if local policy allows
3. Confirm events appear in `SecurityEvent`
4. Confirm analytics rules create incidents

## 8. Investigate

1. Open the incident in Sentinel
2. Capture timeline / entities / evidence
3. Fill [`incident-runbook.md`](incident-runbook.md)
4. Save screenshots under `Evidence/Investigation/`

## Cleanup

When documentation is done:

1. Stop/deallocate the VM
2. Delete `rg-sentinel-soc-lab` if you no longer need it
