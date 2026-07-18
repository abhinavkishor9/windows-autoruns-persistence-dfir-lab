# Investigation Timeline

| Time | Activity | Evidence |
|------|----------|----------|
| 06:21 | Created AutorunsLab working directory | PowerShell |
| 06:22 | Added DemoAutorun registry Run key | reg add |
| 06:23 | Queried HKCU Run registry key | reg query |
| 06:24 | Verified DemoAutorun persistence entry | Registry Output |
| 06:25 | Checked Startup Folder | Startup Folder Empty |
| 06:26 | Reviewed Task Manager Startup Applications | Task Manager |
| 06:27 | Deleted DemoAutorun registry value | reg delete |
| 06:28 | Confirmed registry entry removed | reg query |

---

# Investigation Summary

Initial Finding

↓

Registry Run key added

↓

Persistence confirmed

↓

Startup Folder checked

↓

Task Manager reviewed

↓

Persistence removed

↓

Registry cleaned

↓

Investigation complete

---

# Key DFIR Timeline

Persistence Created
↓

Registry Modified

↓

Persistence Verified

↓

Additional Autorun Locations Reviewed

↓

Persistence Removed

↓

System Returned to Baseline
