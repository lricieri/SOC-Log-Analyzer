# SOC Log Analyzer

A Level 1 triage tool for authentication logs, simulating the first
checks a SOC (Security Operations Center) analyst runs when
investigating suspicious access alerts.

## What it detects

| Pattern | Severity | Description |
|---|---|---|
| Brute force | High | Many failed login attempts from the same IP |
| Password spraying | High | The same IP attempting login against several different users |
| Off-hours login | Medium | Successful login outside business hours (10pm-6am) |
| Success after failures | Critical | Successful login right after a streak of failures - possible sign of a compromised credential |

## How to run

```bash
python analyzer.py logs/auth_sample.csv
```

The input log file is a simple CSV, formatted as:

```csv
timestamp,ip,usuario,status
2026-09-09 14:02:10,203.0.113.55,admin,fail
```

## Example output

```bash
Events analyzed: 19
Alerts generated: 6

[CRITICAL] success_after_failures — IP 192.0.2.77
login by 'carlos.pereira' succeeded after 3 consecutive failures

[HIGH] brute_force — IP 203.0.113.55
6 failed login attempts
```

## Motivation

This project simulates the first stage of a SOC analyst's job: turning a
raw log into a severity-ranked list of alerts, ready for triage and
escalation - the same workflow described in security monitoring roles
(SIEM, alert triage, initial incident response).

## Next steps

- [ ] Read real syslog/auth.log files directly
- [ ] Add IP geolocation to detect "impossible travel"
- [ ] Export alerts as JSON for integration with other tools

## Tech stack

- Python 3 (standard library only - no external dependencies)
