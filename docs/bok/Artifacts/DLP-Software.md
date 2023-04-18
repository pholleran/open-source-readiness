---
title: Data Loss Prevention Software
tags: 
  - Developer (Role)
  - OSPO (Role)
  - Legal (Role)
  - CIO/CTO (Role)
---

This article looks at Data Loss Prevention (DLP) software commonly used in financial organisations and how these impact open source consumption and contribution.  It is not a complete reference for the subject of DLP generally, but should act as a starting point for understanding the issues involved. 

> Data loss prevention (DLP) software detects potential data breaches/data ex-filtration transmissions and prevents them by monitoring, detecting and blocking sensitive data while in use (endpoint actions), in motion (network traffic), and at rest (data storage). - [Data Loss Prevention Software, _Wikipedia_](https://en.wikipedia.org/wiki/Data_loss_prevention_software)

There are three basic types of DLP software, which are worth covering here:

- **Network**: _data in motion_ DLP solutions usually involve Firewalls set up at egress points at the perimeter of the network.  

- **Endpoint**: _data in use_ DLP solutions are installed on an end-user machine (say a laptop or PC) or a server.  

- **Cloud**: Modern enterprises are increasingly turning to the cloud for data storage (_data at rest_) and processing (_data in use_).  This presents another venue for data loss to occur.  

## Firewalls for Network DLP

> In computing, a firewall is a network security system that monitors and controls incoming and outgoing network traffic based on predetermined security rules. A firewall typically establishes a barrier between a trusted network and an untrusted network, such as the Internet.  - [Firewall, _Wikipedia_](https://en.wikipedia.org/wiki/Firewall_(computing))

![Overview of a Firewall](/img/bok/firewall.png)

In a corporate environment such as a bank, there are usually firewalls placed on both _incoming_ and _outgoing_ traffic.  The firewall scans incoming and outgoing data and attempts to set rules about what is and isn't allowed as traffic, much as a security guard can allow or prevent people from entering a building.

_Incoming_ requests from external clients to an organisation's servers (such as requests for web pages, or for delivery of email) are usually routed to machines in the DMZ (or demilitarized zone).   Meanwhile, the _intranet_ contains most of the bank's private hardware including the PCs of the bank's staff.  

Staff connecting from home will usually access the _intranet_ (as though they were in the building) via a [Virtual Private Network (VPN)](https://en.wikipedia.org/wiki/Virtual_private_network).

Sometimes, financial institutions will have further firewalls to divide their network further, say between the general _intranet_ and _production systems_.  A good analogy for this might be a "VIP" area in a night club which has its own security beyond the main front door.

### Filtering / Security

Messages from one machine to another are sent across both the _intranet_ and _internet_ in [packets](https://en.wikipedia.org/wiki/Internet_Protocol).  For messages cross from one to the other, they will have to go through the firewall.

The aim of the firewall is to filter packets as they pass through, only allowing benign packets to pass.  Over time, there has been [considerable evolution in the functionality of firewall technology](https://en.wikipedia.org/wiki/Firewall_(computing)) which we will summarize here:

1.  **Packet-Address Based (1980s-) **. The _address_ component of a networking packet is standard to all networking traffic.  The first firewalls simply maintained a list of allowed destinations for packets to be sent to.   This could be used to prevent staff from accessing a particular web site at a given address.
    
2.  **Connection Based (1990s-)**.  A second generation of firewalls performed more analysis and traced the back-and-forth of packets through the firewall to establish bi-directional packet exchange between two machines (a _connection_).  This allowed policies to be tailored based on _who_ was communicating, and therefore add allow- or deny-lists.

3.  **Deep-Packet Inspection/Next Generation (2010s-)**.  The next step for firewalls was to [inspect the contents of the packets](https://en.wikipedia.org/wiki/Deep_packet_inspection) being sent on the network (made more complex since most content on the internet is now encrypted).  At a simple level, this allows the firewall to be able to filter based on a particular _web page within a site_, or filtering out specific types of action (e.g. `POST`ed data denied but `GET` requests _for_ data are allowed).    

### DLP and Open Source

Internal firewalls have been used as a control for [Data Leakage Prevention (DLP)](../Activities/Level-3/Data-Leakage-Prevention).  By removing access to sites such as [Google Docs](https://docs.google.com), or popular social networking sites, compliance teams are able to remove a certain vector of (mainly accidental) data exfiltration.  

Sites like [GitHub](https://github.com) are often included in deny-lists, since data can be posted to them.  This prevents developers from viewing a large amount of open source software.  

Sites like [StackOverflow](https://stackoverflow.com) (a question-and-answer site for developers) are also often included in deny lists, because they too can have data posted to them, and have a strong social component.  Being unable to access sites like this is a serious impediment to the effective use of open source software.

A workaround for this is that some organisations can use [Deep Packet Inspection Firewalls](https://en.wikipedia.org/wiki/Deep_packet_inspection) to allow GitHub to be viewed either without login, or by denying `POST`ed data on the site (see above).  In many cases, developers have to request access to GitHub (i.e. be added to the _allow list_ for the site) in order to be able to view it at all.

However, anyone _maliciously_ exfiltrating data can send it to _an almost unlimited number_ of destinations on the internet.  This means that tools based on simple allow- and deny- lists are broken:

> Security analysts get fed up with having to manually chase large numbers of false positive incidents that require deep and time-consuming investigations. - [Mediocre DLP Solutions Fall Short on Data Detection, _Palo Alto Networks_](https://www.paloaltonetworks.com/blog/network-security/mediocre-dlp_solutions-fall-short-on-data-detection/)

### Machine Learning

To combat this situation, advanced machine learning is being used for Deep-Packet Inspection in newer tools:

> ... to combat this situation, advanced machine learning is the present and the future of data protection because it makes data identification more accurate and simplifies detection.  [Mediocre DLP Solutions Fall Short on Data Detection, _Palo Alto Networks_](https://www.paloaltonetworks.com/blog/network-security/mediocre-dlp_solutions-fall-short-on-data-detection/)

### Data Fingerprinting

A second technique is to _fingerprint_ the private data within the organisation and use these fingerprints in the firewall to look for private data being exfiltrated:

> In addition, it should leverage Exact Data Matching (EDM) to detect and monitor specific sensitive data, and protect it from malicious exfiltration or loss. Designed to scale to very large data sets, EDM fingerprints an entire database of known personally identifiable information (PII), like bank account numbers, credit card numbers, addresses, medical record numbers and other personal information stored in a structured data source, such as a database, a directory server, or a structured data file such as CSV or spreadsheet. This data is then detected across the entire enterprise, as it traverses the network edge or it is transferred by employees from remote locations. - [A Reliable Data Protection Strategy Hinges Upon Highly Accurate Data Detection, _Palo Alto Networks_](https://www.paloaltonetworks.com/blog/network-security/a-reliable-data-protection-strategy-hinges-upon-highly-accurate-data-detection/)

Here are some tools that support data fingerprinting:

- [Palo Alto Networks]

- [Forcepoint DLP](https://www.forcepoint.com/product/dlp-data-loss-prevention)

## Summary


SIEM / SOAR


https://www.sunnyvalley.io/docs/network-security-tutorials/top-dlp-solutions#what-are-the-best-practices-for-dlp-implementation
