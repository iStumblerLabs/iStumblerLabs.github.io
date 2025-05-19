---
layout: post
title: Wi-Fi’s Service Discovery Problem
tag:
- wifi
- service-discovery
- internet
---

## Wi-Fi’s Service Discovery Problem

Picture yourself in a conference room; you are a visitor here, sitting in front of a laptop looking at a document that you need to send to your host, who works here. You host needs to review the document before sending it on for approvals. There is a lot of money hanging on these approvals and you are anxious to get the document reviewed.

It’s not a huge file, but it’s not small either, too big for email, let’s say a whopping 100 Mb. And it just so happens that the internet connection in this conference room is slow, very slow something like 100 Kb/s, even if you could upload the file to a sharing site your host will have to download it again, taking twice as long…

The good news? Both your laptop and your hosts are equipped with the latest Wi-Fi and Bluetooth radios. Bluetooth won’t help you much, since it’s not fast enough to transfer the file in a reasonable amount of time, but if you have recent laptops you should be able to get more than a gigabit per second using the Wi-Fi Radios.

#### **Bonne Chance!**

Assuming that you and your host have some way to share files locally, and that both the client and server are on the same network, all we need to connect is to figure out what network addresses to use. Thankfully there are standards for doing this. And the beautiful thing about standards is that there are so many to choose from:

*   [Bonjour](https://en.wikipedia.org/wiki/Bonjour_%28software%29), based on the [IETF](https://www.ietf.org) [mDNS](https://tools.ietf.org/html/rfc6762) and [DNS-SD](https://tools.ietf.org/html/rfc6763) RFCs, promoted and branded by Apple
*   [UPnP](https://en.wikipedia.org/wiki/Universal_Plug_and_Play), based on, uh, Microsoft stuff, I guess, promoted by the [Open Connectivity Foundation](http://openconnectivity.org) (totally not a standards group)
*   [SLP](https://en.wikipedia.org/wiki/Service_Location_Protocol) an older IETF RFCs, now considered more or less obsolete

Here we have our first problem: Windows and MacOS implement two different protocols, and neither implements the other. Android implements both natively but doesn’t provide it’s own browser or basic set of tools so you’ll need to find an app to complete our proposed file transfer.

#### Administrative Denials of Service

Provided you’re lucky enough to have two devices that _can_ discover each other, they then have to be on the same network to use any of the service discovery protocols we’ve discussed so far. More specifically, they need to be in the same [broadcast domain](https://en.wikipedia.org/wiki/Broadcast_domain) so that service discovery messages can be heard by other devices. Broadcast domains typically extend across an entire Wi-Fi [SSID](https://en.wikipedia.org/wiki/Service_set_(802.11_network)) or IP [Subnet](https://en.wikipedia.org/wiki/Subnetwork). However most business guest and internal Wi-Fi networks are “separate but equal” networks, with guest not allowed to connect to the internal network.

Even if both laptops join the guest network many enterprise Wi-Fi networks provide a “[client isolation](http://security.stackexchange.com/questions/16751/wireless-client-isolation-how-does-it-work-and-can-it-be-bypassed)” or “[multicast filtering](http://superuser.com/questions/730288/why-do-some-wifi-routers-block-multicast-packets-going-from-wired-to-wireless)” mode which prevents clients on the network for talking to each other, which prevents service discovery from happening.

#### Screw It, We’ll Go Direct

Clearly this is a bad situation: two laptops sitting right next to each other on a table which have an array of communications tools but can’t talk to each other, even if they are compatible, due to the network configuration. Unfortunately it’s not uncommon, so the [Wi-Fi Alliance](https://en.wikipedia.org/wiki/Wi-Fi_Alliance) (WFA) got together and developed the [Wi-Fi Direct](https://en.wikipedia.org/wiki/Wi-Fi_Direct) specification which allows Wi-Fi Devices to connect to each other without the Access Point getting in the way.

The earliest Wi-Fi Direct devices shipped in 2011\. Apple, at about the same time, developed [AirDrop](https://en.wikipedia.org/wiki/AirDrop) and released it in [MacOS 10.7](https://en.wikipedia.org/wiki/Mac_OS_X_Lion). So, once again we have a platform divide: MacOS devices can connect directly (but not with iOS, for a few more years) but AirDrop doesn’t interoperate with Wi-Fi Direct and now we have Apple on one side and Everybody Else on the other. Again.

#### Now What?

Without a cross-platform story Wi-Fi Direct has had lackluster success, and the WFA has not taken the time to specify the IP networking environment for Wi-Fi that would make existing IP service discovery protocols work. They have added a new and exciting twist with [Wi-Fi Aware](http://www.wi-fi.org/discover-wi-fi/wi-fi-aware) which overlaps with Wi-Fi Direct in scope and functionality, and allows for pre-association advertising and discovery of services (which Wi-Fi Direct also supports) and then connection to an Infrastructure, IBSS, P2P or Mesh Wi-Fi network on which the application can do further service discovery to get an IP address and finally connect for application layer traffic to flow.

While it’s not unusual for WFA to publish a specification like this, the situation is clearly fraught. While the industry players shuffle for dominance in the service discovery and connectivity market, users are left with the simple and apparently insoluble problem: “Why can’t I connect to the device right next to me?”
