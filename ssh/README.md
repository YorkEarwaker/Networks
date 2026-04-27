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

## Status
TODO
* <todo: consider, start tutorial first iteration cycle learning for robust good practice usage, >
* <todo: consider, start use case for RPi Zero headless to Ubuntu Core and Raspberry Pi Trixie from Ubuntu 24.04.03 LTS Gnome, in first instance for BMV080 sensor project, >

DONE
* <done: consider, intent to commit >

## Output

Determine ssh client version on localhost on the cli.
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

News Papers - ssh version
* Commands to know the version of OpenSSH client and server?, [WS](https://unix.stackexchange.com/questions/721368/commands-to-know-the-version-of-openssh-client-and-server), 18 Oct 2022 (edited), Unix & Linux, StackExchange, 
