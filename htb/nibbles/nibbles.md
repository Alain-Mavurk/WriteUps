# Nibbles



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

![](img/about_box.png) 



## Profile

[![Akinflo](http://www.hackthebox.eu/badge/image/419539)](https://www.hackthebox.eu/home/users/profile/419539)



## Enumeration

First, nmap scanning:

![](img/nmap.png) 



I went to the webpage and it just printed **"hello world"**, i looked at the source page and i found an interesting comment:

![](img/source_code.png) 

I added this directory to the url and a blog appeared. I decided to enumerate this directory with **gobuster** to get more information:

```bash
 gobuster -o gobuster_res dir -u http://10.10.10.75 -w /usr/share/seclists/Discovery/Web-Content/common.txt
```

![](img/gobuster.png) 



The `/admin` page allowed directory listing:

![](img/admin_directory_listing.png)   

But i found nothing interesting here. I went to the `/admin.php` file and an authentication was required. After brute forcing, i didn't find valid credentials and i was banned temporarily, so i stopped to brute force.

  

## Exploitation

When i was  reading the `README` file, i found that the version of `nibbleblog` installed is 4.0.3:

![](img/nibbleblog_version.png) 

I used **searchsploit** to see if vulnerabilities exist on this version and it does:

 ![](img/searchsploit.png) 

A remote code execution is possible on this version but we need to get authenticated.

As brute forcing was not the solution, i thought that there was hint for the admin password. The box name is **Nibbles** and in the main blog page, the title is the same thing, so i tried `admin:nibbles` credentials and it worked:

![](img/logged_admin.png)

 



## Post-exploitation

### User

I started **metasploit** and search the exploit module: `exploit/multi/http/nibbleblog_file_upload`

 ![](img/nibbleblog_search_metasploit.png) 

After setting all options, i did run the exploit and got the meterpreter:

![](img/get_meterpreter.png) 



I got the user flag:

![](img/own_user.png) 



### Root

First, i used the following command to list all root privileges command the user can do:

 ```bash
sudo -l
 ```

  

![](img/sudo_list.png) 



Here, i can use the `sudo` privilege on `home/nibbler/personal/stuff/monitor.sh`.

The directory is in zip format:

![](img/user_home.png) 

 But i didn't unzip it, i had the idea to create my own script with the same path. As the script is run with `sudo`, the command executed in the script has root privileges. So, i create the directories with:

```bash
mkdir -p personal/stuff
```

I go to the stuff directory and create the `monitor.sh` file with just a interactive bash command:

![](img/script_edit.png) 

I made it executable with:

```bash
chmod +x monitor.sh
```

And i execute the the script. We got the interactive bash shell with root:

![](img/own_root.png) 



## Mitigation