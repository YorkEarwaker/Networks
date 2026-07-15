# Voice over IP vip

Telephone calls using internet protocol stack. Also know as; VoIP, IP telephony, softphone, .

## Notes

Objectives
* communicate with family and friends
* communicate with co workers
* for use in AGW project coms deliverables

Functional requirements
* SIP compliant?
* other?

## Status
TODO
* <todo: consider, research candidate client software, >
* <todo: consider, make first call, >
* <todo: consider, barsip for RPi Z 2 W, embedded, further research for preferred embedded client, >
* <todo: consider, Jitsi for Debian development workflows>
* <todo: consider, Linphone for PBX client interface, >
* <todo: consider, Jami for P2P serverless, >
* <todo: consider, collate functional requirements for client software, > 
* <todo: consider, use case list for cleint software, see objective under notes in first instance, >
* <todo: consider, mobile telephony use of voip, 4G, 5G, >

DONE
* <done: consider, intent to commit, >
* <done: consider, server solution low priority at the moment 2026.07.15, future use case for AGW project a must have, >

## Libs
VoIP, video conferencing systems, voice, video, text

Client 
* Jami, foss, P2P, private, surveillance resistant, serverless, group calls poor, 1 to 1 calls good, 
* Jitsi, [WS](https://jitsi.debian.social/), foss, Debian social, used by Debian developers, YouTube dependency?, hundreds of users on group calls
* Linphone, foss, Belledonne Communications, SIP, PBX, SRTP, TLS, Qt/MQL console, cross platform, enterprise class, white label deployment
* Twinki, SIP, PBX, 
* Ekiga, SIP, H.323, Gnome desktop, toward older kit, 
* barsip, SIP, embedded
* ...

Server
* Asterix, PBX platform, SIP end point handling, voicemail, IVR, PSTN gateways, 
* FreePBX, web based admin interface over Asterix, 
* FreeSwitch, high performance telephony platform, high volume call switching, 
* Mumble, Murmur, uses Opus codex for high quality audio, gaming, community groups, 
* ...

## References

Terms
* VoIP
* Codec, encoding voice and video data, media packets
* Signaling protocol
* Media protocol
* Network protocol

Standards - voip, functional requirement candidates 
* SRTP encryption, media
* E2EE end to end encryption, 
* P2P, peer to peer
* PBX, 
* STUN, Session Transmission Utilities for NAT, IETF, RFC; 3489, 5389 .
* TURN, Traversals Using Relays around NAT, IETF? 
* ICE, Interactive Connectivity Establishment, IETF? 
* NAT, Network Address Transmission, 
* SFU, 
* DHT, 
* ...

Signaling protocol - including internet protocol suite,
* SIP, Session Initiated Protocol, application layer, 
* SCCP, Skinny Client Control Protocol, Cisco, proprietary, 
* H.323, 

Media protocol - including internet protocol suite, 
* RTP, Real-time Transport Protocol, application layer, over UDP, transport of audio and video codec encoded data, media packet, 
* RTCP, Real-time Transport Control Protocol, statistical data about call quality, sibling protocol to RTP, 

Network protocol - including internet protocol suite, 
* TLS, Transport Layer Security, application layer, encryption, signaling, IETF
* TCP, Transmission Control Protocol, transport layer, IETF 
* UDP, User Datagram Protocol, transport layer, IETF

News Papers - voip
* An introduction to VoIP for sysadmins, [WS](https://www.redhat.com/en/blog/introduction-voip), 7 January 2020, RedHat, 
