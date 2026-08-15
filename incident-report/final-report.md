# Security Incident Report

## Incident Overview

**Incident Type:** Suspected Privileged Account Compromise  
**Affected System:** SRV-01  
**Affected Account:** admin  
**Severity:** Critical  
**Date:** August 10, 2026  

## Executive Summary

Analysis of Windows authentication and endpoint activity identified a likely compromise of the `admin` account on SRV-01.

Five failed authentication attempts from the external IP address `185.220.101.44` were followed by a successful login from the same source.

Following authentication, the account performed several system discovery activities, created a new privileged local account, and cleared the Windows Security audit log.

The sequence of events is consistent with unauthorized access followed by discovery, persistence, and defense evasion activity.

## Evidence

### Authentication Activity

Between 09:04:17 and 09:04:37, five failed authentication attempts targeted the `admin` account from `185.220.101.44`.

At 09:04:44, the same source IP successfully authenticated to the `admin` account.

Threat intelligence research identified the source IP as Tor-associated, with multiple security vendors on VirusTotal flagging the address as malicious.

### System Discovery

Following the successful authentication, the `admin` account executed:

- `whoami`
- `ipconfig /all`
- `net user`
- `netstat -ano`
- `Get-Process`

These commands collected information about the current user, network configuration, local accounts, network connections, and running processes.

### Persistence

At 09:08:14, the `admin` account created a new local account:

`svc_backup`

At 09:08:42, `svc_backup` was added to the local Administrators group.

This activity may indicate an attempt to establish persistent privileged access to SRV-01.

### Defense Evasion

At 09:09:31, Windows Security Event ID 1102 indicated that the Security audit log was cleared.

Given the preceding suspicious activity, this may represent an attempt to remove evidence and hinder investigation.

## MITRE ATT&CK Mapping

| Technique ID | Technique |
| --- | --- |
| T1110.001 | Password Guessing |
| T1033 | System Owner/User Discovery |
| T1016 | System Network Configuration Discovery |
| T1087.001 | Account Discovery: Local Account |
| T1057 | Process Discovery |
| T1136.001 | Create Account: Local Account |
| T1070.001 | Clear Windows Event Logs |

## Severity Assessment

**Severity: Critical**

The incident was classified as Critical due to evidence of likely privileged account compromise, post-authentication discovery activity, creation of an additional privileged account, and clearing of security audit logs.

The attacker may retain administrative access to SRV-01 through the newly created account.

## Recommended Response

1. Escalate the incident according to the organization's incident response procedure.
2. Isolate SRV-01 from the network while preserving necessary forensic evidence.
3. Disable or contain the suspicious `svc_backup` account according to the incident response playbook.
4. Secure the compromised `admin` account and terminate unauthorized sessions.
5. Block or monitor the identified source IP where appropriate.
6. Preserve available authentication, endpoint, network, and security logs.
7. Investigate SRV-01 for additional persistence mechanisms or malicious activity.
8. Determine whether the compromised credentials were used against additional systems.
9. Recover the affected system according to organizational procedures after containment and eradication.

## Conclusion

The investigation identified a likely privileged account compromise involving the `admin` account on SRV-01.

Authentication evidence combined with subsequent discovery, persistence, and defense evasion activity provides strong evidence that the successful login was unauthorized.

Immediate escalation, containment, further investigation, and credential remediation are recommended.
