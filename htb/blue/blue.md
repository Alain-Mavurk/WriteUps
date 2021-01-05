# Blue



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



The first thing i do when i see the smb service available is to check vulnerability with `nmap --script`:

![](img/nmap_smb_vuln.png) 



Here, i found that it is vulnerable to `ms17-010` which refers to **eternalblue** (Box name was a hint).  



## Exploitation

So, i started **metasploit** and used the **eternalblue** module: `use exploit/windows/smb/ms17_010_eternalblue` 

I used the meterpreter payload to get a better shell: `windows/x64/meterpreter/reverse_tcp`

I got it with the highest privilege on windows which is `nt authority\system`:

![](img/exploit.png) 



## Post-exploitation

As i had the highest privilege, i could get all users flag. I listed users:

![](img/users.png) 



### User

![](img/own_user.png) 



### Root

![](img/own_root.png) 



## Mitigation

To avoid this vulnerability, it is recommended to upgrade the system in his latest version.