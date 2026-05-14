# Domain name system dns

Core networking capability, core internet capability, 

## Notes

Objectives
* use as a means to stop doom scrolling in the attention/addition economy 
* use as another layer to block domain names, a third layer, in addition to hosts file and Brave filters

Learning 
* use as a means of deeper understanding of dns and dhcp for ldap and similar network services
* use as a means of deeper understanding of relation to IPv4 & IPv6
* use as a means of deeper understanding of other IETF specifications,  

## Status
TODO
* <todo: consider, find precompiled lists of domains to block, like community Brave filters, >
* <todo: consider, use to block domain names to filter out social media >
* <todo: consider, use to block domain names to filter out 24hr news >
* <todo: consider, use to block domain names to filter out suicide sites >
* <todo: consider, use to block domain names to filter out sex sites >
* <todo: consider, use to block domain names to filter out big tech sites >
* <todo: consider, seperate project of ldap, /ldp? /ldap? >
* <todo: consider, dnsmasq like network software lightweight for embedded, >
* <todo: consider, SmartDNS, DNS routing scheduler, to pair with dnsmasq, >

DONE
* <done: consider, intent to commit, >
* <done: consider, concentrate on dnsmasq in first instance due to use case for embedded, >

## Libs
These are not recommendations but things to explore

home labs, routers, simple networks, small LANs, embedded devices
* dnsmasq, [WP](https://en.wikipedia.org/wiki/Dnsmasq), org [WS](https://thekelleys.org.uk/dnsmasq/doc.html), ubuntu [WS](https://manpages.ubuntu.com/manpages/stonking/man8/dnsmasq.8.html), GPL, local dns forwarder and dhcp server and tftp server, single threaded, lightweight, network booting PXE
* smart DNS? [GH](https://pymumu.github.io/smartdns/en/) is this the software?, license?, embedded?, dns resolution enhancement, not sure more research required, 

Init service
* systemd [WP](https://en.wikipedia.org/wiki/Systemd), in Ubuntu
* systemd-resolved, fully featured dns resolver service, in Ubuntu v16 replaced resolvconf 

enterprise - are all these enterprise grade?
* bind, complex large scale deployments, full stack dns server both roles as recursive resolver and limited authoritative server zones
* nds, authoritative server, 
* unbound, security, privacy, full recursive resolver, from OPNsense 
* OPNsense, [WP](https://docs.opnsense.org/index.html), open source firewall, BDS
* ...

dns configuration framework, for managing /etc/resolv.conf file, security concerns, 
* openresolv, BDS, written in POSIX shell, drop in replacement for Debian resolvconf, better maintained?
* resolvconf, [WP](https://en.wikipedia.org/wiki/Resolvconf), GPL, requires Bash shell,

### Services

Proprietary
* OpenDNS, upstream filtering/resolution, US
* ICAN?
* Whois? 

## Scenarios
Different usage scenarios, 
* keeping in mind AGW project and need for embedded
* more general use cases for DNS 

### Linux - embedded - Debian, RPi OS,
Both dnsmasq and smart dns are 
* complementary, 
* Raspberry Pi compatible, 
* <todo: consider, consolidate over same tech stack for DNS for RPi OS and Ubundu Core, A N Other embedded hardware, >

### Linux - embedded - Ubuntu Core
Both dnsmasq and smart dns may cause conflicts
* Core immutable architecture snap constraints make use in Ubuntu Core difficult
* Ubuntu core uses systemd
* systemd won't cover all use cases of dnsmasq or smart dns? confirm. how to mitigate.

Recommended snaps to use with Ubuntu Core, 
* coreDNS
* pi-hole 
* unbound
* <todo: consider, validate these options as good for Core, good for embedded, any other candidates? >
* <todo: consider, consolidate over same tech stack for DNS for RPi OS and Ubuntu Core, is this possible, >

### Linux - desktop/server - Debian, Ubuntu, other
Use dnsmasq to block domain names, maintain sanity in a world driven mad by the compression of time and space by social chaos of move from analogue to digital.
* The world was a better place with only analogue telco landlines

## Output
Examples of how to use dns and dhcp tools 
* <todo: consider, block list, blocked, heading example, >
* <todo: consider, allow list, permitted, heading example, >

### dnsmasq
Status: WIP
* dnsmasq, progress, wip
* dnsmasq, issues ongoing, capability/skills gap to overcome,
* dnsmasq, not achieved first objective of blocking a domain name as of 2026.05.14, 2nd day of finding things out.
* <todo: consider, find possible conflict issues with systemd-resolv Ubuntu OS DNS resolver, >
* <todo: there might be conflicts with dnsmasq and Brave Filters, Brave Filters don't seem to be working in the same way since dnsmasq was installed even though it is inactive, or it may just be browser caching issues, wip >

Install dnsmasq - generates config files and others
```
$ sudo apt install dnsmasq
```

Query dnsmasq version
```
$ dnsmasq -v
Dnsmasq version 2.90  Copyright (c) 2000-2024 Simon Kelley
Compile time options: IPv6 GNU-getopt DBus no-UBus i18n IDN2 DHCP DHCPv6 no-Lua TFTP conntrack ipset nftset auth cryptohash DNSSEC loop-detect inotify dumpfile

This software comes with ABSOLUTELY NO WARRANTY.
Dnsmasq is free software, and you are welcome to redistribute it
under the terms of the GNU General Public License, version 2 or 3.
```

Status of dnsmasq service, not started
```
$ systemctl status dnsmasq
× dnsmasq.service - dnsmasq - A lightweight DHCP and caching DNS server
     Loaded: loaded (/usr/lib/systemd/system/dnsmasq.service; enabled; preset: >
     Active: failed (Result: exit-code) since Wed 2026-05-13 16:11:30 BST; 11mi>
    Process: 34358 ExecStartPre=/usr/share/dnsmasq/systemd-helper checkconfig (>
    Process: 34363 ExecStart=/usr/share/dnsmasq/systemd-helper exec (code=exite>
        CPU: 18ms

May 13 16:11:30 york-earwaker-XPS-15-9560 systemd[1]: Starting dnsmasq.service >
May 13 16:11:30 york-earwaker-XPS-15-9560 systemd-helper[34363]: dnsmasq: faile>
May 13 16:11:30 york-earwaker-XPS-15-9560 dnsmasq[34363]: failed to create list>
May 13 16:11:30 york-earwaker-XPS-15-9560 dnsmasq[34363]: FAILED to start up
May 13 16:11:30 york-earwaker-XPS-15-9560 systemd[1]: dnsmasq.service: Control >
May 13 16:11:30 york-earwaker-XPS-15-9560 systemd[1]: dnsmasq.service: Failed w>
May 13 16:11:30 york-earwaker-XPS-15-9560 systemd[1]: Failed to start dnsmasq.s>
york-earwaker@york-earwaker-XPS-15-9560:~/Documents/dev/repo/networks$  
```

Verify listening port, similar, but not identical, responses
* listing things listening on port 53, like dnsmasq, and protocols udp tcp,
```
$ sudo netstat -tulnp | grep :53
$ ss -tulnp | grep :53
```

Test DNS resolution
```
$ dig @127.0.0.1 example.com
;; communications error to 127.0.0.1#53: connection refused
;; communications error to 127.0.0.1#53: connection refused
;; communications error to 127.0.0.1#53: connection refused

; <<>> DiG 9.18.39-0ubuntu0.24.04.3-Ubuntu <<>> @127.0.0.1 example.com
; (1 server found)
;; global options: +cmd
;; no servers could be reached

$ nslookup example.com 127.0.0.1
;; communications error to 127.0.0.1#53: connection refused
;; communications error to 127.0.0.1#53: connection refused
;; communications error to 127.0.0.1#53: connection refused
;; no servers could be reached
```

Enable dnsmasq service
```
$ sudo systemctl enable dnsmasq.service
Synchronizing state of dnsmasq.service with SysV service script with /usr/lib/systemd/systemd-sysv-install.
Executing: /usr/lib/systemd/systemd-sysv-install enable dnsmasq

```

Start dnsmasq service
* Failure :(
```
$ sudo systemctl start dnsmasq.service
Job for dnsmasq.service failed because the control process exited with error code.
See "systemctl status dnsmasq.service" and "journalctl -xeu dnsmasq.service" for details.
```

Attempt minimal configuration
* Key value pairs suggested by Brave Search Leo
* Helped make some headway
* Not really sure what the implications are in full at this point, 2026.05.13 
```
port=53: Specifies the UDP port for DNS queries. 
listen-address=127.0.0.1,192.168.1.10: Sets the IP addresses dnsmasq listens on. 
interface=eth0: Restricts dnsmasq to specific network interfaces. 
domain-needed and bogus-priv: Prevents forwarding of non-routed or plain names. 
server=8.8.8.8: Defines upstream DNS servers for non-local domain queries. 
dhcp-range=192.168.1.100,192.168.1.200,12h: Enables DHCP with a specific IP range and lease tim
```

Validate /etc/dnsmasq.conf file changes, above
* Test the configuration without starting the service
```
$ sudo dnsmasq --test
dnsmasq: syntax check OK.
```

Restart dnsmasq
```
$ sudo systemctl restart dnsmasq
```

Status of dnsmasq service
* Success! :| at least in part
```
$ systemctl status dnsmasq
● dnsmasq.service - dnsmasq - A lightweight DHCP and caching DNS server
     Loaded: loaded (/usr/lib/systemd/system/dnsmasq.service; enabled; preset: >
     Active: active (running) since Wed 2026-05-13 17:21:45 BST; 2min 8s ago
    Process: 38043 ExecStartPre=/usr/share/dnsmasq/systemd-helper checkconfig (>
    Process: 38048 ExecStart=/usr/share/dnsmasq/systemd-helper exec (code=exite>
    Process: 38056 ExecStartPost=/usr/share/dnsmasq/systemd-helper start-resolv>
   Main PID: 38054 (dnsmasq)
      Tasks: 1 (limit: 38074)
     Memory: 776.0K (peak: 3.3M)
        CPU: 50ms
     CGroup: /system.slice/dnsmasq.service
             └─38054 /usr/sbin/dnsmasq -x /run/dnsmasq/dnsmasq.pid -u dnsmasq ->

May 13 17:21:45 york-earwaker-XPS-15-9560 systemd[1]: Starting dnsmasq.service >
May 13 17:21:45 york-earwaker-XPS-15-9560 dnsmasq[38054]: started, version 2.90>
May 13 17:21:45 york-earwaker-XPS-15-9560 dnsmasq[38054]: compile time options:>
May 13 17:21:45 york-earwaker-XPS-15-9560 dnsmasq-dhcp[38054]: DHCP, IP range 1>
May 13 17:21:45 york-earwaker-XPS-15-9560 dnsmasq[38054]: using nameserver 192.>
May 13 17:21:45 york-earwaker-XPS-15-9560 dnsmasq[38054]: bad address at /etc/h>
May 13 17:21:45 york-earwaker-XPS-15-9560 dnsmasq[38054]: read /etc/hosts - 81 >
May 13 17:21:45 york-earwaker-XPS-15-9560 resolvconf[38062]: Dropped protocol s>
May 13 17:21:45 york-earwaker-XPS-15-9560 resolvconf[38062]: Failed to set DNS >
May 13 17:21:45 york-earwaker-XPS-15-9560 systemd[1]: Started dnsmasq.service ->
```

Stop the dnsmasq service
* check the status of the service to query whether it was started and is `active`
* stop the service, `$ sudo systemctl stop dnsmasq.service`
* check the status of the service to ensure it was stopped and is `inactive`
```
$ systemctl status dnsmasq
● dnsmasq.service - dnsmasq - A lightweight DHCP and caching DNS server
     Loaded: loaded (/usr/lib/systemd/system/dnsmasq.service; enabled; preset: >
     Active: active (running) since Thu 2026-05-14 10:09:40 BST; 44min ago
   Main PID: 1933 (dnsmasq)
      Tasks: 1 (limit: 38074)
     Memory: 3.0M (peak: 5.5M)
        CPU: 71ms
     CGroup: /system.slice/dnsmasq.service
             └─1933 /usr/sbin/dnsmasq -x /run/dnsmasq/dnsmasq.pid -u dnsmasq -r>

May 14 10:09:40 york-earwaker-XPS-15-9560 systemd[1]: Starting dnsmasq.service >
May 14 10:09:40 york-earwaker-XPS-15-9560 dnsmasq[1933]: started, version 2.90 >
May 14 10:09:40 york-earwaker-XPS-15-9560 dnsmasq[1933]: compile time options: >
May 14 10:09:40 york-earwaker-XPS-15-9560 dnsmasq-dhcp[1933]: DHCP, IP range 19>
May 14 10:09:40 york-earwaker-XPS-15-9560 dnsmasq[1933]: using nameserver 192.1>
May 14 10:09:40 york-earwaker-XPS-15-9560 dnsmasq[1933]: bad address at /etc/ho>
May 14 10:09:40 york-earwaker-XPS-15-9560 dnsmasq[1933]: read /etc/hosts - 81 n>
May 14 10:09:40 york-earwaker-XPS-15-9560 resolvconf[1944]: Dropped protocol sp>
May 14 10:09:40 york-earwaker-XPS-15-9560 resolvconf[1944]: Failed to set DNS c>
May 14 10:09:40 york-earwaker-XPS-15-9560 systemd[1]: Started dnsmasq.service ->

$ sudo systemctl stop dnsmasq.service

$ systemctl status dnsmasq
○ dnsmasq.service - dnsmasq - A lightweight DHCP and caching DNS server
     Loaded: loaded (/usr/lib/systemd/system/dnsmasq.service; enabled; preset: >
     Active: inactive (dead) since Thu 2026-05-14 10:56:35 BST; 13s ago
   Duration: 46min 55.421s
    Process: 8735 ExecStop=/usr/share/dnsmasq/systemd-helper stop-resolvconf (c>
   Main PID: 1933 (code=exited, status=0/SUCCESS)
        CPU: 82ms

May 14 10:09:40 york-earwaker-XPS-15-9560 dnsmasq[1933]: read /etc/hosts - 81 n>
May 14 10:09:40 york-earwaker-XPS-15-9560 resolvconf[1944]: Dropped protocol sp>
May 14 10:09:40 york-earwaker-XPS-15-9560 resolvconf[1944]: Failed to set DNS c>
May 14 10:09:40 york-earwaker-XPS-15-9560 systemd[1]: Started dnsmasq.service ->
May 14 10:56:35 york-earwaker-XPS-15-9560 systemd[1]: Stopping dnsmasq.service >
May 14 10:56:35 york-earwaker-XPS-15-9560 resolvconf[8739]: Dropped protocol sp>
May 14 10:56:35 york-earwaker-XPS-15-9560 resolvconf[8739]: Failed to revert in>
May 14 10:56:35 york-earwaker-XPS-15-9560 dnsmasq[1933]: exiting on receipt of >
May 14 10:56:35 york-earwaker-XPS-15-9560 systemd[1]: dnsmasq.service: Deactiva>
May 14 10:56:35 york-earwaker-XPS-15-9560 systemd[1]: Stopped dnsmasq.service ->
$ 
```

For debugging dnsmasq
* Run dnsmasq in debug mode in the foreground in the terminal cli to view operations
* $ sudo dnsmasq --no-daemon --log-queries=extra --log-dhcp --log-debug -C /path/to/dnsmasq.conf
```
$ sudo dnsmasq --no-daemon --log-queries=extra --log-dhcp --log-debug -C /etc/dnsmasq.conf
dnsmasq: started, version 2.90 cachesize 150
dnsmasq: compile time options: IPv6 GNU-getopt DBus no-UBus i18n IDN2 DHCP DHCPv6 no-Lua TFTP conntrack ipset nftset auth cryptohash DNSSEC loop-detect inotify dumpfile
dnsmasq-dhcp: DHCP, IP range 192.168.0.50 -- 192.168.0.150, lease time 12h
dnsmasq: using nameserver 192.168.0.1#53 for domain localnet 
dnsmasq: reading /etc/resolv.conf
dnsmasq: using nameserver 192.168.0.1#53 for domain localnet 
dnsmasq: using nameserver 127.0.0.53#53
dnsmasq: bad address at /etc/hosts line 436
dnsmasq: read /etc/hosts - 81 names
dnsmasq: 1 127.0.0.1/5353 forwarded query to 127.0.0.53
dnsmasq: 2 127.0.0.1/5353 forwarded query to 127.0.0.53
dnsmasq: 3 127.0.0.1/5353 forwarded query to 127.0.0.53
dnsmasq: 4 127.0.0.1/5353 forwarded query to 127.0.0.53
dnsmasq: 5 127.0.0.1/5353 forwarded query to 127.0.0.53
dnsmasq: 6 127.0.0.1/5353 forwarded query to 127.0.0.53
dnsmasq: 7 127.0.0.1/5353 forwarded query to 127.0.0.53
dnsmasq: 8 127.0.0.1/5353 forwarded query to 127.0.0.53
dnsmasq: 9 127.0.0.1/5353 forwarded query to 127.0.0.53
dnsmasq: 10 127.0.0.1/5353 forwarded query to 127.0.0.53
```

Exit (kill the process) when started as dnsmasq --no-daemon
* In a separate terminal window run
* SIGTERM kills the process in a graceful way, instead of direct kill or kill -9 command
* SIGTERM is not a standalone command but a signal, signal number 15
* SIGTERM is used to send to a process to get the process to gracefully terminate
* SIGTERM is used by supplying an argument `-TERM` or `-15` to the kill command, `kill -TERM <PID>` or `kill -15 <PID>`
* The PID is the second value returned from the command, ps aux | grep process_name, `9064` in this instance
* <todo: consider, investigate york-ea+ line as this remains after process termination, don't understand what this is, >
```
$ ps aux | grep dnsmasq
root        9064  0.0  0.0  19664  7492 pts/0    S+   11:04   0:00 sudo dnsmasq --no-daemon --log-queries=extra --log-dhcp --log-debug -C /etc/dnsmasq.conf
root        9065  0.0  0.0  19664  2576 pts/1    Ss   11:04   0:00 sudo dnsmasq --no-daemon --log-queries=extra --log-dhcp --log-debug -C /etc/dnsmasq.conf
root        9066  0.0  0.0  17080  5584 pts/1    S+   11:04   0:00 dnsmasq --no-daemon --log-queries=extra --log-dhcp --log-debug -C /etc/dnsmasq.conf
york-ea+   10200  0.0  0.0   9152  2272 pts/2    S+   11:29   0:00 grep --color=auto dnsmasq

$ SIGTERM 9064
SIGTERM: command not found

$ kill -TERM 9064

$ ps aux | grep dnsmasq
york-ea+   10446  0.0  0.0   9152  2272 pts/2    S+   11:37   0:00 grep --color=auto dnsmasq
```
* The output in the original terminal window where dnsmasq was started as --no-daemon
* The process exits with acknowledgment of SIGTERM process termination
```
dnsmasq: 10 127.0.0.1/5353 forwarded query to 127.0.0.53
dnsmasq: 11 127.0.0.1/5353 forwarded query to 127.0.0.53
dnsmasq: 12 127.0.0.1/5353 forwarded query to 127.0.0.53
dnsmasq: exiting on receipt of SIGTERM
```

View logs
* Use Ctrl+C to exit back to main prompt.
* Ctrl+C appears as `^C` in terminal cli.
```
$ sudo journalctl -u dnsmasq -f
[sudo] password for york-earwaker: 
May 14 10:09:40 york-earwaker-XPS-15-9560 dnsmasq[1933]: read /etc/hosts - 81 names
May 14 10:09:40 york-earwaker-XPS-15-9560 resolvconf[1944]: Dropped protocol specifier '.dnsmasq' from 'lo.dnsmasq'. Using 'lo' (ifindex=1).
May 14 10:09:40 york-earwaker-XPS-15-9560 resolvconf[1944]: Failed to set DNS configuration: Unit dbus-org.freedesktop.network1.service not found.
May 14 10:09:40 york-earwaker-XPS-15-9560 systemd[1]: Started dnsmasq.service - dnsmasq - A lightweight DHCP and caching DNS server.
May 14 10:56:35 york-earwaker-XPS-15-9560 systemd[1]: Stopping dnsmasq.service - dnsmasq - A lightweight DHCP and caching DNS server...
May 14 10:56:35 york-earwaker-XPS-15-9560 resolvconf[8739]: Dropped protocol specifier '.dnsmasq' from 'lo.dnsmasq'. Using 'lo' (ifindex=1).
May 14 10:56:35 york-earwaker-XPS-15-9560 resolvconf[8739]: Failed to revert interface configuration: Unit dbus-org.freedesktop.network1.service not found.
May 14 10:56:35 york-earwaker-XPS-15-9560 dnsmasq[1933]: exiting on receipt of SIGTERM
May 14 10:56:35 york-earwaker-XPS-15-9560 systemd[1]: dnsmasq.service: Deactivated successfully.
May 14 10:56:35 york-earwaker-XPS-15-9560 systemd[1]: Stopped dnsmasq.service - dnsmasq - A lightweight DHCP and caching DNS server.
^C
```

View logs
* Use Ctrl+C to exit back to main prompt.
```
$ sudo tail -f /var/log/syslog | grep dnsmasq
^C
```

For production and service management dnsmasq
* Run dnsmasq in the foreground in the terminal cli to view operations
* $ dnsmasq --keep-in-foreground --conf-file=/path/to/dnsmasq.conf
* <todo: consider, test this, not yet attempted, >
```
$ dnsmasq --keep-in-foreground --conf-file=/etc/dnsmasq.conf
```

/etc/resolv.conf
* suggested change value to 127.0.0.1 of key nameserver 
* Brave Search Leo
* This has not been done, 
* <todo: consider, do this>
* <todo: consider, systemd-resolv conflicts, >

### NetworkManager

```
$ NetworkManager -V
1.46.0
```

### dnsmasq - block a domain name
Several options

Redirect to Null IP
* Failure :( to block address, wip
* Block a domain by resolving it to 0.0.0.0 or 127.0.0.1:
* address=/example.com/0.0.0.0
* add key value below to /etc/dnsmasq.conf file
* key conf-file= value /etc/dnsmasq.d/blocklist.conf 
* restart the dnsmasq service
```
conf-file=/etc/dnsmasq.d/blocklist.conf # ye, was added, 
```
Restart dnsmasq, after the inclusion of the conf-file entry to dnsmasq.conf configuation file above.
* before restarting dnsmasq optionally test the configuration file without starting the service, see elsewhere in this page
* or test the configuration as a first debug step if the dnsmasq service returns errors and does not start
```
$ sudo systemctl restart dnsmasq
```

## References

Terms
* dns, domain name system, 
* dnssec,
* dhcp, dynamic host configuration protocol, 
* ip4, 
* ip6, 
* tftp, [WP](https://en.wikipedia.org/wiki/Trivial_File_Transfer_Protocol), trivial file transfer protocol, udp port 69, unsecure, clear text, LANs, 

Network booting
* bootstrap protocol, boottp
* preboot execution environment, pxe

Lists - catalogues
* Comparison of DNS server software, [WP](https://en.wikipedia.org/wiki/Comparison_of_DNS_server_software)
* Comparison of DHCP server software, 
* ...



