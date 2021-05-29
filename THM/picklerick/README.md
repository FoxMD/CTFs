# Machine

IP: `10.10.0.26`

---

# NMAP:

- 22 - OpenSSH 7.2p2 Ubuntu 4ubuntu2.6
- 80 - Apache httpd 2.4.18 ((Ubuntu))

---
## Web
### Source code 
- Username: `R1ckRul3s`

---
### Dirbuster
run dirbuster -> output:
- /index.html
- /login.php
- /assets
- /portal.php
- robots.txt - `Wubbalubbadubdub`

### /portal.php:
- id: `R1ckRul3s`
- pwd: `Wubbalubbadubdub`

found: `Sup3rS3cretPickl3Ingred.txt` - `mr. meeseek hair`

--- 
portal.php reverse shell py3

---
## Deployed RS
in folder `rick`: 
drwxrwxrwx 2 root root 4096 Feb 10  2019 .
drwxr-xr-x 4 root root 4096 Feb 10  2019 ..
-rwxrwxrwx 1 root root   13 Feb 10  2019 second ingredients
root@ip-10-10-0-26:/home/rick# `cat "second ingredients"`

- found cat: `1 jerry tear`
---

in folder `root: 3rd.txt`
- found cat: 3rd ingredients: `fleeb juice`

# Done
