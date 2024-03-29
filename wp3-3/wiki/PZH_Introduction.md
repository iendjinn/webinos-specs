PZH[¶](#PZH)
============

-   [PZH](#PZH)
    -   [Pre-configuration](#Pre-configuration)
    -   [PZH configuration](#PZH-configuration)
        -   [PZH default policy](#PZH-default-policy)
        -   [PZH Identity](#PZH-Identity)
        -   [PZH Address](#PZH-Address)
        -   [Messaging and Routing](#Messaging-and-Routing)
        -   [PZH/PZP Status Update](#PZHPZP-Status-Update)
        -   [Service Discovery](#Service-Discovery)
    -   [PZH Components](#PZH-Components)
        -   [Enrolling and Revoke device](#Enrolling-and-Revoke-device)
        -   [PZH - PZH Communication](#PZH-PZH-Communication)
        -   [Export and Import of PZH](#Export-and-Import-of-PZH)
        -   [Platform Synchronisation](#Platform-Synchronisation)
    -   [Client and Server TLS
        connection](#Client-and-Server-TLS-connection)
        -   [TLS Servers on the PZH](#TLS-Servers-on-the-PZH)
        -   [Outgoing TLS connections on the
            PZH](#Outgoing-TLS-connections-on-the-PZH)
    -   [PZH States: incoming connections from enrolled
        PZPs](#PZH-States-incoming-connections-from-enrolled-PZPs)

A webinos personal zone is a combination of two types of entity,
Personal Zone Hubs (PZHs) and [Personal Zone
Proxies](Personal%20Zone%20Proxies.html) (PZPs). There is only one PZH
in each zone and it is reachable on the public Internet at all times. It
can either be a cloud-based service or could be integrated in a DSL
router. A PZP, on the other hand, usually resides on a user operated
device. There is one exception - a cloud-based PZP (which does not
belong to a user operated device) can be created to expose services that
other PZPs can use, such as context database.

In client - server terminology, the PZH acts as a server in the webinos
architecture and the PZPs act as clients. The PZH is limited to just one
user, i.e. Alice is a sole owner of her PZH. If the user wishes to
establish communication with the other users, they securely exchange
certificate and perform connection between the two personal zones.

PZHs provide the following functionality:

NA: question to ask ourselves here: is there enough information and what
is the check list for me to imlement a full PZH in Python for example.
is most of the material required in PZH admin section

habib: All the relevant details has been covered such as message
exchanges, pzh web server information, directory structure, pzh tls
connection. IMO the material needed to implement include whole of PZH
and PZH deployment to understand how to communicate with the PZH

-   Routing communication between personal zone devices
-   Synchronizing information about the personal zone, including access
    control policies and device certificates
-   Administration of the personal zone through a web interface
-   Export and import of personal zone information.
-   Storing of certificates, trusted list of devices, policies and user
    data.
-   Support for service discovery API.

[andré] see comment about events API in events API section!

[habib] comment addressed

Most of these capabilities are described in more detail in the [PZH
Admin](.html) section.

In this document we refer to the PZH as a monolithic server. In
implementation, PZH runs externally at service provider. To support
running at same address and port, it uses SNI (server name indication)
and is covered in detail in the informative section, [PZH
deployment](.html).

Pre-configuration[¶](#Pre-configuration)
----------------------------------------

Starting a PZH results in the web server running and listening for the
incoming connections. The PZH and its web server must only allow secure
connections over TLS, so when the PZH runs for the first time it will
create a set of X509 certificates as shown in Figure 1.

![](default_pzh.png)

Figure 1: Default PZH initializing Web Server

PZH configuration[¶](#PZH-configuration)
----------------------------------------

The PZH creation does not bind it with a particular user. The PZH are
configured through the owner logging into the PZH web interface for the
first time using their chosen OpenId credentials. Webinos uses OpenId
mechanism to authenticate the user. The PZH does not provide any
mechanism for storing user credentials, once authenticated via OpenId,
webinos platform allow users to perform various actions.

Any other mechanism that can validate user but does not mandate the PZH
to hold user/password on the PZH could be used for the user
authentication purpose. In this specification only OpenId mechanism is
covered, it does not cover details about other mechanism that could be
used for user authentication.

[andré] Why does webinos needs OpenId support? Is it used for something
else than just log-in to PZH? I understand the current implementation
doesn't wanted to store and handle user data itself. But isn't this
implementation specific. Can i implement a PZH using electronic identity
cards (like the German one
<http://en.wikipedia.org/wiki/German_identity_card>) or just using
Username/Password and ask for user data?

[habib] no it is for user authentication and not implementation
specific. Since any mechanism for username and password will mandate
storing information and we do not want the PZH to have any
secure/database storing mechanism.

After the user has successfully logged in, the PZH will received an
identity assertion from the OpenID identity provider providing about the
user details. This identity information will then be re-used when
authenticating subsequent log-ins by the zone owner.

Once configured with the user identity, the TLS server is initialized
and will wait for the incoming PZP connections. The processes involved
in PZH configuration are:

-   Certificate generation (see the [Personal Zone Key
    Infrastructure](.html) documentation to see which certificates are
    required)
-   Initialization of PZH TLS Server
-   Storing certificates, keys and user data

This is a one time activity that will be dependent on the PZH service
provider rules. In this document we do not specify how a PZH provider
will configure their system or how users are allowed to create PZHs. It
is assumed before providing login option, user has to select the service
provider's facilities.

![](pzh_creation.png)

Figure 2: PZH configuration via PZH web interface

The PZH can also be created from the PZP, It is part of browser
enrollment as described in the [PZH
Admin](/wp3-3/wiki/PZH_Admin)
section. In the PZP enrollment step, if the PZH does not exist it asks
for a user consent to create the PZH. Based on the user consent, the PZH
is created for the user. It is similar in process as described above,
but differs only that it is initiated from the PZP end.

[andré] PZH Admin spec does not describe how this can happen when
triggered from the PZP. Connect to PZH provider? How, protocols needed?
How to tell PZH provider that i want to create a new PZH for me?

[andré] Yes it does please auth-status message. I have covered in pzh
admin all protocols and message detail. By logging in if pzh does not
exists it creates for you. As described before above diagram PZH
provider should impose some rules before allowing PZH to be created.

After PZH is configured, the following functions will be performed by
the PZH.

-   Create PZH default policy
-   Create PZH identity
-   Assign PZH address
-   Update PZH/PZP Status
-   Messaging and routing
-   Service discovery

### PZH default policy[¶](#PZH-default-policy)

After the PZH is configured it should be given a set of default
policies. Policies comprise a target, set of rules and conditions. The
policy target should make sure that this PZH can only be used by the
user identity provided. Default policy are covered in the [following
section](/wp3-3/wiki/Policy#Default-policy).

[andré] did we defined how the default policy looks like? If so provide
reference, if not we need to define one.

[habib] added link, salvatore is going to add contents to above link

### PZH Identity[¶](#PZH-Identity)

The identity assigned to the PZH is fetched via user authentication
mechanism. The user authentication mechanism should return attributes of
values that identifies the user. The information that the PZH looks
after authentication are the user's first name, last name, country and
email id. The PZH identity used is user email id such as
<alice@example.org>

[andré] again, is OpenID really mandatory or implementation specific?
Currently still don't see that OpenID is a must for a PZH.

[habib] IMO still yes it is mandatory but altered text to make it
generic .

### PZH Address[¶](#PZH-Address)

The PZH should be reachable by a standard URL and this address can be
enrolled with the WebFinger server in order to map it to a user
identity. This address should be reachable to user all the time when
connected to the Internet. The [Entity Definitions](.html) documentation
describes the address of a PZH.

A WebFinger server should typically return following following
attributes. The attribute pzhid should describe the fields.

      <Subject>acct:alice@example.org</Subject>
      <Link rel=`http://webinos.org/spec/1.0' 
            ref=`http://pzh.example.org/alice@example.org'/>

To find another user PZH, minimum information needed is user email id to
retrieve value from the WebFinger server.

[andré] could we have an example here? On the one hand we could say that
discovering PZH address is out of scope of the spec but if we say
WebFinger can be used don't we need then to specify something like a key
that represents a webinos PZH URL? Or how to know which URL is the one
for the PZH?

[habib]added information about pzh id.

### Messaging and Routing[¶](#Messaging-and-Routing)

The PZH provides routes between personal zone devices and for
communication outside the personal zone devices. It is a central point
of communication in the personal zone architecture and facilitates
devices in different location communicate despite location or the
network they are using. Routing is performed by the PZH which is trusted
to send messages to the right locations.
Messaging:"/wp3-3/wiki/Messaging\_and\_Routing"
section covers this in details.

### PZH/PZP Status Update[¶](#PZHPZP-Status-Update)

The PZH maintains a list of all the PZPs and the PZHs that may be
connected to the PZH at any time, as well as their current connection
status. This includes list of trusted the PZP's which are not connected.
The PZH sends the PZP *update* message at the following occasions :

-   PZP connected to the personal zone
-   PZP disconnected from the personal zone.
-   A PZH from another zone has connected
-   A PZH from another zone has disconnected

The update message include following fields:

-   Remote PZP's friendly name and identity
-   Remote PZH's friendly name and identity
-   Connection status i.e current connection between the PZH and other
    PZHs

[andré] clarify that the connection status is about a connection between
"my PZH" and other PZHs - otherwise it reads like my PZH sends me a
message about if i am connected to my PZH.

[habib] comments addressed

The update message sent by PZH to PZP format is presented below:\
JSON:\

    {
      “to”: PZP ID,
      “from”: PZH ID,
      “type”: “prop”,
       “payload”: {
         “status”:”Update”,
         “message”: {
                      "PZH": 
                      {
                        ["name": "", 
                         "connected":true/false]
                      },
                      "PZP": 
                      {
                        ["name": "", 
                         "connected":true/false,
                         "ipaddress": "",
                         "port": ""]
                      }             
                    }
        }
    }

The PZH uses identity information internally but for display purposes
the user is always shown a friendly name.

### Service Discovery[¶](#Service-Discovery)

Each webinos enabled device has a set of services. These services are
updated in the PZH when they connect or when they become available.
These services are discoverable by other PZP's. The PZH acts as a
central repository to get all services searchable for all connected
PZP's. It also holds services hosted at other PZHs that belong to the
trusted third parties, such as friends. All services hosted at the PZH
are services from connected PZPs and PZHs.

Details are covered further in the [Service Discovery](.html) section.

PZH Components[¶](#PZH-Components)
----------------------------------

The PZH provides a web interface for administering the personal zone.
This administrative functionality can only be accessed through logging
into the PZH with OpenID user credentials. After logging into a PZH web
interface, the user can:

-   Enrol and revoke devices
-   Establish connections with other personal zones
-   Export and import data

### Enrolling and Revoke device[¶](#Enrolling-and-Revoke-device)

Enrolling a new personal zone device is a one-time event (per device)
that allows a new PZP to join the personal zone. More information about
this can be found in the [PZH Administration](PZH%20Administration.html)
section.

Removing (or "revoking") a device from a personal zone is also done
through the same web interface. After revocation all personal zone
devices and known PZHs are updated with this information.

### PZH - PZH Communication[¶](#PZH-PZH-Communication)

Communication between two PZHs requires the owners of both zones to be
able to identify one another and trust each other. Identification is
assured through a certificate exchange protocol described in the
[Personal Zone Key Infrastructure](.html) section . Once certificates
have been exchanged both PZHs can connect to each other, although
policies will limit what these are able to do, with no access granted by
default.

### Export and Import of PZH[¶](#Export-and-Import-of-PZH)

The PZH can be migrated from its current service provider to another
provider. Export and import ensures policies, user preferences and user
details are moved to new location. More detail on this can be found in
the [PZH Administration](PZH%20Administration.html) section.

### Platform Synchronisation[¶](#Platform-Synchronisation)

The PZH allows for
synchronisation:"/wp3-3/wiki/Synchronisation"
between PZPs. It does synchronisation of certificates, policies and
settings. The synchronisation of items is bi-directional i.e., PZPs can
update the PZH with changes to synchronised items as well as the PZH
making changes to PZPs.

[andré] add reference to synchronization section.

[habib] done

Client and Server TLS connection[¶](#Client-and-Server-TLS-connection)
----------------------------------------------------------------------

The PZHs have the following client and server TLS connections. The TLS
Server is the main entity and it facilitates communication between the
personal zones.

### TLS Servers on the PZH[¶](#TLS-Servers-on-the-PZH)

[andré] why is port 80 mandatory? could be default but i don't think
that we can mandate this. Is this TLS Server on Port 80 the admin
interface Web site or something different for connecting devices (or is
both on same port?)?

[habib] if we do not mandate 80 then we cannot connect to PZH from PZP.
we can faciliate finding PZH via webfinger but not port.

Port

80 (Should be consistent, if address changed then PZP will not be able
to communication with PZH)

Description

Incoming connections from PZPs (zone devices) as well as connections
from external (friend) PZHs.

Parameters

rejectUnauthorized = true (unauthorized certificate connection is
rejected),\
 requestCert = true (this is to enable mutual authentication)

Trusted certificates

Signed PZP certificates & trusted external (connection) PZH certificates

Authentication

Entities with PZH certificates are assumed to be a device within other
user's PZH

Entities with PZP certificates are assumed to be zone devices

### Outgoing TLS connections on the PZH[¶](#Outgoing-TLS-connections-on-the-PZH)

Port

Random Port

Description

Outgoing connections to connect external PZHs

Parameters

Connecting PZH address

Trusted certificates

Just the certificate of the PZH we are contacting. May not be entirely
trusted

Authentication

The remote party must use the certificate we are expecting

Any incoming data from this connection must be mapped to the user of the
PZH we are connecting to. They may not be trusted to do anything other.

[andré] i am not an expert in TLS connections but if we are talking here
about parameters must then not also the whole message be defined? Or is
it part of TLS? How does the message / protocol looks like when using
rejectUnauthrized etc parameters?

[habib] it is standard tls interface and that's why not specified in
detailed.

PZH States: incoming connections from enrolled PZPs[¶](#PZH-States-incoming-connections-from-enrolled-PZPs)
-----------------------------------------------------------------------------------------------------------

The PZH moves between the following states when PZPs connect, starting
with the state "NoPzpsConnected". In this state chart, multiple PZPs may
connect to the PZH at any time, with the list of connected PZPs shown in
the state "PzpsConnected".

[andré] i don't see how this diagrams helps to understand PZHs. What
does an implementer of a PZH get from looking into this Figure? Also it
looks more implementation dependent. This spec should be about mandatory
features and protocols needed to implement these features. The rest is
probably implementation specific and must no be specified.

[Habib] this is necessary for getting PZH in the correct states

![](pzh-pzpsconnecting.png)\
Figure 3: PZH State diagram

