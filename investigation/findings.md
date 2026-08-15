# SOC Authentication Investigation

## Investigation Summary

A review of Windows authentication logs identified suspicious login activity involving the `admin` account.

## Initial Findings

- Multiple failed login attempts targeted the `admin` account.
- Five failed authentication attempts occurred within approximately 30 seconds.
- The failed attempts originated from `185.220.101.44`.
- The same IP address successfully authenticated to the `admin` account shortly afterward.
- The source IP was external to the organization's private `10.0.0.0` network.

## Threat Intelligence

VirusTotal analysis of `185.220.101.44` showed:

- 16 of 91 security vendors flagged the IP as malicious.
- The IP was tagged as associated with Tor.
- Network: `185.220.101.0/24`
- ASN: `AS60729`
- Organization: Stiftung Erneuerbare Freiheit

## MITRE ATT&CK Mapping

- Technique: Brute Force
- Sub-technique: Password Guessing
- Technique ID: T1110.001
- Evidence: Five failed authentication attempts against the `admin` account were followed by a successful authentication from the same external IP address.
- Country associated with the network: Germany (DE)

## Current Assessment

The activity is consistent with a possible password-guessing or brute-force attack against the `admin` account. The successful authentication following multiple failures increases the likelihood that the account may have been compromised.

Further investigation is required before confirming a compromise.




## Post-Authentication Activity

Following the suspicious successful login to the `admin` account, several system discovery commands were executed on `SRV-01`.

- `whoami` - Identified the account associated with the current session.
- `ipconfig /all` - Collected network configuration information.
- `net user` - Enumerated user accounts on the system.
- `netstat -ano` - Displayed active network connections, listening ports, and process IDs.
- `Get-Process` - Enumerated running processes.

The timing and sequence of these commands following the suspicious authentication indicate possible system discovery activity.

## Additional MITRE ATT&CK Mapping

- T1033 - System Owner/User Discovery
- T1016 - System Network Configuration Discovery
- T1087.001 - Account Discovery: Local Account
- T1057 - Process Discovery
- 
