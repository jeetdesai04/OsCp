# Methodology/Checklist

- shell spawning

```
https://netsec.ws/?p=337
python -c 'import pty; pty.spawn("/bin/bash")'

CTRL+Z
stty raw -echo
fg
```

### SMB

```
$ nmap -v -p 139,445 -oG smb.txt 10.11.1.5    # initial scan for smb, output greppable format

$ sudo nbtscan -r <ip>  # specialized tool for NetBIOS Information

$ nmap --script smb-vuln* -p 139,445 <ip>   # check for vulns

$ enum4linux -a <ip>    # overall scan

$ smbmap -H <ip/hostname>   # command will show shares on host

$ smbmap -H <ip> -d <domain> -u <user> -p <password>

$ smbclient -L \\<ip>

$ echo exit | smbclient -L \\\\<ip>   # exit will take care of any password popups

$ smbclient \\\\<ip>\\<share name>    # attempt to connect to the share

####################################
FOR SAMBA: (grab the version number)
####################################

ERROR: protocol negotiation failed: NT_STATUS_CONNECTION_DISCONNECTED

DO:
/etc/samba/smb.conf and add one line to the global section:
client min protocol = LANMAN1

1st console: sudo ngrep -i -d tun0 's.?a.?m.?b.?a.*[[:digit:]]' port 139
2nd console: echo exit | smbclient -L [Target IP]

github script which does something similar (MAKE SURE TO CHANGE IPS AND TUN0): https://github.com/rewardone/OSCPRepo/blob/master/scripts/recon_enum/smbver.sh

```

### MySQL - SQL injection

- connect to sql database

```
$ sqsh -S <server ip> -U <username> -P <password>
```

- General SQL cheatsheets

```
https://www.exploit-db.com/papers/12975

https://bhanusnotes.blogspot.com/2019/09/sql-injection-cheat-sheet.html

```

- error based SQL cheatsheet

```
https://perspectiverisk.com/mssql-practical-injection-cheat-sheet/
```


### POP

```

$ nc -nv <IP> 110    # banner grabbing

$ telnet <IP> 110   # connect/banner grabbing

USER <user>
PASS <pass>


```

### Active directory

```
C:> net user
C:> net user /domain     ----> will enumerate all users in domain
C:> net user <user> /domain

C:> net group /domain    ----> enumerate all groups in domain

(use net.exe to lookup users and groups in domain)

LDAP://HostName[:PortNumber][/DistinguishedName]  ----> LDAP provider path format

PS C:> [System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain()   ----> retrives the domain object for current user logged in



```