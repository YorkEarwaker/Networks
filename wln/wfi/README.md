# Wifi wfi

Wireless local area networks based on the IEEE 802 standards and protocol stack

## Notes

Objectives
* OS environments for AGW project

## Status
TODO
* <todo: consider, new install of Ubuntu 24.04 on rpi-z2w no wifi only access via serial bridge chip and screen session, get wifi working as only means for internet access >
* <todo: consider, eathernet breakout board to connect direct to router local area network as initial work around, use seperate /eth ethernet sub project in networks repo >
* <todo: consider, clean up mess from AI suggestions from 8 October 2026, /etc/modprobe.d/cfg80211.conf 'options cfg80211 ieee80211_regdom=GB'  /etc/default/crda 'REGDOMIN-GB' >

DONE
* <done: intent to commit>

## Libs

Standards
* ISO/IEC 8802.11, IEEE 802.11x [WP](https://en.wikipedia.org/wiki/IEEE_802.11), wifi standards and protocols

## References

Terms
* IEEE 802 [WP](https://en.wikipedia.org/wiki/IEEE_802), osi model, 
* WiFi [WP](https://en.wikipedia.org/wiki/Wi-Fi), wireless lan protocols base on 802.11 standards


Docs - ubuntu, linux
* Official Linux Wireless documentation, [WS](https://wireless.docs.kernel.org/en/latest/index.html), wireless docs kernel
* Netplan documentation, [WS](https://netplan.readthedocs.io/en/0.106/)
* Canonical Netplan, [WS](https://netplan.io/), overview
* Configure Wi-Fi connections, [WS](https://documentation.ubuntu.com/core/explanation/system-snaps/network-manager/how-to-guides/configure-wifi-connections/), ubuntu core, 
* NetworkManager
* Systemd-networkd

News Papers
* How to Configure WiFi from the Command Line on Ubuntu Server, [WS](https://oneuptime.com/blog/post/2026-03-02-configure-wifi-command-line-ubuntu-server/view), 02 March 2026, Nawaz Dhandala, OneUptime, Learn how to configure WiFi connections from the command line on Ubuntu Server using Netplan and NetworkManager, including WPA2 authentication and static IPs.

