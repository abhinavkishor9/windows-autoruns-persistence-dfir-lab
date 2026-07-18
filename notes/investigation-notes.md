# Investigation Notes – Windows Autoruns Persistence Investigation

## Lab Summary

This investigation demonstrates how Windows autorun registry keys can be abused to achieve persistence. A suspicious startup entry (`DemoAutorun`) is created under the current user's **Run** registry key, verified through Windows startup settings and registry inspection, and then removed during remediation. The exercise focuses on identifying persistence artifacts rather than malware execution.

---

## Analyst Methodology

The investigation followed a structured DFIR workflow:

1. Simulate a persistence mechanism using a Windows Run Registry key.
2. Enumerate autorun entries using native Windows utilities.
3. Validate the persistence artifact through multiple evidence sources.
4. Correlate registry configuration with Windows Startup applications.
5. Assess whether the persistence mechanism appears suspicious.
6. Remove the malicious registry value.
7. Verify successful remediation through post-investigation validation.

---

## Investigation Scenario

A workstation is suspected of maintaining persistence after a phishing incident. Although no malware is currently executing, investigators believe a registry-based startup mechanism was created to automatically launch a payload whenever the user logs in.

The objective is to determine:

- Whether a suspicious autorun entry exists.
- What executable it launches.
- Whether it is legitimate or malicious.
- Whether persistence has been successfully removed.

---

## Evidence Collected

### Evidence 1 – Registry Run Key

Registry Path:

```

HKCU\Software\Microsoft\Windows\CurrentVersion\Run

```

Observed Entry:

```

DemoAutorun REG_SZ notepad.exe

```

Finding:

- Startup entry created successfully.
- Launches Notepad at user logon.
- Demonstrates Registry Run Key persistence.

---

### Evidence 2 – Windows Startup Applications

Windows Startup Apps displayed:

- Microsoft Edge
- OneDrive
- Windows Security Notification
- VMware Tools
- Other legitimate applications

Finding:

- Startup applications were reviewed to distinguish legitimate autoruns from suspicious persistence.
- Registry inspection remains the authoritative evidence source for custom Run key entries.

---

### Evidence 3 – Registry Validation

Command:

```

reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Run

```

Finding:

- Confirmed DemoAutorun registry value.
- Verified executable configured for automatic execution.

---

### Evidence 4 – Remediation

Command:

```

reg delete HKCU\Software\Microsoft\Windows\CurrentVersion\Run /v DemoAutorun /f

```

Finding:

- Registry value removed successfully.

---

### Evidence 5 – Post-remediation Verification

Registry query performed again.

Finding:

- DemoAutorun no longer present.
- Only legitimate startup entries remained.

---

## DFIR Analysis

The persistence mechanism uses the **Run Registry Key**, one of the most common Windows persistence techniques.

Characteristics observed:

- User-level persistence
- Executes during interactive logon
- Requires no scheduled task or Windows service
- Frequently abused by malware families and loaders

Although Notepad was used as a harmless payload, the same persistence location is commonly used for:

- Remote Access Trojans (RATs)
- Infostealers
- Banking malware
- Ransomware loaders

---

## MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Persistence | Registry Run Keys / Startup Folder | T1547.001 |
| Defense Evasion | Modify Registry | T1112 |

---

## Analyst Observations

- The suspicious autorun entry was successfully created and immediately detectable through registry inspection.
- Native Windows utilities (`reg query`) provided sufficient visibility without requiring third-party forensic tools.
- Startup application review helped differentiate expected software from unusual persistence mechanisms.
- Removing the registry value immediately eliminated the persistence mechanism.
- Post-remediation validation confirmed that no malicious autorun entries remained.

---

## Conclusion

The investigation successfully demonstrated how Registry Run Keys provide persistence on Windows systems.

The simulated artifact was identified, validated, analyzed, removed, and verified using native forensic techniques.

Although the payload executed only Notepad, the investigation mirrors the same workflow analysts perform when investigating real-world malware persistence.
