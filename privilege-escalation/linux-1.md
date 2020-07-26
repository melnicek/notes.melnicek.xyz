---
description: post/multi/recon/local_exploit_suggester
---

# Linux

### Situational awareness

```text
id
cat /etc/passwd
hostname
cat /etc/issue
cat /etc/*-release
uname -a
ps aux
ip a
ifconfig
route
routel
netstat -anp
ss -anp
cat /etc/iptables
la -lah /etc/cron*
dpkg -l

# page 528 for more

find / -user <user> -perm -4000 -exec ls -ldb {} \; 2>/dev/null
```

### Checking for out of touch SUID binaries

```text
https://github.com/Anon-Exploiter/SUID3NUM/blob/master/suid3num.py
```

### gtfobins

```text
https://gtfobins.github.io/
```

### Enumeration tools

```text
https://github.com/rebootuser/LinEnum
https://github.com/sleventyeleven/linuxprivchecker
```

### If everything else fails

```text
https://book.hacktricks.xyz/linux-unix/linux-privilege-escalation-checklist
```
