Discovery[¶](#Discovery)
========================

Scope:

The Webinos discovery involves two major steps: to find other PZPs and
to find webinos services provided by the found PZPs. This section only
focuses on the process of finding other PZPs. Security and privacy
issues related to the PZP discovery are not covered.

1. Introduction[¶](#1-Introduction)
-----------------------------------

Webinos PZP discovery defines interfaces and procedures to allow
automatic detection of PZPs in other devices, within or outside personal
zone, via local or remote connections.

From webinos discovery API point of view, PZP is treated as a service of
webinos. It is, however, different from other Webinos services. PZP
provides the functionality of hosting and managing other webinos
services.

This section outlines PZP discovery process in three steps

-   PZP registration and advertisement
-   Querying or finding other PZPs based on certain criteria
-   Binding with discovered PZPs

Facing the challenges of a wide variety of discovery protocols used
these days due to multiplicity of networking technology and various
working scenarios introduced by webinos personal zone concept, webinos
PZP discovery aims at providing a generic PZP discovery interface for
web developers in all circumstances.

Descriptions of each of these steps are associated with two discovery
approaches based on the network availability:

-   PZH assisted PZP discovery. This requires the availability of
    network connections between PZPs and their PZHs, and between PZHs if
    cross-zone PZP discovery happens.
-   Direct PZP discovery. It refers a direct discovery conversation
    between PZPs. Various existing discovery mechanisms can be used for
    this purpose, either via remote or local network connections.

When existing discovery mechanisms are adopted for PZP discovery, a
protocol mapper/wrapper is required to isolate the complexity of
different internetworking technologies and present discovery interface
as generic as possible to the web developers. The relationship among
these three parties is show in the following diagram.

![](http://dev.webinos.org/redmine/attachments/2289/wrapper.png)

In each step, protocols and interfaces are defined.

2. Technical Use Cases[¶](#2-Technical-Use-Cases)
-------------------------------------------------

3. Technical Formal Specification[¶](#3-Technical-Formal-Specification)
-----------------------------------------------------------------------

**Preconditions:**

-   Each PZP has enrolled in a persona zone. Enrolment is defined by
    when a PZP receives a certificate signed by the PZH for all future
    TLS connections.
-   Zones have authenticated each other in inter-zone PZP discovery
    scenario. To ensure a secure and successful inter-zone discovery,
    e.g. a PZP in PZH\_A to discovery PZPs in PZH\_B, the zones involved
    in the discovery have to authenticate with each other beforehand. It
    means that both parties have registered each other's certificate as
    being trusted after a certificate exchange procedure.

### 3.1. PZP registration and advertisement[¶](#31-PZP-registration-and-advertisement)

One of the key areas in PZP discovery is to make the PZP discoverable or
visible to potential PZPs that performing PZP searches. This requires
registering and advertising the PZP at a point, e.g. a database in a
central server or service list file in a local device, that others can
locate or look up.

### 3.1.1 PZP registers with PZH[¶](#311-PZP-registers-with-PZH)

In webinos, for the first time PZP connects its PZH, it shall registers
its service information to the PZH. The following information are
mandatory:

-   PZP identity
-   PZP name
-   PZP connection state

These information are updated at the following cases:

-   On receiving change notification from PZP
-   On PZP re-connecting to PZH

PZH has provided a central place to maintain the information that all
its PZPs provide. The following diagram shows the message flows when
PZPs registers with their PZH.

![ PZP\_A -\> PZH : setupTLSConnection(PZP\_A\_ID, PZP\_A\_Name, ...)
PZP\_A -\> PZP\_A : openListenerChannel PZH -\> PZH :
addPZPInfo(ConnectedPZPList, PZP\_A) PZP\_B -\> PZH :
setupTLSConnection(PZP\_B\_ID, PZP\_B\_Name, ...) PZP\_B -\> PZP\_B :
openListenerChannel PZH -\> PZH : addPZPInfo(ConnectedPZPList, PZP\_B)
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=c1c784f50b1fe4fe4d5ebb7877e43053bb4e1970cbb5706d4e857b3bd6eb901c)

### 3.1.2 Register PZP in existing discovery schemes[¶](#312-Register-PZP-in-existing-discovery-schemes)

In the case that PZH is not reachable or direct PZP discovery is
preferred, PZP relies on available existing discovery schemes for the
purpose. To be able to use existing discovery schemes for PZP discovery,
the PZP service must make itself registered and available in the service
list or service database of the discovery scheme. In this case, new
service registration procedure in under layer discovery scheme is
triggered by a call on the generic PZP registration interfac.

![](http://dev.webinos.org/redmine/attachments/2279/PZP_registration.png)

### 3.1.3 Interface mappings[¶](#313-Interface-mappings)

Since PZP is considered as a service in webinos. It shall follow URI
format of service type defined in 3.4. This format is not adopted by all
existing discovery schemes. While registering or creating PZP service in
these schemes, a type mapping scheme shall be provided in PZP discovery
design. The following diagram give an example on how this works.

![](http://dev.webinos.org/redmine/attachments/2239/service_type_mapping.png)

### 3.1.4 Functions and Data Structure[¶](#314-Functions-and-Data-Structure)

???CreateServices

  ------------------------ ---------------------------------------------------------- -------------- ---------------
  **Attribute**            **Description**                                            **Required**   **Data type**
  ServiceType(api)         URI used to identify unique service type of API created.   mandatory      String
  Filter:DiscoveryMethod   Discovery methods to be used                               optional       String
  ------------------------ ---------------------------------------------------------- -------------- ---------------

### 3.2. Finding other PZPs based on certain criteria[¶](#32-Finding-other-PZPs-based-on-certain-criteria)

#### Intra-zone PZP discovery[¶](#Intra-zone-PZP-discovery)

PZP\_A, PZP\_B, PZP\_C are PZPs from the same PZ.

-   **PZH-assisted intra-zone PZP discovery**

![ PZP\_A -\> PZH : FindServices(ServiceType:PZP) PZH -\> PZP\_A :
onFound(Service:ConnectedPZPList) PZP\_A -\> PZP\_A :
updatePZPInfo(ConnectedPZPList)
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=297c534993337719938d7fdfc008211f56cff3abc01e9b82784751e9622c0b68)

-   **Direct intra-zone PZP discovery**

![ PZP\_A -\> Network: FindServices(ServiceType:PZP, Filter:
Discoverymethod) Network -\> PZP\_B : FindServices(ServiceType:PZP,
Filter: Discoverymethod) Network -\> PZP\_C :
FindServices(ServiceType:PZP, Filter: Discoverymethod) PZP\_B -\>
Network : onFound(Service: PZP\_B) PZP\_C -\> Network : onFound(Service:
PZP\_C) Network -\> PZP\_A : onFound(Service: PZP\_B) PZP\_A -\> PZP\_A
: addPZPInfo(ConnectedPZPList, PZP\_B) Network -\> PZP\_A :
onFound(Service: PZP\_C) PZP\_A -\> PZP\_A :
addPZPInfo(ConnectedPZPList, PZP\_C)
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=a8aea01b37f491b9c91dcafccae225ba4d59d79169dec8512afd70bfd4ca6fe3)

#### Inter-zone PZP discovery[¶](#Inter-zone-PZP-discovery)

Preconditions:

-   PZH\_A and PZH\_B have authenticated with each other, which means
    that both parties have registered each other's certificate as being
    trusted after a certificate exchange procedure.
-   PZP\_AA is a PZP in zone PZ\_A, PZH\_A as PZH.
-   PZP\_BB is a PZP in zone PZH\_B, PZH\_B as PZH.
-   PZP\_BC is a PZP in zone PZH\_B, PZH\_B as PZH.

<!-- -->

-   **PZH-assisted inter-zone PZP discovery**

![ PZP\_A -\> PZH\_A: FindServices(ServiceType:PZP, Filter: ZoneId)
PZH\_A -\> PZH\_B: FindServices(ServiceType:PZP, Filter: ZoneId)
PZH\_B -\> PZH\_A: onFound(Service:ConnectedPZPList) PZP\_A -\> PZP\_A :
updatePZPInfo(ConnectedPZPList)
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=d1e162ab5a7187953e40075a2f04560077c07958d319adbc24c58951012ae0f7)

-   **Direct inter-zone PZP discovery**

![ PZP\_AA -\> Network: FindServices(ServiceType:PZP, Filter: ZoneId,
Filter: Discoverymethod) Network -\> PZP\_BB :
FindServices(ServiceType:PZP, Filter: ZoneId, Filter: Discoverymethod)
Network -\> PZP\_BC : FindServices(ServiceType:PZP, Filter: ZoneId,
Filter: Discoverymethod) PZP\_BB -\> Network : onFound(Service: PZP\_BB)
PZP\_BC -\> Network : onFound(Service: PZP\_BC) Network -\> PZP\_AA :
onFound(Service: PZP\_BB) PZP\_AA -\> PZP\_AA :
addPZPInfo(ConnectedPZPList, PZP\_BB) Network -\> PZP\_AA :
onFound(Service: PZP\_BC) PZP\_AA -\> PZP\_AA :
addPZPInfo(ConnectedPZPList, PZP\_BC)
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=4aa16feeee6a570fd94667f346091d499a1a20975e4079effc459a33ad89d5cb)

-   **Relations between under layer discovery methods and discovery
    JavaScript APIs**

Above diagram shows message sequences at Javascript level. Relationships
between the discovery Javascript API and the under layer discovery
method is shown in the following diagram.

![](http://dev.webinos.org/redmine/attachments/2251/DM_API_relationship.png)

### Discovery Querying or finding device that has PZP[¶](#Discovery-Querying-or-finding-device-that-has-PZP)

#### FindServices[¶](#FindServices)

  ------------------------ ---------------------------------------------------------------------------------------------------------------------- -------------- ----------------
  **Attribute**            **Description**                                                                                                        **Required**   **Data type**
  ServiceType(api)         URI used to identify which type of API that is requested.                                                              mandatory      String
  FindCallBack             Asynchronous callback used whenever a new service is found                                                             mandatory      Interface
  Options:timeout          A timeout value for the findService operation in seconds                                                               optional       unsigned short
  Filter:zoneId            Identities of personal zones                                                                                           optional       String
  Filter:remoteServices    If remoteServices is true, the findServices method will extend the search for services outside the local IP network.   optional       boolean
  Filter:DiscoveryMethod   Discovery methods to be used                                                                                           optional       String
  Filter:serviceLocation   physical location of the service                                                                                       optional       struct
  ------------------------ ---------------------------------------------------------------------------------------------------------------------- -------------- ----------------

-   **ServiceType**\
    PZP is considered as a service in webinos. It shall follow URI
    format of service type defined in 3.4. In order to isolate the
    complexity of lower level discovery schemes and expose a generic
    service type to web developer, a type mapping scheme shall be
    provided in PZP discovery design. The following diagram illustrate
    the relationships among these entities.

![](http://dev.webinos.org/redmine/attachments/2239/service_type_mapping.png)

-   **??Options**

The timeout value shall be overrode by messaging timeout value if
specified.

-   **Filter**

The use of DiscoveryMethod is in conjunction with remoteServices. Whilst
remoteServices is disabled, local discovery methods, e.g. zeroconf,
bluetooth SDP etc, apply. If remoteServices is enabled, remote discovery
mechanisms, e.g. XMPP discovery, apply.

In the case of zoneId is not specified, PZP discovery shall only look
for other PZPs in the same zone.

In the case of remoteServices is not specified, PZP discovery shall
limit the search for services that are connected directly to the device
or to the same local IP network.

In the case of DiscoveryMethod is not specified, a default
DiscoveryMethod set by the system shall be used.

### Bind services[¶](#Bind-services)

Basically, the Webinos service discovery module enables web developers
to find service (it includes devices) based on a certain search
criteria. The found services are listed in a selection list in an
asynchronous manner. Once the user selected a service, the
implementation of the service is initiated by binding to the service.
For further details on these APIs and example codes, please refer WP3.2
Discovery APIs.

bind(BindCallBack bindCallBack, optional DOMString serviceId);

  --------------- ------------------------------------------------------------------------------------------------------- -------------- ---------------
  **Attribute**   **Description**                                                                                         **Required**   **Data type**
  bindCallBack    Asynchrounous callback to report the states of the bind operation and the availability of the service   mandatory      BindCallBack
  serviceId       Unique id of the binding to the particular service.                                                     optional       String
  --------------- ------------------------------------------------------------------------------------------------------- -------------- ---------------

### 3.1. PZP Service Object[¶](#31-PZP-Service-Object)

(Only essential attributes that related to PZP service are listed
below - remove icon?)

**Attribute**

**Description**

**Required**

**Data type**

SERVICE\_INITATING

SERVICE\_AVAILABLE

SERVICE\_UNAVAILABLE

state

api

id

displayName

description

PZPNames

PZPAddresses

return multiple PZP intances - how to handle this?

### JavaScript APIs[¶](#JavaScript-APIs)

Webinos provides a JavaScript Discovery API for web developers. The
Discovery API is defined in Webinos Discovery specification. The
Discovery Interface provides two methods that are used to find services:

-   findServices(), to query for services
-   getServiceId(), to get a unique identity of service that can be
    shared between two peers.

[1] servicetype: definition of servicetype shall follow
InterfaceServiceType defined in 3.4.\
[2] Filter:

interface Filter {

    attribute DOMString[] zoneId;

    attribute boolean remoteServices;

-   attribute DOMString[] DiscoveryMethod;\*

    attribute ServiceLocation? serviceLocation;\
     };

The search query is asynchronous and there will be a success callback
for every service that is found. The time for finding services can vary
significantly depending of which type of discovery method that is used,
e.g. Bluetooth service discovery. An application must thereby be able to
handle cases where the search query continues for a reasonable amount of
time. The default max search query time is defined to 120 seconds.

The second part of the service discovery process is to Bind to the
requested services. This method is implemented by the Service Interface
as defined in Service Interface.

The Bind operation will mutually authenticate the application/service,
verify access/privacy policies and instantiate an implementation of the
API in asynchronous manner. Once the service binding has been
successfully executed, the API will be ready to use by the application
and the service object will act as a proxy to the remote peer. A more
detailed example of how to use the API is available here discovery code
example

### Protocol definitions[¶](#Protocol-definitions)

-   Addressing

<!-- -->

-   PZP service registration

<!-- -->

-   PZP advertisement

<!-- -->

-   Discover PZP

