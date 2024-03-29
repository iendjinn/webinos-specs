XMPP for discovery[¶](#XMPP-for-discovery)
==========================================

Abbreviations[¶](#Abbreviations)
--------------------------------

  ----------------- ------------------------------------------------------------------------------------------
  Abbreviation      Description
  Ad-Hoc Commands   Application-specific commands (see [XEP-0050](http://xmpp.org/extensions/xep-0050.html))
  IETF              Internet Engineering Task Force
  IP                Internet Protocol
  JID               Jabber ID
  NAT               Network Address Translator
  PubSub            Publish-Subscribe (see [XEP-0060](http://xmpp.org/extensions/xep-0060.html))
  RFC               Request For Comments
  RPC               Remote Procedure Call
  SASL              Simple Authentication and Security Layer
  TLS               Transport Layer Security
  XEP               XMPP Extension Protocol
  XML               Extensible Markup Language
  XMPP              Extensible Messaging and Presence Protocol
  ----------------- ------------------------------------------------------------------------------------------

Introduction[¶](#Introduction)
------------------------------

This document investigates the possibility of using XMPP to implement an
RPC-like mechanism in the context of device/application/service
discovery for remote discovery requests, i.e., establishing a
communication channel and exchanging data between a device delegating
discovery to another entity that returns back the results of such
operation.

In this document, we will also look at the existing implementations. As
the starting point, we define a typical use case. Based on the use case,
we will cover the following areas:

1.  Candidate solution using XMPP
2.  Gap Analysis between the proposed solution with Discovery
    requirements of WebinOS
3.  Proposals to fill the Gap found in 2.

The output of this document shall contribute to architecture design,
also w.r.t. the "event handling" and "overlay networks" areas.

Requirements[¶](#Requirements)
------------------------------

It is possible to summarize the desired functionality of the remote
discovery process by the following high-level requirements:

-   It SHALL be possible for a Webinos-enabled device to ask another
    Webinos-enabled device, whether in the same network or not, for
    device/application/service discovery results, if the former device
    is authorized and the latter offers this service. (one-shot
    discovery)
-   It SHALL be possible for a Webinos-enabled device to ask another
    Webinos-enabled device, whether in the same network or not, to
    report device/application/service discovery information as soon as
    this information is generated and/or available, if the former device
    is authorized and the latter offers this service. (continuous
    monitoring)

Work Scenarios - Use cases[¶](#Work-Scenarios-Use-cases)
--------------------------------------------------------

Description: The user wants to access data and/or device features
offered by some device in his home network while he is away (e.g., get
the temperature from a heat sensor). The device he/she uses is not
directly connected to the home network.

### Pre-conditions[¶](#Pre-conditions)

-   A device in the home network offering remote discovery is connected
    to a remote XMPP server and its JID is known.

### Flow[¶](#Flow)

1.  If not already connected, the user's current device connects and
    performs login to a remote XMPP server (need not to be the same as
    the device in the home network).
2.  If the JID associated to the device in the home network is not
    present the operation fails.
3.  A discovery request in the form of a XMPP message of some kind
    (e.g., chat message, ad-hoc command) along with discovery criteria
    is sent to the XMPP server the current device is connected to, with
    destination specified as the JID of the device in the home network
    and source specified as the JID associated to the current device.
4.  If there are two different XMPP servers involved, the server the
    current device is connected to forwards the message to the server
    the device in the home network is connected to.
5.  The XMPP server the device in the home network is connected to
    forwards the message to the device in the home network (this is
    possible even if the device in the home network has no public IP
    address, since the connection was established by that device - in
    this case, the destination IP address will be that of the NAT in
    this "transaction", and the NAT will let the packet(s) go through
    since there is already a connection).
6.  The device in the home network sends a response message with results
    to the XMPP server it is connected to with destination specified as
    the source in the request message and source specified as its JID.
7.  The XMPP server(s) forward the message as before in the other
    direction, etc. (a communication channel is established).
8.  Any further communication between the current device and the
    discovered devices in the home network is done through the device
    providing discovery, since returned addresses may not be valid
    outside of that network.

This use case is deliberately simplicistic and does not address
security/authorization issues. It is only meant to show how XMPP can be
used to exchange data among entities in different networks that may not
have public IP addresses in a concrete scenario.

Candidate technology[¶](#Candidate-technology)
----------------------------------------------

As already outlined in the previous section, XMPP could help in remote
discovery by creating a communication channel between the requesting
device and the device acting as a discovery proxy, providing a clean way
to do NAT traversal and “address translation” (i.e., no public IP
address required).

### XMPP[¶](#XMPP)

#### Technical Details[¶](#Technical-Details)

-   Formerly known as Jabber, XMPP is an open, decentralized and
    extensible protocol for near-real-time XML data exchange, is backed
    and formalized by IETF (RFCs 3920-3923, 4854, 4979, 5122) and
    further developed by the [XMPP Standards
    Foundation](http://xmpp.org/). In particular, the XMPP Standard
    Foundation has developed a series of extensions to the protocol,
    known as XEPs, that address quite a significant number of concrete
    applications beyond the scope of the core protocol.
-   The use of XMPP inside Webinos is being considered in several
    different areas, since it seems to offer concrete solutions to a
    significant number of problems that we are facing. Furthermore,
    several mature implementations are already available, some of which
    are open source and Javascript-only, and also its decentralized and
    extensible design should be attractive for our purposes, also w.r.t.
    future and/or unforeseen developments.
-   The protocol is decentralized in the sense that there is no central
    authoritative server. Instead, domain names (or IP addresses) in
    JIDs are used in a similar fashion to e-mails to refer to servers.
-   A typical message delivery scenario between two entities involves
    four actors: the two said entites and the two XMPP servers they are
    connected to (or just one server if they both are connected to the
    same server). The message is routed from the sender entity to the
    XMPP server it is connected to, then to the server the other entity
    is connected to and, eventually, to the receiving entity. However,
    it is possible to also have other means of exchanging data, e.g.,
    serverless using
    [XEP-0174](http://xmpp.org/extensions/xep-0174.html).
-   Typically. when a client connects to a server, it goes through an
    authentication procedure based on SASL and the traffic is encrypted
    using TLS.
-   Two of the most important XEPs are [XEP-0060:
    Publish-Subscribe](http://xmpp.org/extensions/xep-0060.html), that
    is a protocol enabling "entities to create nodes (topics) at a
    pubsub service and publish information at those nodes", so that "an
    event notification (with or without payload) is then broadcasted to
    all entities that have subscribed to the node", and [XEP-0050:
    Ad-Hoc Commands](http://xmpp.org/extensions/xep-0050.html), that is
    a "protocol extension for advertising and executing
    application-specific commands, such as those related to a
    configuration workflow".
-   Messages exchanged via XMPP are in XML format. The core protocol
    specifies three message types: "presence" that carry user presence
    information, "message" used for instant messaging, and "iq" that
    stands for info/query (often used by extensions to define more
    message types).

#### Gap Analysis & Proposals[¶](#Gap-Analysis-38-Proposals)

-   The following proposals are valid under the assumption that a
    certain "protocol" for requesting remote discovery is previously
    defined (i.e., syntax and semantic of request and response
    messages) - in a sense, this could be considered as the first gap.
-   The actual implementation, whether XMPP-based or not, is probably
    going to be based on the outcome of event handling and overlay
    networks areas, hence the whole issue might very well be hidden to
    the discovery area developers, yet the choices behind the underlying
    implementation in such areas will probably have consequences w.r.t.
    the architectural design of the discovery mechanisms as well, thus
    they should take these issues into account.

  --------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Requirement           Gap                                                                                                                                                                                                                    Proposed Solution
  DA-DEV-SEMC-001       Availability and capabilities should be propagated by the device in the local network to authorized and interested remote listeners                                                                                    The device in the local network could publish the information to one or more PubSub nodes on the XMPP server it is connected to, which in turn would deliver it to authorized and interested listeners efficiently
  DA-DEV-SEMC-002       A way for a device to specify interest towards certain remotely discoverable entities should be provided, and the device in the local network shall indicate to the requesting device how to obtain that information   An ad-hoc command could be provided by the device in the local network for remote devices to specify interest towards a certain class of discoverable entities, whose response would be a reference to the resource that will provide the requested information (e.g., PubSub node)
  DA-DEV-SEMC-004       Propagation of availability information both in case of continuous monitoring or one-shot discovery                                                                                                                    As in DA-DEV-SEMC-001 for continuous monitoring, while in case of one-shot discovery the requested information could be transmitted by a single response message of some kind (e.g., result of an ad-hoc command)
  DA-DEV-SEMC-005       Transfer of discovery request and results from/to the device in the local network and the remote devices                                                                                                               This is pretty much covered by the use case described in this document; a (set of) ad-hoc command(s) could be used for this purpose, where the remote device communicates discovery criteria to the device in the local network and gets back the results
  DA-DEV-SEMC-008       In case of remote requests, propagation of information                                                                                                                                                                 The gaps and proposed solutions already outline should suffice in this case
  DA-DEV-FHG-005        The part of the route due to the XMPP layer should be added to the total route                                                                                                                                         The route shall consist of: sub-route from current device to XMPP server it is connected to, sub-route from the latter to the XMPP server the other device is connected to, sub-route from the latter to the other device (discovery proxy), sub-route from the latter to the discovered/remote device
  DA-DEV-ISMB-001       Propagation of information and association of the discovered addresses to the discovery proxy                                                                                                                          As before, plus the addresses of the discovered entities should be associated to the address of the device in the local network (discovery proxy) for further communication - the discovery proxy should act as a generic traffic proxy between the discovered and the requested entity (traffic could be tunneled into, e.g., ad-hoc commands or chat messages)
  DA-DEV-ISMB/FHG-005   As before                                                                                                                                                                                                              As before
  --------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

#### Conclusions[¶](#Conclusions)

XMPP can provide a good underlying mechanism, both complexity- and
efficiency-wise, to perform remote discovery, in particular w.r.t. NAT
traversal and lack of public IP addresses. The amount of gaps to be
filled is not overwhelming and most of the issues, especially the most
fundamental and lower level ones, are going to be tackled by developers
operating in other areas.

However, in any case, a relevant portion of remote discovery-specific
code needs to be written, whether XMPP will be chosen or not.

