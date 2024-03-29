User ID and Data Management[¶](#User-ID-and-Data-Management)
============================================================

Introduction and gap analysis[¶](#Introduction-and-gap-analysis)
----------------------------------------------------------------

According to the Specification in T3.1
(</wp3-1/wiki/Spec_-_Authentication#Conceptual-Architecture>),\

    Within webinos, the authentication and identity issues need to be addressed at two distinct levels.

       1. Intra webinos authentication: the mechanisms via which users and devices are authenticated by the personal zone
       2. Extra webinos authentication: which describe some utility capability, where the personal zone hub can assist in the authentication against multiple external web applications and services, which are not necessarily webinos based.

Main differences: 3.1 specs vs 4.1 implementation[¶](#Main-differences-31-specs-vs-41-implementation)
-----------------------------------------------------------------------------------------------------

Referring to the above statement, in case of user authentication, at
implementation there is no a clear distinction between Intra and Extra.
In particular, the method to authenticate a user against a PZH is OpenID
(which is external).\
In case of device authentication, in intra case, we do authenticate
devices by personal zone i.e. through device certificate.

### PZP Enrollment[¶](#PZP-Enrollment)

For enrollment of new PZP in the zone is used an out-of-band channel.
This consists in showing on the screen a QR code,the QR code is seen by
the PZP (or a user sees the QR code sent by the PZH and manually insert
it as PZP starting parameter) and then used to authorize PZP connections
toward the PZH
(</wp4/wiki/PZP_Device_Enrolment>).

### User authentication[¶](#User-authentication)

    authentication is done in two steps: first the user is authenticated to at least one of his devices. Second the device communicates on behalf of the user identifying itself with its public key and its certificate.

Actually the user is always authenticated to the PZH.

The Authentication API has been designed to provide authentication to
the present device, exploiting mechanisms of the underlying OS. And
devices communicates through a secure TLS exchange, based on
certificates signed by the PZH (which acts as a Personal CA).\
Authentication API is partially developed, for Linux and MacOSX, but was
not integrated with PZH, it should be probably be integrated to mention
we authenticate versus device using Authentication API.\
Note: the sort of the authentication API is at the moment unclear and
need some further investigation/scenarios development.

### Secure Storage[¶](#Secure-Storage)

    Once the user is authenticated to a device, the device reveals access to the secure storage which keeps the private key in a protected environment.

Secure storage has been investigated
(</wp4/wiki/Secure_Storage_Analysis>)
and an implementation proof of secure storage was provided for node 0.4.
It was no longer developed so presently is in the status of early
prototype. Where available, the system keyring is used to securely store
attributes.

    The PZP is the only entity which can access the private key. The PZP uses the private key for mutual authentication within the zone and
    across zones, and for integrity and confidentiality of communication between devices.

Private keys are usually stored in plain in the file system, so easily
accessible by any other entity on the same device. The use of keyring
provide some encryption, and it requires authentication before being
accesible. However, even if stored in the keyring, other authorized
entities (outside webinos) can access it as well, since it's not a
specific PZP store.

### Routing[¶](#Routing)

    When being messaged from devices on the open internet, the PZH acts like a DNS server, finding the most relevant end device application,
    to which the incoming webinos messages should be routed.

This is not strictly related to the authentication part, (possibly it
falls under "Device, Application and Service Discovery")

    The PZP therefore intercepts and either directly deals with or forwards the authentication requests.

It differs on the base of the authentication involved

-   For User-Device authentication, using Phase 1 authentication API,
    the PZP is mediator between user and underlying OS
-   For device-device authentication, the PZP-PZH or PZP-PZP interaction
    happens without user intervention (certificate exchange)

There is also a third-party OpenID authentication (at the PZH start) in
which the PZH is the intermediary between user and third party (e.g.
Google), but does not influence the process, apart relying on the third
party authentication result.

### Synchronization[¶](#Synchronization)

    The PZP synchronises key information with the PZH to allow it to perform its functions. This data includes
       * critical user identity information (to assist discovery) e.g. email, first name, last name etc
       * webinos PZH authentication tokens
       * extra webinos, 3rd party service authentication tokens (webinos Phase II)
       * identity tokens for trusted devices
       * identity tokens for trusted applications
       * identity tokens for trusted people
       * identity tokens for services that can be accessed from other people
       * all policy description files
       * context data
       * session data
       * application data

In general, synchronization has been investigated
(</wp4/wiki/Synchronisation_Analysis>)
but not consistently implemented. The information exchange (with no
specific synchronization requirement) among application involves
**events**. In phase 1 there is no synchronization of authentication
tokens (or policies) among Personal Zone devices

### User authentication level[¶](#User-authentication-level)

Unimplemented, currently the system can distinguish only if
authenticated or not.\
There is no the required built-in secure storage (as mentioned above,
the device keyring when available) and there is no the remote delete.

### User authentication notification[¶](#User-authentication-notification)

    event-based notification of user authentication each time the user authenticates without request by the PZP

Not implemented a mandatory system authentication notification. An
application can discretionary allow this with the Event API. Moreover,
any pzp joining is do updated on PZH and its presence informed to
corresponding pzp.\
Note: It was not explicit (in the 3.1 specification) where user
authentication should be notified, and for what use.

### User identifiers[¶](#User-identifiers)

     For user visible identifiers we use:
        * the URI of the PZH, or
        * some piece of data (e.g. the user's email address) that reliably
    resolves (e.g. via Webfinger) to a single PZH URI.

Presently, we use data derived from openID attributes to define a PZH
name, and no webfinger mechanism is implemented.

### Differences in the sequence diagrams[¶](#Differences-in-the-sequence-diagrams)

#### Technical Use Cases - Overview[¶](#Technical-Use-Cases-Overview)

-   The first time we have to authenticate to PZH (and obtain the QR
    code) before to start the PZP. The next time we can skip the
    authentication to PZH, but we have to start PZH and then the PZP, to
    avoid the PZP to run in virgin mode.
-   There is no data cache synch.

*Habib: Do we intend to allow PZP to join PZH as it is available as this
would require some kind of heartbeat server. There is no requirement
that's why not implemented*

#### scenario 1[¶](#scenario-1)

-   authentication and secure channel set-up are not separate steps. The
    PZP authenticates to PZH using PZH signed certificate establishing
    the TLS connection.
-   there is no data synchronization
-   about device list transmission and device status, it happens every
    time a PZP joins or leaves the zone (and the notification is
    broadcasted to each PZP component in the list)

#### scenario 2[¶](#scenario-2)

same notes of scenario 1

#### scenario 3[¶](#scenario-3)

The PZH does not mediate application authentication to Service
Providers.

In the other sequence diagrams there some of the differences already
highlighted above

### Virgin PZP[¶](#Virgin-PZP)

    If the PZH is not accessible, the PZP is accessible to other PZPs on the local network. The PZP MUST respond to other PZPs who intend to establish communication.

PZP to PZP authentication has been impemented if the PZPs have been
previously enrolled to the PZH. So, they use the PZH as Personal Zone
CA, and use the PZH certificate as trusted certificate to
authenticates/authorizes each other (note: Ziran has just implemented
zeroconf implementation to facilitate pzp to pzp communicate). If there
is no previous PZP enrollment, the item is on the agenda but not yet
implemented.

Focus[¶](#Focus)
----------------

The implementation used some concepts deferred in the specification in
the second phase that in some cases was needed in advance in
implementation phase 1, as well as some not planned but not implemented
in phase 1.

For example, the availability of a uniform identity inside the zone, as
well as the single sign-on. An application can obtain a userID from the
zone (distilling it from the OwnId string, composed of the user
identifier, which is derived form openID attributes, the PZP name, and
an app number) but this should be improved by offering a more direct way
to get it.\
*Habib agreed this should be added in WP3.4 standard apis* at the moment
could be achieved through functions like getPzpId() or getPzhId()

Thus, some work is further needed to conceptually integrate all the
specification in a robust and coherent framework, and possibly some of
the specs in 3.1 can be reworked in light of first phase implementation
lessons.

