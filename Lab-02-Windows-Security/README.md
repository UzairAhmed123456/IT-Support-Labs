# Lab 02 — Windows Defender & Firewall Verification

## Objective

Inspect and verify Windows 11 security settings using the Windows Security application and PowerShell. Identify potential security configuration issues, document findings, and practice basic endpoint security troubleshooting.

## Environment

- Operating System: Windows 11
- Tools: Windows Security, Windows PowerShell
- Lab Date: November 5, 2026
- Lab Type: Endpoint security configuration and verification

## Part 1 — Windows Security Inspection

Opened Windows Security and reviewed the security dashboard.

### Findings

- App & browser control displayed a yellow warning.
- The initial warning indicated that potentially unwanted app (PUA) blocking was disabled.
- Enabled PUA blocking and verified reputation-based protection settings.
- Confirmed SmartScreen and phishing protection settings were enabled.
- Enabled warnings for password reuse and unsafe password storage.

**Result:** Individual reputation-based protection settings appeared enabled, but the main dashboard continued displaying a yellow warning. The cause remains unresolved.

## Part 2 — Microsoft Defender Antivirus

Verified the following settings:

| Setting | Status |
|---|---|
| Real-time protection | On |
| Cloud-delivered protection | On |
| Automatic sample submission | On |
| Tamper Protection | On |

**Result:** All four inspected protection settings were enabled.

## Part 3 — Windows Firewall

Inspected the Domain, Private, and Public firewall profiles.

| Network Profile | Firewall Status |
|---|---|
| Domain | Enabled |
| Private | Enabled |
| Public | Enabled — Active profile |

The Public network profile was active during testing. No firewall settings were changed.

## Part 4 — PowerShell Firewall Verification

Executed the following command:

```powershell
Get-NetFirewallProfile | Select-Object Name, Enabled, DefaultInboundAction, DefaultOutboundAction
```

### Findings

- All three firewall profiles returned `Enabled = True`.
- DefaultInboundAction and DefaultOutboundAction returned `NotConfigured` for all three profiles.
- These values indicate that no explicit action was configured in those properties; they do not establish that firewall traffic is unrestricted.

## Part 5 — PowerShell Defender Verification

Executed the following command:

```powershell
Get-MpComputerStatus | Select-Object AntivirusEnabled, RealTimeProtectionEnabled, BehaviorMonitorEnabled, IoavProtectionEnabled, AntivirusSignatureLastUpdated
```

### Findings

| Property | Result |
|---|---|
| AntivirusEnabled | True |
| RealTimeProtectionEnabled | True |
| BehaviorMonitorEnabled | True |
| IoavProtectionEnabled | True |
| AntivirusSignatureLastUpdated | November 5, 2026, 5:45:11 AM |

**Result:** The inspected Defender protections were enabled, and the reported antivirus signature update timestamp was from the morning of the lab.

## Troubleshooting Experience

Initially attempted to execute a PowerShell cmdlet in Command Prompt, which returned a command-not-recognized error.

Resolved this by launching PowerShell from Command Prompt using:

```cmd
powershell
```

The firewall verification command then executed successfully.

## Skills Practiced

- Windows 11 endpoint security inspection
- Microsoft Defender Antivirus configuration verification
- Windows Firewall profile inspection
- PowerShell security diagnostics
- Identifying and documenting security warnings
- Technical troubleshooting and documentation

## Conclusion

Completed a read-only security verification using Windows Security and PowerShell, with one configuration change to enable recommended reputation-based protections.

Verified that Microsoft Defender Antivirus and all three Windows Firewall profiles were enabled.

The remaining App & browser control dashboard warning requires further investigation. No evidence was found during these checks that the verified antivirus or firewall protections were disabled.
