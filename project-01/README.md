
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


## Investigation Results

### Objective
Identify repeated failed authentication attempts that may indicate password guessing or other suspicious login activity.

### Data and Method
- Dataset: `sample_auth_logs.csv`
- Dataset type: Fictional authentication events
- Analysis tool: Python with pandas, in a Kaggle notebook
- Detection threshold: Three or more failed logins for the same username and source IP

### Findings

| Username | Source IP | Failed attempts |
|---|---|---:|
| bob | 198.51.100.24 | 4 |
| alice | 203.0.113.55 | 2 |
| david | 192.0.2.77 | 1 |

Only Bob met the detection threshold.

### Key Observation
Bob had four failed login attempts followed by a successful login at 09:02:02 UTC. The first failure occurred at 09:01:05 UTC, so the successful login followed 57 seconds later.

### Analyst Assessment
This pattern warrants further investigation because repeated failures followed by a success can be consistent with password guessing. The available events do not prove that the account was compromised.

### Recommended Response
1. Review additional authentication events around the suspicious activity.
2. Verify whether the source IP, device and login context are expected.
3. Review MFA results and identity-provider risk signals.
4. Escalate according to the organisation's incident response process if further evidence supports compromise.

### Validation and Limitations
The detection logic was tested in Python against the fictional sample data. The expected result was one flagged username/IP pair: Bob, with four failures.

The KQL query is saved in `failed_login_detection.kql`, but it has not yet been executed in Microsoft Sentinel. The Python test validates the detection logic; it is not a SIEM execution.

The dataset is small and synthetic, so these results do not establish real-world malicious activity.

### Evidence
See `failed-login-test.png` for the Python test output.

