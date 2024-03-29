Device, Application and Service discovery[¶](#Device-Application-and-Service-discovery)
=======================================================================================

Partners Involved in this Theme[¶](#Partners-Involved-in-this-Theme)
--------------------------------------------------------------------

-   **Samsung, TNO**
-   W3C
-   Impleo
-   SEMC
-   ISMB

*Security and privacy contacts: W3C, Impleo, Samsung. SEMC*

Deliverable Structure[¶](#Deliverable-Structure)
------------------------------------------------

[Draft Deliverable Structure](.html)

Meeting[¶](#Meeting)
--------------------

-   Minutes for 22 March Meeting : [DD\_22MarMinutes](.html)
-   Minutes for 30 March Meeting : [DD\_30MarMinutes](.html)

Progress Report[¶](#Progress-Report)
------------------------------------

-   Repotts on 6 April : [30 March - 05 April](.html)

Working definition of Device/Service Discovery[¶](#Working-definition-of-DeviceService-Discovery)
-------------------------------------------------------------------------------------------------

-   Device Discovery definition
    -   [The capability of a device] "to find other devices and maintain
        that connectivity within the same network". [1]
    -   "Device Discovery [...] is a service using which a device can
        detect all its neighbors and make its presence known to each
        neighbor in the network." [2]
    -   *(Bluetooth-specific)* "A process that allows one device to
        detect another device." [3]
    -   *(Bluetooth-specific)* "A procedure for retrieving the Bluetooth
        device address, clock, class-of-device field and used page scan
        mode from discoverable devices." [4]
    -   *(ZigBee-specific)* "Device Discovery involves interrogating a
        remote node for address information." [5]

A High-level definition might be: "A mechanism that allows a device to
discover other locally or remotely available and discoverable devices
through any of the supported networking technologies, possibly based on
one or more predefined criteria, in order to obtain addressing
information that's needed to establish a connection with it.”

High Level Architecture[¶](#High-Level-Architecture)
----------------------------------------------------

A very high level architecture/interaction of different components
involved in the webinos device and service discovery. [Device Discovery
High Level Architecture](.html)

At the moment application discovery is not included as it might prolong
discovery process.

Functional/API model[¶](#FunctionalAPI-model)
---------------------------------------------

An initial investigation on [mNDS/DNS-SD](.html)

State-of-the-art Technologies[¶](#State-of-the-art-Technologies)
----------------------------------------------------------------

  ------------------------ --------------------------------------- ----------------------------- ------------------------ ------------------------- --------- ---------
  Technologies             Analysis                                Network structure             What does it discover?   Local/Remote discovery?   Lead      Status
  UPnP                     [UPnP Information](.html)               Control Point                 Device & service         Local                     Samsung   Done
  Zero config              [ZeroConfig](.html)                     Peer-to-peer/ control point   Device & service         Local                     Samsung   Done
  XMPP                     [XMPP for discovery](.html)             Peer to peer/Control point    Device&Service           Local/Remote              ISMB      Done
  Web Introducer           [Web Introducer investigation](.html)   Control point                 Service                  Remote                    SEMC      Done
  WebFinger                [WebFinger](.html)                      Control point                 Application              Remote                    SEMC      Done
  Distributed Hash Table   [Distributed Hash Table](.html)         P2P                           Peers                    Both                      Samsung   Ongoing
  ------------------------ --------------------------------------- ----------------------------- ------------------------ ------------------------- --------- ---------

Scoping statement[¶](#Scoping-statement)
----------------------------------------

-   Discovery Mechanisms based on certain criteria to obtain addressing
    information
-   Device, service, application to expose their availability,
    capability, status & event to the network
-   Descriptions of device, service & application
-   Security & Policy issues related to accessing control

Work Status[¶](#Work-Status)
----------------------------

  -------------------------------------------- --------------------------------------------------------------------------------------------------------------------------
  **Work Area**                                **Status**
  State of art analysis for device discovery   Done
  Use Case relevant for device discovery       Pending - Nick Input required, Samsung proposal [source:WP5.1.pptx](/redmine/projects/wp3-1/repository/entry/WP5.1.pptx)
  Device discovery architecture                Defined
  Functional API                               Done - Local discovery, WebIntroducer, Remaining - Remote Discovery, WebFinger
  Addressing and Naming                        Ongoing, [Addressing and Naming](.html)
  Elaborate Application Discovery              Ongoing, TNO looking into it
  -------------------------------------------- --------------------------------------------------------------------------------------------------------------------------

Collaboration with other groups:[¶](#Collaboration-with-other-groups)
---------------------------------------------------------------------

-   User ID Management, Overlay Network, and Context Management
    -   Overlay network for discovery mechanism effect
    -   Context management to know about proximity
    -   UserId Management: how to address devices and store them online
        and locally.
-   Security and policy issues
    -   To specify discovery process and propose solutions

Issues[¶](#Issues)
------------------

-   ~~Naming~~ Naming **and addressing**:
    -   Resolve IP address using DHCP address, if no address found
        resolve using mDNS or AUTO IP mechanism.
    -   (Auto-)create sensible names for users and devices

<!-- -->

-   Discovery Decision
    -   Local
    -   Remote
    -   Physical/Close proximity
    -   Social Proximity

<!-- -->

-   Device Discovery
    -   Pointer to find properties of device (URL)
    -   Device ID (Unique ID)
    -   Device Type
    -   Mapping between User ID and Device ID - As part of
        authentication
    -   Advertise availability in form of alive, update (change in
        device situation), bye bye
    -   How to discover device DNS Query (Bonjour) or SSDP or XMPP

<!-- -->

-   Device and Service Description\
    Once device is discovered, next step is to find more about the
    device, each embedded system supported in device and services
    provided by each embedded systems. Message can be either multicast
    or unicast depending on architecture, in central architecture,
    unicast mechanism is feasible but in peer to peer multicast appears
    more appropriate.
    -   Root device, each embedded system in device, and services
        provided by each embedded system of device
    -   To include information about service, way to access service,
        service variables.

Requirements[¶](#Requirements)
------------------------------

  ------------------------------------ ------------------------------------
  **Requirement**                      **Area investigating this issue**

  **Device, application, and           Includes local and remote connected
  services**                           device.

  - Identification\                    User identification
  - Assigned address\                  
  - Scope of address\                  
  - Address resolution                 

  - Advertise                          Device, Service and Application
                                       discovery

  - Capabilities/Descriptions          Device, Service and Application
                                       discovery

  - Context information                Context Management

  - Availability                       Device, Service and Application
                                       discovery

  - Close proximity                    Device, Service and Application
                                       discovery

  - Physical location                  Device, Service and Application
                                       discovery

  - Social proximity                   Context Management

  - Other devices of same user         User data management

  - Other users devices and service    User Data Management

  **Device**                           

  - Status of device\                  Device, Service and Application
  - Identify event in device           discovery

  **Service**                          

  - Install software to work with new  This issue is platform
  service                              implementation issue

  **Application discovery**            

  - Each instance separately           This issue is platform
  addressable                          implementation issue
  ------------------------------------ ------------------------------------

Security & policy issues[¶](#Security-38-policy-issues)
-------------------------------------------------------

Few identified mentioned, [Security
Issues](/t3-5/wiki/WP31_Mirror_ApplicationDiscovery)

References[¶](#References)
--------------------------

[1] [Develop P2P applications with device discovery
technologies](http://www.ibm.com/developerworks/architecture/library/wi-peerapp/index.html)
(IBM)\
[2] S. I. Ahamed, M. Zulkermine and S. Anamanamuri, "A Dependable Device
Discovery Approach for Pervasive Computing Middleware", *IEEE
Proceedings of the First International Conference on Availability,
Reliability and Security (ARES '06)*, 2006\
[3] [Bluetooth glossary of terms](http://support.apple.com/kb/HT3894)
(Apple)\
[4]
[Glossary](http://www.bluetooth.com/English/Technology/Pages/Glossary.aspx)
(Bluetooth SIG)\
[5] [Device and Service
Discovery](http://www.jennic.com/elearning/zigbee/files/html/module6/module6-7.htm)
(Jennic)\
[6] [Zeroconf/UPnP
comparison](http://www.zeroconf.org/ZeroconfAndUPnP.html) (ZeroConf)

