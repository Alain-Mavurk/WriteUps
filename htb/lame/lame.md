# Lame



## Contents

- [**Box**](#Box)
- [**Profile**](#Profile)
- [**Enumeration**](#Enumeration)
- [**Exploitation**](#Exploitation)
- [**Post-exploitation**](#Post-exploitation)
  - [**User**](#User)
  - [**Root**](#Root)

- [**Mitigation**](#Mitigation)



## Box

![](img/box_info.png) 



## Profile

[![Akinflo](http://www.hackthebox.eu/badge/image/419539)](https://www.hackthebox.eu/home/users/profile/419539)



## Enumeration

First, nmap scanning:

![](img/nmap.png) 



There are several services used. I focused on the smb service and searched `Samba smbd 3.0.20-Debian exploit` on google and i got an **rce** exploit in this version from **rapid7** website: `'Username' map script' Command Execution`

![](img/rapid7.png) 



## Exploitation

I used the previous exploit in **metasploit**. After setting all options, i did run it and got a simple shell with root privileges:

![](img/exxploit.png) 



## Post-exploitation

After this, i had the highest privileges of the system so i could get users flag easily.



### User

![](img/own_user.png) 



### Root

![](img/own_root.png) 



## Mitigation

To avoid this exploit, it is recommended to upgrade and patch the system.