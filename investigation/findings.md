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
