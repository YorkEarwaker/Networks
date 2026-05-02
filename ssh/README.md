# Secure Shell ssh

Application layer protocol, software package that enables secure system administration and file transfer over insecure networks.

See also
* Electrical engineering, various embedded SBC projects [GH](https://github.com/YorkEarwaker/Electrical-Engineering), e.g. /rpi-z, ...

## Notes

AGW project requirements. 
* Secure headless communications remote access to embedded systems.
* Remote log in.
* Remote command line execution.
* Remote file transfer.
* Remote systems administration.
* ...

Use Cases - ssh high level use cases for IoT/IIoT
* <todo: consider, these are actually business scenarios/buiness use cases, refactor accordingly, find other suitable names for same which might apply, >
* <todo: condider, matrix against which to place tech software or hwardware which will be used against each business scenario, e.g. ssh clearly aligns with each busienss scenario, multiple use cases likely in each business scenario for use of ssh, use case is a workflow/business process within the business scenario, >
* <todo: consider, create a 'strategy and architecture' repo, find better name, for enterprise views of AGW project, elaborate these in first instance, >
```
* Use case; 01, development, systems engineering in the lab/field,        making,      Test
* Use case; 02; manufacture, systems assembly line in the factory/plant,  producing,   Quality Assurance
* Use case; 03, operations,  systems working deployed in the environment, functioning, Business As Usual 
* Use case; 04, servicing,   systems maintenance in the shop/field,       repairing,   IT Service/Asset Management
* Use case; NN, tbd ...
```

## Status
TODO
* <todo: consider, start tutorial first iteration cycle learning for robust good practice usage, >
* <todo: consider, start use case for RPi Zero headless with either Ubuntu Core or Raspberry Pi Trixie from Ubuntu 24.04.03 LTS Gnome, in first instance for BMV080 sensor project, >
* <todo: consider, ssh appropriate for all use cases listed in notes above, might be secondary not primary in some cases, i.e. REST in some/most operations and servicing? ponder more, >
* <todo: consider, not ssh, REST so place elsewhere 'applications repo?', REST example see GitHub personal access tokens, for IIoT example see home electricity smart meters, REST use cases for the AGW project, >
* <todo: consider, ssh for RPi Pico MCU, search for available libs? or would footprint be to large and processing to expensive in MCU env? bare metal ssh? probs not, find use case, verify possibility yes or no, >
* <todo: consider, install sshd server on RPi Trixie, login from ssh client on Dell Ubuntu 24 LTS, >
* <todo: consider, detail dev to prod workflows which will differ for RPi Trixie and Ubuntu Core and Ubuntu Server, headless,  e.g. Ubuntu Core require snap of new app/functoinality to be added to OS image? , RPi Trixie workflow likely more similar to Ubuntu Server although these likely have some wf activity detail differences?  move this else where? where? PMO? PPM? DevOps? to start document as things are accomplished but where to put docs info?, >
* <todo: consider, ubuntu server ssh example, prerequisite Ubuntu Server OS image installed on MicroSd Card, headline as reminder too below  >

DONE
* <done: consider, intent to commit >
* <done: consider generic use case diagrams? generic context diagram? generic interaction diagram? wip>
* <done: consider, for Rpi Zero 2 W, check if ssh server (sshd) is installed on RPi Trixi and Ubuntu Core 24, install if not, setup to enable login via Dell Ubuntu ssh client (ssh), different mechanisms to install and manage ssh in both OS's, so different workflows required, >
* <done: consider, dev use cases above with RPi Zero running Ubuntu Core, for initial dev ssh workflow for AGW project, sensor device making, ssh logon from Dell Ubuntu LTS dev host to RPi Zero Ubuntu Core 4 deployment target, ssh logon success, other dev tasks for this workflow wip, >
* <done: consider, ssh login to RPi Z Ubuntu Core 24 from Dell Ubuntu 24 LTS, >

## Output
* Using ssh for access to embedded systems like Raspberry Pi single board computers SBC's.
* Ubuntu Core 24, sshd server available out of the box, uses a SSH snap built in, managed service by core system. sshd server not installed separately. See 'Ubuntu Core 24' below.
* Raspberry Pi Trixie, confirm sshd server installed separately? See 'Raspberry Pi Trixie' below.

Context diagram
* Network may be wired (e.g. CATV ethernet) or wireless (e.g. 3G/4G/5G WiFi) or both
* Network may be local area LAN or wide area WAN or both
* Network may be internal or external or both
* Client software, installed on an operating system on a hardware device (i.e. ssh)
* Server software, installed on an operating system on a hardware device (i.e sshd)
* Device operating system may have installed on it both client software and server software
* Box's might be; cloud container, virtual machine, hardware like a server blade or laptop or tablet or ...
* Box's, while often separate hardware devices, all have OS execution env into which ssh/sshd is preinstalled or must be installed separately
```
     --------                                                 --------  
    |  Box 1 |                     elided                    |  Box 2 |
    | Client | ------------------- Network ----------------- | Server |
    |  ssh   |                                               |  sshd  |
     --------                                                 --------
```

Interaction diagram
* interactions happen over an operating network.
* fine grained network systems operations activity is elided.
```
     ---------                                                ---------
    | Client  |                    Network                   | Server  |
     ---------                                                ---------
         |                                                        |
         | -- 1. client initiates connection contacting server -> |
         |                                                        |
         | <- 2. sends server public key ------------------------ |
         |                                                        |
         | <- 3. negotiate perameters and open secure channel --- |
         |                                                        |
         | -- 4. user login to server host operating system ----> |
         |                                                        |
         | -- 5. user does use case activities on/via server ---> |
         :                                                        :
         | -- 6. close ssh session -----------------------------> |
```

### Output - Check ssh version
* for both the client software and the server software installed on localhost.
* for security to ensure version has been patched for vulnerabilities.

Determine ssh client version on localhost on the cli.
* Note version 9.6, this version has been fixed for the 'terrapin attack' 
```
$ ssh -V
OpenSSH_9.6p1 Ubuntu-3ubuntu13.15, OpenSSL 3.0.13 30 Jan 2024
```

Determine ssh server version on localhost on the cli.
* Note in this case no server version was detected on the localhost
```
$ sshd -V
Command 'sshd' not found, but can be installed with:
sudo apt install openssh-server
```

Determine ssh server version as well as client version on localhost on the cli.
* Note in this case no server version was detected on the localhost
```
$ dpkg-query --showformat='${Version}\n' --show openssh-server openssh-client
1:9.6p1-3ubuntu13.15

$ dpkg -l | grep ssh
ii  libssh-4:amd64                                0.10.6-2ubuntu0.4                                amd64        tiny C SSH library (OpenSSL flavor)
ii  libssh-gcrypt-4:amd64                         0.10.6-2ubuntu0.4                                amd64        tiny C SSH library (gcrypt flavor)
ii  openssh-client                                1:9.6p1-3ubuntu13.15                             amd64        secure shell (SSH) client, for secure access to remote machines

$ dpkg -l |grep openssh-client
ii  openssh-client                                1:9.6p1-3ubuntu13.15                             amd64        secure shell (SSH) client, for secure access to remote machines

$ dpkg -l |grep openssh-server
```

### Ubuntu Core 24 - embedded SBC OS deployment target
* Status: Success! Completed during install.
* SSH key setup prior to installation of the OS on MicroSD Card. SSH key is required during installation process.
* Core uses a SSH snap built in, managed service by core system. snap-based SSH service.
* <todo: consider, review in more detail Ubuntu client/server built in managed service in core system. >
* <todo: consider, review 'snap set' commands to manage ssh snap configuration, find Ubuntu docs for same, >
* <todo: consider, bau dev workflow for ssh with Ubuntu Core, use AGW project rpi-z/cpa/snr-rsl as examplar, >

see
* Ubuntu One SSH

### Raspberry Pi Trixie - embedded SBC OS deployment target
* Status: TBD
* <todo: consider, tasks to accomplish ssh access to RPi Trixie SBC from Dell Ubuntu dev box, >
* <todo: consider, confirm standard openssh-server use, standard /etc/ssh/sshd_config file, >
* <todo: consider, RPi docs for ssh into Trixie OS, >
* <todo: consider, bau dev workflow for ssh with RPi Trixie, use AGW project rpi-z/cpa/snr-rsl as examplar, >


### Ubuntu Server - embedded? SBC OS deployment target
* Status: TBD
* <todo: consider, probably not embedded deployment target, likely just sever farms, what could be stripped out, might require bespoke compilaton of the server code base, keep under review, >
* <todo: consider, source or do benchmarking for comparison of RPi Trixi and Ubuntu Core and Ubuntu Server, for various embedded targets,  >
* <todo: consider, likely not snap based SSH service, so would require openssh-client openssh-server install, verify this? >
* ...

### Dell Ubuntu LTS - laptop dev host
* Status: TBD
* <todo: consider, dev use cases above with RPi Zero running RPi Trixie, for initial dev ssh workflow for AGW project, sensor device making,  >
* <todo: consider, review in more detail Ubuntu client/server built in managed service in core system. is it managed service for LTS or not? in which case openssh client and server would have to be sintalled in this env. >
* <todo: consider, other use cases for ssh with wider server side IT platfrom estate for AGW project, very many, >
* <todo: consider, unintall openssh-client from Dell Ubuntu LTS, how might it comflict with Ubuntu snap-based SSH service, >

#### SSH logon - from Dell Ubuntu 24 LTS to RPi Zero Ubuntu Core 24
From Dell laptop running Ubuntu 24 LTS 'the development host' OS logon to Raspberry Pi Zero running Ubuntu Core 24 'the deployment target' OS.
* Success!
* SSH client on Dell XPS-15-9560 hardware running Ubuntu 24 LTS Gnome operating system
* SSH server on RPi Zero 2 W hardware running Ubuntu Core 24 operating system
* Query some of the RPi Zero specifications information

```
york-earwaker@york-earwaker-XPS-15-9560:~$ ssh yorkearwaker@<your-rpi-sbc-ip-address>
Welcome to Ubuntu Core 24

* Documentation: https://ubuntu.com/core/docs

This is a pre-built Ubuntu Core image. Pre-built images are ideal for
exploration as you develop your own custom Ubuntu Core image.

To learn how to create your custom Ubuntu Core image, see our guide:

* Getting Started: https://ubuntu.com/core/docs/get-started

In this image, why not create an IoT web-kiosk. First, connect a
screen, then run:

   snap install ubuntu-frame wpe-webkit-mir-kiosk
   snap set wpe-webkit-mir-kiosk url=https://ubuntu.com/core

For more ideas, visit:

* First steps: https://ubuntu.com/core/docs/first-steps
Last login: Tue Jan 20 14:50:08 2026 from <your-dev-host-pc-ip-address>
yorkearwaker@localhost:~$ 
```

Simple Model Identification
```
yorkearwaker@localhost:~$ cat /sys/firmware/devicetree/base/model
Raspberry Pi Zero 2 W Rev 1.0
```

Subset of /proc/cpuinfo info using grep
* Note, the Hardware line value not shown, it has been removed by kernel developers as it is not standard across arm architectures
* for full info 'cat /proc/cpuinfo'
```
yorkearwaker@localhost:~$ cat /proc/cpuinfo | grep -E "Hardware|Revision|Model"
Revision  	: 902120
Model		: Raspberry Pi Zero 2 W Rev 1.0
```

Operating system version
```
yorkearwaker@localhost:~$ cat /etc/os-release
NAME="Ubuntu Core"
VERSION="24"
ID=ubuntu-core
PRETTY_NAME="Ubuntu Core 24"
VERSION_ID="24"
HOME_URL="https://snapcraft.io/"
BUG_REPORT_URL="https://bugs.launchpad.net/snappy/"
```

Kernel version running
```
yorkearwaker@localhost:~$ uname -a
Linux localhost 6.8.0-1043-raspi #47-Ubuntu SMP PREEMPT_DYNAMIC Fri Oct 17 22:33:56 UTC 2025 aarch64 aarch64 aarch64 GNU/Linux
```

RAM size
```
yorkearwaker@localhost:~$ free -h
               total        used        free      shared  buff/cache   available
Mem:           409Mi       149Mi        20Mi       4.3Mi       258Mi       259Mi
Swap:             0B          0B          0B
```

CPU
```
yorkearwaker@localhost:~$ lscpu
Architecture:             aarch64
  CPU op-mode(s):         32-bit, 64-bit
  Byte Order:             Little Endian
CPU(s):                   4
  On-line CPU(s) list:    0-3
Vendor ID:                ARM
  Model name:             Cortex-A53
    Model:                4
    Thread(s) per core:   1
    Core(s) per cluster:  4
    Socket(s):            -
    Cluster(s):           1
    Stepping:             r0p4
    CPU(s) scaling MHz:   100%
    CPU max MHz:          1000.0000
    CPU min MHz:          600.0000
    BogoMIPS:             38.40
    Flags:                fp asimd evtstrm crc32 cpuid
Caches (sum of all):      
  L1d:                    128 KiB (4 instances)
  L1i:                    128 KiB (4 instances)
  L2:                     512 KiB (1 instance)
Vulnerabilities:          
  Gather data sampling:   Not affected
  Itlb multihit:          Not affected
  L1tf:                   Not affected
  Mds:                    Not affected
  Meltdown:               Not affected
  Mmio stale data:        Not affected
  Reg file data sampling: Not affected
  Retbleed:               Not affected
  Spec rstack overflow:   Not affected
  Spec store bypass:      Not affected
  Spectre v1:             Mitigation; __user pointer sanitization
  Spectre v2:             Not affected
  Srbds:                  Not affected
  Tsx async abort:        Not affected
  Vmscape:                Not affected
```

Number of cores
```
yorkearwaker@localhost:~$ nproc
4
```

Log out of ssh session
```
yorkearwaker@localhost:~$ exit
logout
Connection to <your-rpi-sbc-ip-address> closed.
```

#### SSH logon - from Dell Ubuntu 24 LTS to RPi Zero RPi Trixie
From Dell laptop running Ubuntu 24 LTS 'the development host' OS logon to Raspberry Pi Zero running RPi Trixie 'the deployment target' OS.
* Status: TBD
* SSH client on Dell XPS-15-9560 hardware running Ubuntu 24 LTS operating system
* SSH server on RPi Zero 2 W hardware running RPi Trixie operating system
* Query some of the RPi Zero specification information
```
TBD
```

#### SSH logon - from Dell Ubuntu 24 LTS to RPi Zero Ubuntu Server
From Dell laptop running Ubuntu 24 LTS 'the development host' OS logon to Raspberry Pi Zero running Ubuntu Server 'the deployment target' OS.
* Status: TBD
* SSH client on Dell XPS-15-9560 hardware running Ubuntu 24 LTS operating system
* SSH server on RPi Zero 2 W hardware running Ubuntu Server operating system
* Query some of the RPi Zero specification information
* <todo: consider, Ubuntu Server 26 for start of evaluation of new release, >
```
TBD
```

## References

Terms
* SSH, secure shell [WP](https://en.wikipedia.org/wiki/Secure_Shell), org [WS](https://www.ssh.com/academy/ssh), 
* File transfer
* System administration

Concerns - vulnerabilities
* Terrapin Attack, [WP](https://en.wikipedia.org/wiki/Terrapin_attack), fixed in ssh version 9.6

Docs - RPi
* Remote Access, [WS](https://www.raspberrypi.com/documentation/computers/remote-access.html), RPi docs, 

News Papers - ssh version
* Commands to know the version of OpenSSH client and server?, [WS](https://unix.stackexchange.com/questions/721368/commands-to-know-the-version-of-openssh-client-and-server), 18 Oct 2022 (edited), Unix & Linux, StackExchange, 

News Papers - ssh RPi, ssh Trixie
* configure SSH trixie, [WS](https://forums.raspberrypi.com/viewtopic.php?t=396708), 7 March 2026, RPi Forums, 
* Can't change RPi4 hostname, disable cloud init [WS](https://forums.raspberrypi.com/viewtopic.php?p=2355903&hilit=disable+cloud+init#p2355903), 30 Dec 2025, RPi Forums, 
