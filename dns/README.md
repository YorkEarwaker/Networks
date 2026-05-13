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
* systemd-resolved, fully featured dns resolver service, in Ubuntu v16 replaced resolvconf### Services

Proprietary
* OpenDNS, upstream filtering/resolution, US
* ICAN?
* Whois? 

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
Use dnsmasq to block domain names, maintain sanity in a world driven made by the compression of time and space by social transition from analogue to digital.
* I preferred the world when there were only analogue telco landlines

## Output
Examples of how to use dns and dhcp tools 
* <todo: consider, black list, blocked, heading example, >
* <todo: consider, white list, permitted, heading example, >

### block a domain name


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
