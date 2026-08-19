
# Case 02 Investigation

## Summary

Explain:
- What type of attack occurred?
- Which account appears to have been compromised?
- What happened after access?


## Evidence

At approximately 09:41, following multiple failed authentication attempts consistent with password spraying, the `helpdesk` account was successfully accessed from the suspicious source IP. Immediately afterward, several discovery commands were executed to identify the current account and system, enumerate local users and administrators, and examine user directories.

This behavior increases confidence that the successful authentication represents an account compromise rather than normal user activity.

### Attack Timeline

- Failed authentication attempts against multiple accounts
- Successful `helpdesk` authentication at 09:41:31
- `whoami`
- `hostname`
- `net user`
- `net localgroup administrators`
- `Get-ChildItem C:\Users`

## Threat Intelligence

The suspicious source IP `45.83.64.17` was investigated using VirusTotal.

- VirusTotal detections: 1/91
- Country: Germany
- ASN: AS208843
- Organization: Alpha Strike Labs GmbH
- Community score: -13

Although only one security vendor flagged the IP, the low detection count does not rule out malicious activity. The authentication and process logs provide additional evidence of suspicious behavior associated with the IP.

## MITRE ATT&CK Mapping
- T1110.003 - Password Spraying
- T1087.001 - Account Discovery: Local Account
- T1069.001 - Permission Groups Discovery: Local Groups
- T1083 - File and Directory Discovery

## Severity

**High**
The incident was classified as High severity because the `helpdesk` account was successfully accessed following authentication attempts consistent with password spraying. After gaining access, the account immediately performed system, account, group, and directory discovery.

Although the evidence indicates a likely account compromise, no privilege escalation, persistence, malware execution, data exfiltration, or destructive activity was identified in the available logs.

## Recommended Response

- Isolate `WS-120` from the network to contain potential unauthorized activity.
- Disable or secure the compromised `helpdesk` account according to the organization's incident response procedures.
- Reset the password for the `helpdesk` account.
- Terminate existing sessions associated with the compromised account.
- Review authentication logs to determine whether the `helpdesk` credentials were used on other systems.
- Investigate the other accounts targeted during the suspected password-spraying activity for additional successful authentications.
- Preserve relevant authentication and process logs for further investigation.
- Block or monitor `45.83.64.17` where appropriate.
- Implement or enforce multi-factor authentication (MFA), particularly for remote and privileged access.

## Conclusion

The investigation identified activity consistent with a password-spraying attack that resulted in likely compromise of the `helpdesk` account on `WS-120`. Following the successful authentication, the account performed multiple discovery activities involving the system, local accounts, administrator group membership, and user directories.

The incident should be contained and further investigated to determine the full scope of the compromise and whether additional systems or accounts were affected.
