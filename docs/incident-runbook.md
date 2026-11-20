# Incident Runbook — Failed Logons / Account Lockout

Use this when Sentinel fires the lab analytics rules for Event ID **4625** or **4740**.

## 1. Triage (2–5 minutes)

- [ ] Open the incident and note severity, tactics, and rule name
- [ ] Confirm time range and affected account / host
- [ ] Check whether activity is expected lab testing or unexpected

**Questions**
1. Which account is targeted?
2. Source host / logon type (if present)?
3. How many failures in the window?
4. Did a lockout (4740) follow the failures?

## 2. Validate (true positive vs false positive)

| Signal | Likely true positive | Likely false positive / lab noise |
|---|---|---|
| Burst of 4625 | Repeated wrong-password attempts | Single typo, known test |
| 4740 after failures | Lockout policy working / brute force impact | Intentional lockout test |
| Known test account | Expected during lab exercise | Still document it |

## 3. Investigation steps

1. Query recent 4625/4740 events for the account/host ([queries](../queries/))
2. Review account status (locked / unlocked)
3. Note whether admin unlock was required
4. Capture screenshots for `Evidence/Investigation/`

## 4. Response actions (lab)

- Document findings in the incident
- Unlock test account only if needed for continued testing
- Do not disable production accounts (none in this lab)

## 5. Closeout

- [ ] Incident notes completed
- [ ] Evidence screenshots saved
- [ ] Rule behavior matches expected threshold
- [ ] README / Evidence index updated

## Investigation log (fill during lab)

| Field | Value |
|---|---|
| Date | |
| Rule name | |
| Incident ID | |
| Account | |
| Host | |
| Event IDs observed | |
| Outcome (TP/FP/lab test) | |
| Notes | |
