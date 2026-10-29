
# Project 01: SOC Authentication Log Investigation

## About This Project

This project demonstrates practical Security Operations Centre (SOC) skills by analysing authentication logs, identifying suspicious login patterns, and documenting investigation findings.

## Objective

- Identify repeated failed login attempts.
- Investigate successful logins following multiple failures.
- Develop and validate detection logic.
- Assess suspicious activity and recommend appropriate response actions.

## Tools

- **GitHub:** Project documentation and version control
- **CSV:** Sample authentication event dataset
- **Python and pandas:** Initial detection logic validation
- **Kusto Query Language (KQL):** Detection query development
- **Microsoft Sentinel:** Planned SIEM implementation and testing

## Investigation Scenario

A SOC analyst receives authentication logs and must determine whether repeated failed login attempts, particularly those followed by a successful login, warrant further investigation.

The dataset contains fictional authentication events and uses documentation-only IP addresses.

## Investigation Methodology

1. Review the authentication events and their timestamps.
2. Filter for failed login attempts.
3. Group failures by username and source IP address.
4. Flag groups with three or more failed attempts.
5. Review whether successful logins follow the failed attempts.
6. Assess the evidence and recommend next steps.

## Investigation Findings

### Failed Login Summary

| Username | Source IP | Failed Attempts | Detection Outcome |
|---|---|---:|---|
| bob | 198.51.100.24 | 4 | Flagged |
| alice | 203.0.113.55 | 2 | Below threshold |
| david | 192.0.2.77 | 1 | Below threshold |

**Detection threshold:** Three or more failed login attempts for the same username and source IP.

Only Bob's activity met the detection threshold.

### Key Observation

Bob had four failed login attempts from `198.51.100.24`, followed by a successful login at `09:02:02 UTC`.

The first failure occurred at `09:01:05 UTC`, meaning the successful login occurred 57 seconds later.

This sequence may warrant investigation because it is consistent with a pattern such as password guessing followed by successful authentication. However, the available evidence does not establish that an attack occurred or that the account was compromised.

## Detection Logic

The KQL query is stored in [`failed_login_detection.kql`](failed_login_detection.kql).

The query filters failed login events, counts them by username and source IP, and returns groups with three or more failures.

The intended detection logic is:

- **Input:** Authentication events
- **Filter:** Failed login events
- **Grouping:** Username and source IP
- **Threshold:** Three or more failures
- **Expected result:** Bob, with four failed attempts

## Validation and Evidence

The detection logic was tested in a Kaggle notebook using Python and pandas against the fictional authentication data.

The test returned one matching username/IP pair: Bob, with four failed login attempts.

The test screenshot is available at [`failed-login-test.png`](failed-login-test.png).

**Validation status:**

- CSV analysis: Completed and verified.
- Python detection test: Completed.
- KQL query: Saved in the repository; not yet executed in a SIEM.
- Microsoft Sentinel ingestion and execution: Planned.

The Python test validates the intended detection logic but does not demonstrate execution in Microsoft Sentinel.

## Recommended Response

If this pattern appeared in a real environment, a SOC analyst should:

1. Review surrounding authentication events for the account and source IP.
2. Verify whether the source IP, device, location, and login context are expected.
3. Review multi-factor authentication (MFA) results and identity-provider risk signals.
4. Check for additional suspicious activity involving the account.
5. Escalate according to the organisation's incident response procedures if further evidence supports compromise.

Response actions should be proportionate to the evidence and the organisation's procedures.

## Limitations

- The dataset is small and fictional.
- The events do not include device information, MFA outcomes, or identity-provider risk signals.
- The threshold is a basic detection rule and may generate false positives.
- The analysis does not prove malicious activity or account compromise.
- Microsoft Sentinel testing remains outstanding.

## Disclaimer

This is an educational portfolio project using fictional authentication events and documentation-only IP addresses. No real credentials, confidential employer data, or production security logs are included.

## Next Steps

- Ingest the sample authentication events into a suitable SIEM lab.
- Execute and validate the detection query in Microsoft Sentinel.
- Capture the SIEM query results and document any differences.
- Refine the detection logic and record its limitations.
