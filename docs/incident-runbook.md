# Incident Runbook — Failed Logons / Account Lockout

This is the checklist I use when one of my lab rules fires for **4625** or **4740**.

## 1. Triage (a couple minutes)

- [ ] Open the incident and note the rule name + severity
- [ ] Check the time range and which account/host got hit
- [ ] Ask myself: was this me testing, or unexpected noise?

Questions I ask:

1. Which account was targeted?
2. What host did it come from?
3. How many failures happened in the window?
4. Did a lockout (4740) show up after the failures?

## 2. True positive vs noise

| What I see | I’m leaning true positive | I’m leaning lab noise / FP |
|---|---|---|
| Burst of 4625 | Someone / something hammering passwords | One typo, or me testing |
| 4740 after failures | Lockout actually kicked in | Me intentionally locking a test account |
| Known lab account | Expected during the exercise | Still worth writing down |

## 3. What I check next

1. Pull recent 4625/4740 events with my queries in [`queries/`](../queries/)
2. See if the account is locked
3. Note whether I had to unlock it
4. Save screenshots in `Evidence/Investigation/`

## 4. Lab response

- Add a short note on the incident
- Unlock the test account only if I need it again
- Reminder: this lab has no production users

One note I used:

> Lab test: intentional failed logons against a local account to validate the Failed Logons 4625 rule and incident workflow.

## 5. Closeout

- [ ] I wrote incident notes
- [ ] Screenshots are saved
- [ ] The rule behaved the way I expected
- [ ] README / evidence index is updated

## Investigation log

| Field | Value |
|---|---|
| Date | 2026-11-21 |
| Rule name | Lab - Failed Logons 4625 |
| Host | vm-sentinel-lab |
| Event IDs observed | 4625 (primary); 4740 rule created |
| Outcome | Lab true positive / expected test activity |
| Notes | Incidents created successfully after failed logon activity. Public RDP also attracted extra spray noise, so I’d restrict access next time. |
