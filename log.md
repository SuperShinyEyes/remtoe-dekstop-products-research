## Problem: VNCViewer shows black blank screen
When connecting to VNCServer(cs-208@org.aalto.fi) from client, the connection is established but gives black blank screen.
No error in .vnc/log.log.

### Cause: `.vnc/xstartup`
Aalto Ubuntu has its own its own `xinitrc` and  it collids with VNCServer accessing XAuthority or whatever.
Here's the original `.vnc/xstartup` created by TigerVNC:
```bash
#!/bin/sh

unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
OS=`uname -s`
if [ $OS = 'Linux' ]; then
    case "$WINDOWMANAGER" in
        *gnome*)
            if [ -e /etc/SuSE-release ]; then
                PATH=$PATH:/opt/gnome/bin
                export PATH
            fi
            ;;
    esac
fi
if [ -x /etc/X11/xinit/xinitrc ]; then
    exec /etc/X11/xinit/xinitrc
fi
if [ -f /etc/X11/xinit/xinitrc ]; then
    exec sh /etc/X11/xinit/xinitrc
fi
[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
xsetroot -solid grey
xterm -geometry 80x24+10+10 -ls -title "$VNCDESKTOP Desktop" &
twm &
```

### Solution: new `xstartup`
Replace with below:
```bash
#!/bin/sh

unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS

[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
xsetroot -solid grey
xterm -geometry 80x24+10+10 -ls -title "$VNCDESKTOP Desktop" &

startxfce4 &
```

## Authentication: use Aalto credential
### Problem: TigerVNC authenticates with VNCServer pw by default.
If a user has set weak pw then another user can hijack his sessions.

### Solution: Start server with PAM and specific user.
```bash
vncserver -SecurityTypes=TLSPlain -PlainUsers=$USER -pam_service login -desktop $HOSTNAME
```
If you start a server this way then you will need to give your login credential which you used to login to the machine.

### How Aalto authentication works
```
sshd ---> pam ---> sssd ---> AD 
```


### Reference
- [PAM](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/Pluggable_Authentication_Modules.html)
- [Kerberos](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/Using_Kerberos.html)
- []()

   
## Encryption
Simo tested with Wireshark. If **SecurityTypes** is `None` then everything, including keystrokes, mouse positions and etc., will be plainly transferred. However, even the default type is secured.


## Auto port number allocation(Not resolved)
### Problem: find an intuitive way to allocate port numbers for users
By default VNCServer uses ports starting from 5901.(The starting state is 5900 and you add a display number to it.)

We tried:
```bash
vncserver :$UID -SecurityTypes=TLSPlain -PlainUsers=$USER -pam_service login -desktop $HOSTNAME
```
`$UID` is an unique ID for every user. It didn't work unfortunately because `$UID`s are seven digits which seemed to be too large for a port number.

## Problem
```bash
```




