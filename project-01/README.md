
# Project 01: SOC Authentication Log Investigation

## About This Project
This project demonstrates practical Security Operations Centre (SOC) skills by analysing authentication logs and identifying potentially suspicious login activity.

## Objective
- Identify repeated failed login attempts.
- Investigate successful logins following multiple failures.
- Practise security log analysis and detection logic.
- Document findings and recommend response actions.

## Tools
- GitHub
- CSV authentication logs
- Kusto Query Language (KQL)
- Microsoft Sentinel (planned lab environment)

## Investigation Scenario
A SOC analyst receives authentication logs and must determine whether any login activity warrants further investigation.

## Investigation Steps
1. Review the available authentication events.
2. Group failed logins by username and source IP.
3. Identify repeated failures.
4. Check for successful logins following failures.
5. Assess the evidence and recommend next steps.

## Findings
To be completed after analysing the sample dataset.

## Recommendations
To be completed after the investigation.

## Disclaimer
This educational project uses fictional authentication events and documentation-only IP addresses. No real credentials or confidential employer data are included.

## Test Results

The sample CSV was analysed in Google Sheets.

| Username | Source IP | Failed login attempts |
|---|---|---:|
| bob | 198.51.100.24 | 4 |
| alice | 203.0.113.55 | 2 |
| david | 192.0.2.77 | 1 |

### Detection Outcome
Using a threshold of three or more failed logins per username and source IP, Bob's activity is flagged for further investigation.

### Analyst Assessment
Bob had four failed login attempts followed by a successful login. This is a suspicious pattern, but it does not prove an account compromise.

### Recommended Next Steps
- Review surrounding authentication events.
- Check whether the login device and location are expected.
- Review MFA and identity-provider risk events.
- Escalate if additional evidence supports compromise.

### Validation Notes
The CSV counts were verified in Google Sheets. The KQL query has been saved in this repository but has not yet been executed in a SIEM.

The dataset is fictional and uses documentation-only IP addresses.
