# windows-autoruns-persistence-dfir-lab

## Executive Summary

This DFIR lab demonstrates how Windows Registry Run Keys can be abused to establish persistence. A simulated autorun entry was created under the current user's **HKCU\Software\Microsoft\Windows\CurrentVersion\Run** registry key, analyzed using native Windows tools, mapped to the MITRE ATT&CK framework, and safely removed.

The investigation focuses on identifying persistence artifacts, validating their legitimacy, understanding their security implications, and documenting the complete forensic process.

---

# Overview

Persistence allows malware or unauthorized software to survive system reboots and automatically execute without user interaction.

One of the simplest and most common persistence mechanisms is the **Windows Registry Run Key**, where executables are configured to launch automatically whenever a user logs in.

During this investigation, a simulated registry persistence entry was created, validated, investigated, and removed while documenting all forensic evidence.

---

# Learning Objectives

- Understand Windows Autoruns persistence.
- Investigate Registry Run Key entries.
- Differentiate legitimate and suspicious startup entries.
- Perform persistence analysis using native Windows utilities.
- Map persistence techniques to MITRE ATT&CK.
- Document DFIR findings professionally.

---

# Skills Demonstrated

- Windows Registry Forensics
- Persistence Investigation
- Autoruns Analysis
- Registry Run Key Enumeration
- Windows Startup Analysis
- Evidence Collection
- DFIR Documentation
- MITRE ATT&CK Mapping
- IOC Identification
- Incident Reporting
- Native Windows Forensic Techniques

---

# Tools Used

- Windows 10 VM
- Registry Editor (regedit)
- Windows Command Prompt
- Windows PowerShell
- Task Manager (Startup Applications)
- File Explorer

---

# Lab Environment

| Component | Details |
|-----------|---------|
| Operating System | Windows 10 x64 |
| Virtualization | VMware Workstation Player |
| User Account | Local Standard User |
| Persistence Location | HKCU\Software\Microsoft\Windows\CurrentVersion\Run |
| Investigation Tools | Native Windows Utilities |
| Internet Required | No |

---

# Investigation Scenario

A SOC analyst receives an alert indicating that a workstation may contain unauthorized persistence.

The analyst suspects that a Registry Run Key has been modified to launch a program every time the user logs in.

The objective is to identify the persistence mechanism, validate its purpose, determine whether it is legitimate or suspicious, and safely remove the unauthorized autorun entry.

---

# Lab Workflow

1. Create a dedicated investigation folder.
2. Create a simulated Registry Run Key.
3. Verify registry persistence.
4. Review Startup Applications.
5. Investigate Startup folder.
6. Correlate persistence artifacts.
7. Remove the persistence entry.
8. Validate successful cleanup.
9. Document findings.

---

# MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Persistence | Registry Run Keys / Startup Folder | T1547.001 |
| Execution | User Logon | T1204 |
| Defense Evasion | Modify Registry | T1112 |

### Why T1547.001?

Windows automatically executes programs referenced under the Registry Run Keys whenever a user logs in. Attackers frequently abuse this mechanism because it provides simple and reliable persistence without requiring elevated privileges.

---

# Evidence Collected

- Registry Run Key before persistence creation
- Registry Run Key after persistence creation
- Registry value (DemoAutorun)
- Startup Applications screenshot
- Startup Folder inspection
- Registry cleanup verification
- Command outputs
- Removal confirmation

---

# Evidence Correlation

| Evidence | Observation | Investigation Value |
|----------|-------------|--------------------|
| Registry Run Key | DemoAutorun → notepad.exe | Persistence mechanism identified |
| Startup Applications | DemoAutorun visible | Confirms registry entry is active |
| Startup Folder | Empty | Rules out Startup Folder persistence |
| Registry after cleanup | DemoAutorun removed | Confirms successful remediation |
| Command output | Operation completed successfully | Verifies cleanup process |

Correlating multiple artifacts ensures the persistence originated from the Registry Run Key rather than another startup mechanism.

---

# Investigation Findings

- Persistence was created through the **HKCU Run Registry Key**.
- The autorun entry launched **notepad.exe** as a safe simulation.
- Startup Applications reflected the newly created persistence entry.
- No persistence artifacts were found in the Startup Folder.
- Registry cleanup successfully removed the persistence mechanism.
- Post-remediation verification confirmed the system returned to its expected state.

---

# Key Takeaways

- Registry Run Keys are one of the most common Windows persistence mechanisms.
- Startup Applications can quickly reveal active autorun entries.
- Registry persistence should always be correlated with Startup Folder analysis.
- Native Windows utilities are sufficient to perform basic persistence investigations.
- Persistence verification before and after remediation is essential during DFIR investigations.
- Proper documentation improves repeatability and incident reporting.

---
