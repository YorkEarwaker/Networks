# Secure Shell ssh

Application layer protocol, software package that enables secure system administration and file transfer over insecure networks.

See also
* 

## Notes

AGW project requirements. 
* Secure headless communications remote access to embedded systems.
* Remote log in.
* Remote command line execution.
* Remote file transfer.
* Remote systems administration.
* ...

Use Cases - IoT/IIoT
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
* <todo: consider, ssh for RPi Pico MCU, search for available libs? or would footprint be to large and processing to expensive in MCU env? bare metal ssh? probs not, find use case, verity possibility yes or no, >

DONE
* <done: consider, intent to commit >
* <done: consider generic use case diagrams? generic context diagram? generic interaction diagram? wip>
* <done: consider, for Rpi Zero 2 W, check if ssh server (sshd) is installed on RPi Trixi and Ubuntu Core 24, install if not, setup to enable login via Dell Ubuntu ssh client (ssh), different mechanisms to install and manage ssh in both OS's, so different workflows required, >

## Output
* Using ssh for access to embedded systems like Raspberry Pi single board computers SBC's.
* Ubuntu Core 24, sshd server available out of the box, uses a SSH snap built in, managed service by core system. sshd server not installed separately. See 'Ubuntu Core 24' below.
* Raspberry Pi Trixie, confirm sshd server installed seperately? See 'Raspberry Pi Trixie' below.

Context diagram
* Network may be wired (e.g. CATV ethernet) or wireless (e.g. 3G/4G/5G WiFi) or both
* Network may be local area LAN or wide area WAN or both
* Network may be internal or external or both
* Client software, installed on an operating system on a hardware device (i.e. ssh)
* Server software, installed on an operating system on a hardware device (i.e sshd)
* Device operating system may have installed on it both client software and server software
```
      Client --------------------- Network ------------------- Server
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

### Ubuntu Core 24 - embedded SBC deployment target
* Success! Completed during install.
* SSH key setup prior to installation of the OS. SSH key is required during installation process.
* Core uses a SSH snap built in, managed service by core system. snap-based SSH service.
* <todo: consider, review in more detail Ubuntu client/server built in managed service in core system. >
* <todo: consider, review 'snap set' commands to manage ssh snap configuration, find Ubuntu docs for same, >
* <todo: consider, bau dev workflow for ssh with Ubuntu Core, use AGW project rpi-z/cpa/snr-rsl as examplar, >

see
* Ubuntu One SSH

### Raspberry Pi Trixie - embedded SBC deployment target
* TBD
* <todo: consider, tasks to accomplish ssh access to RPi Trixie SBC from Dell Ubuntu dev box, >
* <todo: consider, confirm standard openssh-server use, standard /etc/ssh/sshd_config file, >
* <todo: consider, RPi docs for ssh into Trixie OS, >
* <todo: consider, bau dev workflow for ssh with RPi Trixie, use AGW project rpi-z/cpa/snr-rsl as examplar, >

### Dell Ubuntu LTS - laptop dev box
* TBD
* <todo: consider, two dev use cases above with Ubuntu Core and RPi Trixie, for initial dev ssh workflow for AGW project, sensor device making,  >
* <todo: consider, review in more detail Ubuntu client/server built in managed service in core system. >
* <todo: consider, other use cases for ssh with wider server side IT platfrom estate for AGW project, very many, >
* <todo: consider, unintall openssh-client from Dell Ubuntu LTS, how might it comflict with Ubuntu snap-based SSH service, >

## References

Terms
* SSH, secure shell [WP](https://en.wikipedia.org/wiki/Secure_Shell), org [WS](https://www.ssh.com/academy/ssh), 
* File transfer
* System administration

Concerns - vulnerabilities
* Terrapin Attack, [WP](https://en.wikipedia.org/wiki/Terrapin_attack), fixed in ssh version 9.6

News Papers - ssh version
* Commands to know the version of OpenSSH client and server?, [WS](https://unix.stackexchange.com/questions/721368/commands-to-know-the-version-of-openssh-client-and-server), 18 Oct 2022 (edited), Unix & Linux, StackExchange, 
