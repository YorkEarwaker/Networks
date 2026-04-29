# Secure Shell ssh

Application layer protocol, software package that enables secure system administration and file transfer over insecure networks.

## Notes

AGW project requirements. 
* Secure headless communications remote access to embedded systems.
* Remote log in.
* Remote command line execution.
* Remote file transfer.
* Remote systems administration.
* ...

Use Cases - IoT/IIoT
* Use case; 01, development, systems engineering in the lab/field,        making,      Test
* Use case; 02; manufacture, systems assembly line in the factory/plant,  producing,   Quality Assurance
* Use case; 03, operations,  systems working deployed in the environment, functioning, Business As Usual 
* Use case; 04, servicing,   systems maintenance in the shop/field,       repairing,   IT Service/Asset Management
* Use case; NN, tbd ...

## Status
TODO
* <todo: consider, start tutorial first iteration cycle learning for robust good practice usage, >
* <todo: consider, start use case for RPi Zero headless with either Ubuntu Core or Raspberry Pi Trixie from Ubuntu 24.04.03 LTS Gnome, in first instance for BMV080 sensor project, >
* <todo: consider, ssh appropriate for all use cases listed in notes above, might be secondary not primary in some cases, i.e. REST in some/most operations and servicing? ponder more, >
* <todo: consider, not ssh, REST so place elsewhere 'applications repo?', REST example see GitHub personal access tokens, for IIoT example see home electricity smart meters, REST use cases for the AGW project, >

DONE
* <done: consider, intent to commit >
* <done: consider generic use case diagrams? generic context diagram? generic interaction diagram? wip>

## Output
* Using ssh for access to embedded systems like Raspberry Pi single board computers SBC's.

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

## References

Terms
* SSH, secure shell [WP](https://en.wikipedia.org/wiki/Secure_Shell), org [WS](https://www.ssh.com/academy/ssh), 
* File transfer
* System administration

Concerns - vulnerabilities
* Terrapin Attack, [WP](https://en.wikipedia.org/wiki/Terrapin_attack), fixed in ssh version 9.6

News Papers - ssh version
* Commands to know the version of OpenSSH client and server?, [WS](https://unix.stackexchange.com/questions/721368/commands-to-know-the-version-of-openssh-client-and-server), 18 Oct 2022 (edited), Unix & Linux, StackExchange, 
