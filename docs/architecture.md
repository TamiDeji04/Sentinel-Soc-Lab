# Architecture

## What I set up

I kept everything inside one Azure lab footprint:

- A small Windows VM as my log source
- A Log Analytics workspace to store and query the logs
- Microsoft Sentinel on top of that workspace
- A Data Collection Rule so Azure Monitor Agent could ship Windows Security events

## How data moves

```text
1. I generate failed logons (or a lockout) on the VM
2. Windows writes those events to the Security log
3. Azure Monitor Agent picks them up through my DCR
4. They show up in Log Analytics as SecurityEvent rows
5. My Sentinel analytics rules run on a schedule
6. Matching activity creates an incident I can investigate
```

## Components I used

| Piece | Name | What it’s for |
|---|---|---|
| Resource group | `rg-sentinel-soc-lab` / `nrg-sentinel-soc-lab` | Keeps the lab resources together |
| Windows VM | `vm-sentinel-lab` | Where the Security events come from |
| Log Analytics | `law-sentinel-soc-lab` | Where I query the logs |
| Sentinel | Enabled on that workspace | Detections + incidents |
| DCR / AMA | `dcr-soc-ab` + Azure Monitor Agent | The shipping path |

## Things I kept in mind

- This is a student lab, not production identity work
- I used the VM mainly as a controlled place to generate and collect Security events
- I tried to keep cost down: small VM size, stop it when I’m idle, and delete the resource group when I’m fully done
