# Troubleshooting Notes

## Lab
Windows Autoruns Persistence Investigation

---

## Issue 1 — Registry Value Not Visible

### Problem

After creating the persistence entry, the registry key did not appear immediately.

### Cause

The registry path was queried before the value was successfully written.

### Resolution

Re-run:

```cmd
reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Run
```

Verify that the newly created value appears.

---

## Issue 2 — Startup Folder Empty

### Observation

The Startup folder contained no files.

### Explanation

This is expected.

Persistence can exist through multiple autorun mechanisms:

- Registry Run Keys
- Startup Folder
- Scheduled Tasks
- Services
- Winlogon
- WMI

An empty Startup folder does not indicate the system is clean.

---

## Issue 3 — Task Manager Shows Only Legitimate Startup Items

### Observation

Task Manager Startup tab did not show DemoAutorun.

### Explanation

Task Manager only displays supported startup applications.

Registry entries pointing directly to simple executables such as:

```
notepad.exe
```

may not always appear.

Professional investigations should rely on:

- Registry inspection
- Autoruns utility
- DFIR artifacts

instead of Task Manager alone.

---

## Issue 4 — Registry Entry Still Exists After Reboot

### Explanation

Registry Run persistence survives reboot.

This behavior is expected.

Investigators should determine:

- Who created it
- When it appeared
- What executable it launches

rather than assuming persistence is malicious.

---

## Issue 5 — Unable to Delete Registry Entry

### Cause

Incorrect registry path or value name.

### Resolution

Delete using:

```cmd
reg delete HKCU\Software\Microsoft\Windows\CurrentVersion\Run /v DemoAutorun /f
```

Verify removal:

```cmd
reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Run
```

---

# Lessons Learned

✔ Registry Run Keys are one of the most common Windows persistence mechanisms.

✔ Startup Folder inspection alone is insufficient.

✔ Always validate persistence using multiple artifact sources.

✔ Legitimate software and malware often use identical persistence locations.

✔ DFIR investigations should focus on context rather than simply identifying autorun entries.
