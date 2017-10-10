# Graphical SSH Tool Benchmark

## Test Environment
### Host
#### Lubuntu desktop for TigerVNC and X2GO
| Features |  |
| ------------- | ------------- |
| Processor |  8x Intel Xeon CPU E3-1230v3 3.30GHz |
| Memory | 16GB |
| OS | Ubuntu 16.04.3 LTS 64bit |
| X11 Vendor | The X.Org Foundation |
| Desktop | LXDE |
| GPU | NVIDIA Quadro K2000 |

### Clients
#### Mac
| Features |  |
| ------------- | ------------- |
| Model| MacBook Pro (13-inch, 2017, Two Thunderbolt 3 ports)|
| Processor | 2,3 GHz Intel Core i5 |
| Memory | 16 GB 2133 MHz LPDDR3 |
| OS | macOS 10.12.6 |
| GPU | Intel Iris Plus Graphics 640 |

#### Windows
| Features |  |
| ------------- | ------------- |
| Model| HP ZBook 15 G3 |
| Processor | 2.7GHz (8 CPUs) Intel i7 |
| Memory | 16GB |
| OS | Windows 10 64bit |
| GPU | Intel HD Graphics 530 |


#### Linux
| Features |  |
| ------------- | ------------- |
| Model| HP ZBook 15 G2 |
| Processor | 2.8GHz (8 CPUs) Intel i7-4810MQ |
| Memory | 16GB |
| OS | Ubuntu 16.04.LTS 64bit |
| GPU | NVIDIA Quadro K2100M |
### Network
| Elisa 4G on iPhone SE |  |
| ------------- | ------------- |
|ping|13 ms|
|download| 50.13 Mbps|
|upload|19.42 Mbps|




## 1. NoMachine on CSC(nxkajaani.csc.fi)

![noMachineOnCSC](/images/noMachineOnCSC.png)
### Environment
#### Host
* Login nodes: RedHat Enterprise Linux 6 (RHEL6) distribution
* Computing nodes: CendOS 6 (Free distro entirely derived from RHEL6)

There are two servers: Taito & Sisu
* Taito(taito.csc.fi): 16 cabinet HP cluster
* Sisu (sisu.csc.fi): Massively Parallel Processor (MPP) supercomputer produced by Cray Inc., belonging to the XC40 family

Commands on client side:
```bash
/usr/NX/bin/nxplayer
```

### Usability
| Category | Review |
| ------------- | ------------- |
| Coding | Ok. Very smooth on Vim/RStudio  |
| Web surfing| Unusable. Resources load fast but UI latency(scrolling) is terrible.|
| Youtube | Unusable. It feels like 10FPS. Sound is forwarded without a lag. |
|Stability| Very good. Clear UI notification if network is unstable. Session recovery is as good as others.|
|Num of session| One session for free version. NXKajaani is enterprise still allows only one session per user.|
|Key forwarding| `alt` + `tab` can be sent over to sessions when in fullscreen mode. To toggle fullscreen, `ctrl`+`alt`+`0`|

### Graphical Usability
#### Video
[![CSC Taito shell video test](/images/CSC-Taito-shell-video-test.png)
](https://youtu.be/9qn_G0bI9jA "taito test")

#### R Plot
![R plot](/images/R-plot.png)

### Matlab
[Setup](https://research.csc.fi/-/matlab)

### Pros
- clipboard is shared by default

### Cons
- Some shells doesn't authenticate your credential. Use [taito-shell](https://research.csc.fi/taito-shell-user-guide)

### Mobile network test


### References
- [Operating system and shell environment](https://research.csc.fi/taito-operating-system-and-shell-environment)
- [Taito supercluster](https://research.csc.fi/taito-supercluster)
- []()
- []()
- []()

## 2. NoMachine Free on Lubuntu Desktop
### Running server
```bash
sudo /usr/NX/bin/nxserver --restart
```

### Running client
The free version does not support SSH connection. I couldn't figure out to connect using only NX. You can tunnel the NX protocol in an SSH connection:
```bash
ssh -L 4000:localhost:4000 -N -f -l seyoung 130.233.195.77
```
Then edit the NXClient settings as:
![NXClient settings](/images/NXClient-settings.png)

### Youtube test on TigerVNC session
[![TigerVNC-youtube](/images/TigerVNC-youtube.png)](https://youtu.be/GZjPTrmuXII)

## 3. X2GO
X2GO uses X.Org(in Mac, XQuartz) as an X11 vendor. Even though X2GO uses X as its X11, it is still much faster than bare-bones X-forwarding using `ssh -Y`.

Commands on server side:
```bash
service x2goserver start
service x2goserver status
service x2goserver stop
```

### Usability
| Category | Review |
| ------------- | ------------- |
| Coding | Ok. Very smooth on Vim. Pretty smooth on PyCharm. Huge UI latency on Jupyter Notebook |
| Web surfing| Unusable. Resources load fast but UI latency(scrolling) is terrible.|
| Youtube | Unusable. It feels like 10FPS. Sound is forwarded without a lag. |
|Stability| Very good on Linux client poor on Mac. On Linux, the session recovery is as good as others. On Mac, session recovery doesn't happen; the session is detached.|
|Num of session| Multi sessions supported automatically. However, on Macs, client can run only one session at a time.|
|Key forwarding| `alt` + `tab` can be sent over to sessions when in fullscreen mode. To toggle fullscreen, `ctrl`+`alt`+`f`|


### Pros

### Cons
https://wiki.x2go.org/doku.php/wiki:development:roadmap

## 3. TigerVNC
TigerVNC is its own X11 vendor.

### Installation
- Download package @ https://github.com/TigerVNC/tigervnc/releases
- Extract and move the files to `/usr/bin/`

### Running
#### Host
```bash
vncserver       # Launch
```

#### Client
```bash
# 1. Establish an SSH session. Port number is 5900 + (#display)
ssh -L 5901:127.0.0.1:5901 -N -f -l host-username host-ip

# 2. Launch TigerVNC Viewer

# 3. Type in at *VNC server*: localhost:5901

# 4. Enter pw for TigerVNC server
```

### Connection info
- Pixel format: depth 24 (32bpp) little-endianrgb888
- Security method: TLSVnc


### Usability
| Category | Review |
| ------------- | ------------- |
| Coding |  Very good. Tested on Jupyter Notebook. Plotting/Scrolling/Editing/Running works fine. |
| Web surfing| Good. Can browse non-video websites pretty fast. Scrolling is little laggy but still very usable.|
| Youtube | OK. HD & 60FPS is possible when you are not viewing fullscreen. At fullscreen, frame rate is under 28fps. Felt like 22fps. **For sound, one needs to setup a separate sound forwarding server** such as PulseAudio|
|Stability| Good. TigerVNC Viewer freezes when the Internet connection is interrupted. However the session is resumed after the network became stable. For instance when I plugged my iPhone off/in the USB there was a short pause but the session was resumed automatically. |
|Num of session| Multi sessions supported. **Needs manual work on both server and client.** Launch a new session on server and set correct ports on client.|
|Key forwarding| `alt` + `tab` can be sent over to sessions when in fullscreen mode. To toggle fullscreen, `F8` and click `Fullscreen`|

### Pros

### Cons
#### 1. Doesn't forward sound.
Use Pulseaudio server for sound

#### 2. Client needs to setup an SSH session separately.

#### 3. Cannot unlock servers remotely.
When a screensaver starts on the server, you can't unlock the session via VNC.  

Work-around:
```bash
ssh user@vnc_server_address

# View all sessions
loginctl list-sessions
'
SESSION        UID USER             SEAT            
      9       1000 seyoung                          
      2       1000 seyoung                          
      4       1000 seyoung                          
     c6       1000 seyoung          seat0           
      7       1000 seyoung                          
    c12        109 lightdm          seat0           

6 sessions listed.
'

loginctl unlock-session session_id

# I don't know which session is locked...
loginctl unlock-sessions

```
### Reference
https://wiki.archlinux.org/index.php/TigerVNC

## 4. X Forwarding

### Environment
#### Host
Aalto Kosh

#### Client
- macOS 10.12.6
    - MacBook Pro (13-inch, 2017, Two Thunderbolt 3 ports)
    - 2,3 GHz Intel Core i5
    - 16 GB 2133 MHz LPDDR3
    - Intel Iris Plus Graphics 640


### Graphical Usability
#### Coding
Impossible to work on Eclipse. 0.5 sec latency.

#### Image viewing
Good. Almost as good as X2Go

### Cons
- Cannot save sessions
