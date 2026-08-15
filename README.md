
# SOC Authentication Investigation Lab

## Overview

This project simulates a Security Operations Center (SOC) investigation of suspicious authentication activity on a Windows server.

The investigation began with repeated failed authentication attempts against a privileged account and followed the activity through successful authentication, system discovery, persistence, and defense evasion.

The goal of this project was to practice analyzing security logs, identifying suspicious behavior, using threat intelligence, mapping activity to MITRE ATT&CK, and documenting an incident.

## Scenario

A Windows server named `SRV-01` generated suspicious authentication activity involving the `admin` account.

The investigation identified:

- Multiple failed authentication attempts
- A subsequent successful authentication
- System and network discovery
- Local account enumeration
- Creation of a new privileged account
- Windows Security audit log clearing

## Tools & Technologies

- Windows Security Event Logs
- VirusTotal
- MITRE ATT&CK
- GitHub
- CSV log analysis
- Threat intelligence

## Skills Demonstrated

- SOC alert triage
- Log analysis
- Authentication analysis
- Threat intelligence research
- Incident timeline creation
- MITRE ATT&CK mapping
- Incident severity classification
- Incident response recommendations
- Technical documentation

## Key MITRE ATT&CK Techniques

| Technique | ID |
| --- | --- |
| Password Guessing | T1110.001 |
| System Owner/User Discovery | T1033 |
| System Network Configuration Discovery | T1016 |
| Account Discovery: Local Account | T1087.001 |
| Process Discovery | T1057 |
| Create Account: Local Account | T1136.001 |
| Clear Windows Event Logs | T1070.001 |

## Repository Structure

- `logs/` - Authentication, process, and security event datasets
- `investigation/` - Analyst findings and incident timeline
- `incident-report/` - Final security incident report

## Incident Assessment

The investigation identified evidence consistent with a likely compromise of a privileged account.

Following suspicious authentication activity, the account performed discovery, created an additional privileged local account, and cleared Windows Security audit logs.

The simulated incident was classified as **Critical** and would require immediate escalation and containment according to organizational incident response procedures.

## Disclaimer

This project uses simulated security data created for educational and portfolio purposes.
