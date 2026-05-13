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
```
$ sudo dnsmasq --test
dnsmasq: syntax check OK.
```

Restart dnsmasq
```
$ sudo systemctl restart dnsmasq
```

Status of dnsmasq service
* Success! at least in part
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



