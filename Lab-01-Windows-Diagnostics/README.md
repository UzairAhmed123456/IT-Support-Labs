# Lab 01 — Windows 11 System Diagnostics

## Objective
Practice entry-level IT support troubleshooting by examining Windows 11 system performance, reviewing system event logs, and investigating a BitLocker error using built-in Windows diagnostic tools.

## Lab Environment
- **Computer:** MINISFORUM UM760S Mini PC
- **Operating System:** Windows 11
- **Processor:** AMD Ryzen 5 7640HS (6 cores, 12 logical processors)
- **Memory:** 16 GB DDR5 RAM
- **Storage:** Kingston NVMe SSD (approximately 954 GB)
- **Tools:** Windows Task Manager, Event Viewer, Windows PowerShell, BitLocker command-line utility

## 1. CPU Diagnostics

Opened Task Manager and navigated to Performance → CPU.

**Observations:**
- CPU utilization: approximately 6%
- CPU speed: 4.09 GHz
- 6 physical cores and 12 logical processors
- 183 running processes

**Finding:** No sustained CPU bottleneck was observed at the time of inspection.

## 2. Memory Diagnostics

Examined memory usage using Task Manager.

**Observations:**
- Installed RAM: 16 GB
- Usable RAM: 13.8 GB
- Memory in use: 7.7 GB (56%)
- Available memory: approximately 6.0 GB
- Hardware reserved: 2.2 GB

**Finding:** The system had available memory and showed no obvious memory pressure at the time of inspection.

## 3. Storage Diagnostics

Examined Disk 0 (C:) in Task Manager.

**Observations:**
- Storage device: Kingston NVMe SSD
- Capacity: approximately 954 GB
- Active time: 1%
- Average response time: 7.0 ms
- Read speed: 0 KB/s
- Write speed: 8.2 KB/s

**Finding:** No sustained disk activity bottleneck was observed in the captured performance snapshot. SSD health was not independently tested.

## 4. Windows Event Viewer Investigation

Opened Event Viewer → Windows Logs → System.

Identified the following error:

- **Source:** BitLocker-Driver
- **Event ID:** 24641
- **Severity:** Error
- **Message:** An unexpected error was encountered attempting to retrieve the BitLocker volume master key during restart.

Reviewed event history and identified:
- October 25, 2026: Three occurrences at approximately 5:42 PM
- October 28, 2026: Another occurrence

**Finding:** The error was recurring rather than a single isolated event.

## 5. BitLocker Verification

Opened Windows PowerShell as Administrator and executed:

`manage-bde -status C:`

**Results:**
- Conversion status: Used Space Only Encrypted
- Percentage encrypted: 100%
- Encryption method: XTS-AES 128
- Protection status: Protection On
- Lock status: Unlocked
- Key protectors: TPM and Numerical Password

**Finding:** The Windows system drive was encrypted, unlocked, and reporting active BitLocker protection despite the recorded errors.

## 6. Troubleshooting Conclusion

The investigation identified recurring BitLocker-Driver Event ID 24641 errors during the restart process.

However, the BitLocker status check confirmed that drive encryption was enabled and the operating system volume was accessible.

No evidence of a CPU, memory, or disk performance bottleneck was observed in the captured Task Manager readings.

The underlying cause of the BitLocker event remains undetermined. No configuration changes were made.

## 7. Recommended Follow-Up

- Monitor Event Viewer for additional BitLocker errors.
- Verify that the BitLocker recovery key is securely backed up.
- Investigate further if startup failures, recovery-key prompts, or additional BitLocker warnings occur.
- Avoid changing TPM, BIOS, or encryption settings without an appropriate backup and recovery plan.

## Skills Practiced

- Windows 11 system diagnostics
- CPU, RAM, and disk performance monitoring
- Windows Event Viewer log analysis
- PowerShell command-line diagnostics
- BitLocker status verification
- Troubleshooting documentation
- Evidence-based technical reporting

## Lab Outcome

Completed a read-only investigation of Windows 11 system performance and a recurring BitLocker error. Documented observations, verified the current encryption state, and identified safe follow-up actions without making unnecessary system changes.
## Screenshots and Supporting Evidence

### CPU Performance
![CPU performance](CPU%20performance.png)

### Memory Performance
![Memory performance](Memory%20performance.png)

### Disk Performance
![Disk performance](Disk%20performance.png)

### BitLocker Error — October 28
![BitLocker error](Bitlocker%20error%20code.png)

### BitLocker Error — October 25
![Previous BitLocker error](Previous%20Bitlocker%20error%20code.png)

### PowerShell BitLocker Status
![PowerShell BitLocker status](Powershell%20Bitlocker%20status.png)
