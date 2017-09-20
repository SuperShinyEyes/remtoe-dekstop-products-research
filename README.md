# Graphical SSH Tool(Remote Control) Analysis
Compare the following tools for Aalto IT servers.
- NX
    - NoMachine(on [CSC](https://www.csc.fi/))
    - OpenNX
    - FreeNX
    - NeatNX
- X2GO

## Scenario
1. Mac/Windows/Linux users want to work on a linux server where there are huge sets of data, Matlab and powerful computation power.

2. Mac/Windows/Linux users connect to a Windows server and use MS Word/Exel/Powerpoint/Visual Studio.

## Technologies

### 1. [NoMachine (NX)](https://en.wikipedia.org/wiki/NX_technology)
[*We recommend NoMachine for remote usage of graphical interfaces instead of X11 connections. It often speeds up the graphical response even 10 fold with respect to the normal X11 connections.*](https://research.csc.fi/csc-guide-connecting-the-servers-of-csc)

#### License
Free & Enterprise

#### Platform support
| Host | Client |
| ------------- | ------------- |
| Windows, Mac, Linux and Linux ARM | Windows, Mac OS X, iOS, Android, Linux, Linux ARM and HTML/JavaScript permitting access|

#### Features
- sharing network devices
- session recording
- file transfer
- multi-media capability
- browser-based access
- multi-node clustering **(enterprise-only)**
- failover functionality **(enterprise-only)**
- run multiple virtual Linux instances on the same machine **(enterprise-only)**

#### Graphics
Uses VirtualGL, which means high-end OpenGL-based X applications and 3-D CAD programs are rendered and displayed with the best possible accuracy. VirtualGL is an open source program that redirects the 3D rendering commands from Unix and Linux OpenGL applications to 3D accelerator hardware in a dedicated server and displays the rendered output interactively to a thin client located elsewhere on the network.

#### Pros
- clipboard is shared by default

#### Cons
- Some shells doesn't authenticate your credential. Use [taito-shell](https://research.csc.fi/taito-shell-user-guide)


### 2. [X2GO](https://wiki.x2go.org/doku.php/doc:newtox2go)

#### License
Free

#### Platform support
| Host | Client |
| ------------- | ------------- |
| Linux| Linux, PC, Mac |

#### Features
- Session
- Desktop sharing
- **Disconnect and reconnect to a session, even from another client** (Security?)
- Support for sound
- Support for **as many simultaneous users** as the computer's resources will support (NX3 free edition limited you to 2.)
- File Sharing from client to server
- Printer Sharing from client to server
- Easily select from multiple desktop environments (e.g., MATE, GNOME, KDE)
- Remote support possible via [Desktop Sharing](https://wiki.x2go.org/doku.php/doc:usage:desktop-sharing)
- The ability to access single applications by specifying the name of the desired executable in the client configuration or selecting one of the pre-defined common applications

#### Graphics
No Machine NX3 under the hood

#### Network
- SSH


#### Installation




setxkbmap us
sudo -i
