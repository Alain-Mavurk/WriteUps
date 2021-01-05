# Legacy



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

First, i start with nmap scanning:

![](img/nmap.png) 



Here, we have a **Windows XP** which use **smb** service. I start **metasploit** to scan the smb version using `scanner/smb/smb_version` module:

![](img/smb_version.png)  



I got some informations and i start to search on google `Windows XP SP3 exploit`. I found an exploit from **Rapid7** website in first result:

![](img/rapid7.png)  



## Exploitation

I set the previous exploit on my **metasploit**, set all options and run. After that, i got a meterpreter and on top of that, i had the highest privilege on windows which is `nt authority\system`:

![](img/exploit.png) 



## Post-exploitation

As i had the highest privilege, i could get all users flag. So, i listed users and got it:

 ![](img/users.png)



### User

![](img/own_user.png) 



### Root

![](img/own_root.png) 



## Mitigation

To avoid the `ms08_067` exploit, it is recommended to upgrade and patch the system.