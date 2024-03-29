Addressing and Naming[¶](#Addressing-and-Naming)
================================================

This section talks about different addressing mechanism used by
different technologies which are relevant to discovery mechanism. It
tries to conclude how to map user id with different device ids.

Assumptions:[¶](#Assumptions)
-----------------------------

1.  Device such as BT or WiFi uses broadcast mechanism to indicate about
    their presence. If user does not know which device to connect to,
    this is the only mechanism possible.
2.  Each webinos device will have a database and can store information
    about user devices. Devices which are offline will get updated when
    they are connected and have access to webinos cloud. If device
    cannot go online, it can try accessing information from other peers.
3.  At start of webinos system, the information about the user devices
    are hold in form of structure by WRE (Webinos runtime Environment)
    and these information will be used by discovery mechanism to connect
    to those devices only.
4.  Local connectivity devices such as WiFi, BT, and USB have first
    connection establishment based on MAC address, (In case of USB it is
    of this form:Vendor:Product:Serial. It is somewhat similar to MAC
    address.)
5.  After connecting on MAC layer they try connecting at IP layer. The
    applications used by OS tries to assign IP address after WLAN is
    connected to AP, it is not part of WLAN but done in order to provide
    IP connectivity to user. BT and USB can also run IP network on top
    after getting connected, so they are also IP connectible.
6.  Devices that will be communicative in webinos system, should be IP
    addressable.
    (To make it IP addressable is part of discovery mechanism but for
    user to communicate over BT, it should be IP addressable and not
    deal with the MAC address of devices.)

Scenarios:[¶](#Scenarios)
-------------------------

1.  Registered device, which can be looked in some database (online or
    local) and information can be retrieved about the device owned by
    the user.
2.  User connects device for first time, in this scenario if device is
    connected to public IP network it should be registered with webinos
    cloud and if user is connected locally it should be stored in local
    database. It can try sending information to already connected
    devices about new devices. It will be unicast communication.
3.  User wants to connect to friend device. It will involve discovery
    through
    broadcast mechanism
    in local scenario (how to enforce policy in local scenario)and in
    cloud scenario it could use web finger to fetch user friend devices
    and connect to one which are connectible. Devices available through
    web finger should allow to specify which are allowed to be seen by
    friends. (Policy enforcement)

Security Aspect:[¶](#Security-Aspect)
-------------------------------------

Authentication with device is required (PS-USR-Oxford-26) and quite
necessary as it is only way of verifying before providing access to list
of user devices and connecting to them.

Identities description:[¶](#Identities-description)
---------------------------------------------------

Below sections described different identities used by three different
discovery mechanism that will be used:

1.  Local Discovery
2.  Local Connectivity
3.  Remote Discovery

Local Discovery[¶](#Local-Discovery)
------------------------------------

These section describes, ZeroConf and UPnP addressing mechanism. It uses
multicast mechanism to assign proper link local address and then uses
multicast address to find information about the services offered by
device.

### ZeroConf[¶](#ZeroConf)

-   MAC Address
-   Type:\_workstation.\_tcp
-   Domain:local/remote

These information are provided by ZeroConf discovery mechanism. It
includes information about finding more information about services
offered by device. It resolves information from multicast DNS and DNS
service discovery mechanism.

ZeroConf devices have IP address through which they can be communicated
and MAC address which can be used to identify it as a user device.

### UPnP[¶](#UPnP)

-   Device Type: urn:dmc-samsung-com:device:SyncServer:1
-   UDN: uuid:35ca43df-f9d7-4550-9d8e-4aca0a4d2da0
-   Friendly Name: WS-0915A

Other details include information about manufacturer, URL, and other
details as per UPnP specification. Required information for UPnP
connection is to retrieve about services as specified in service URL.

UPnP UDN and device type could be used to identify device as a user
device. The UPnP device are IP addressable, so the communication can
happen over IP with these devices.

Local connectivity[¶](#Local-connectivity)
------------------------------------------

It uses MAC address to connect to each other, along with some security
mechanism. BT and WiFi uses radio interface and all the communication is
over the air and can be sniffed. Only way to guarantee is using an
encryption mechanism to communicate with these devices.

Issue: MAC address could be changed by some hacks. This is inevitable if
user does himself he should follow process of registration of device.

### Bluetooth[¶](#Bluetooth)

Identification : MAC Address\
Device Name: Could change\
Categories: Phone/Printer

BT discovery provides information mentioned above. As MAC address are
supposed to be unique, it could be used as an identity parameter for the
device. It can make use of PAN profile to be IP addressable.

### WiFi[¶](#WiFi)

Identification: MAC Address\
SSID: Could be changed.

WLAN AP sends beacon information which is broadcast message which
includes information about SSID, Channel number, and other related
details telling client about requirements to connect to AP. It also
includes information about if AP supports WPA/WPA2.

First step, is selecting the AP user wants to connect. It could be
either user selected or information is hold in a file by OS, which is
used by device while starting up to connect to user selected AP or
already connected AP. (same in MAC, iPhone, and Android as they all use
open source wpa\_supplicant). After devices exchange authentication,
association, and 4 way handshake mechanism. AP and client are connected
to each other, then DHCP is used to get IP address. If no IP address is
assigned, it uses link local address.

Common way to hide information is to use hidden AP. Device does not
broadcast its SSID through beacons and thus is not searchable, it can be
only connected if user knows the device MAC address and connect to such
device. It is not that common to have this mechanism.

### USB[¶](#USB)

-   Vendor ID
-   Product ID
-   Serial Number: changes as you plug in and plug out device to
    different points on device.

Combination of Vendor Id and product id are supposed to be unique, but
they are not quite unique as some vendor do not follow rules. [USB Over
IP](http://usbip.sourceforge.net/) is a way to access devices remotely
that are connected using USB.

Remote Discovery mechanism.[¶](#Remote-Discovery-mechanism)
-----------------------------------------------------------

This is separate from local discovery and connectivity as here it is not
a mac address but devices communicate with remote node using IP address
of node. Below mechanism are applicable for local discovery too but will
make local infrastructure of webinos system quite complex.

### XMPP[¶](#XMPP)

-   JID: Unique Identifier
-   Password:

These fields are use while authenticating with XMPP server. XMPP server
then presents the user to see other user JID's status and then p2p
communication establishment is done.

### DHT[¶](#DHT)

-   NodeId: NodeId that is generated from keyspace.
-   Port number:

These details are used to find other nodes in DHT network. Each request
is sent to nearest node id and based on the query message is forwarded
to nearest node until it reach its destination.

### WebFinger[¶](#WebFinger)

-   Email
-   User Information Links

Conclusion:[¶](#Conclusion)
---------------------------

Each technology has its own way of addressing. What is required is
mapping between webinos id and different devices.

Mapping between webinos identity and different device identities.

Suggestion:

1.  Each device should be registered and information to be present in
    local database and in webinos cloud.
2.  Target should be IP addressable devices, only unique entities in
    these are USB and BT. Which require something running on top to
    exchange messages.

User's webinos id should map to these unique identity to find devices.

  ------------ --------------------- ---------------------------------------------------------------------------
  Technology   Unique Identity       IP Address connection possible
  ZeroConf     MAC Address           Yes (Link Local)
  UPnP         UDN and Device type   Yes (AutoIP)
  WiFi         MAC Address           (IP address or Link local usually retrieved from DHCP server)
  BT           MAC Address           If PAN profile is used IP connectivity is possible
  USB          VendorID:ProductID    MTP profile allow access to IP network
  XMPP         JID                   IP addressable
  DHT          NodeID                IP addressable
  WebFinger    UserID                It just provides information, IP address connectivity already established
  ------------ --------------------- ---------------------------------------------------------------------------


