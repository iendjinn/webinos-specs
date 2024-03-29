Webinos sessions[¶](#Webinos-sessions)
======================================

A functioning webinos network will consist of, multiple devices,
multiple servers and multiple applications. It will require the
interaction of PZPs and PZHs belonging to different users, over multiple
different networks.

Within that complex interaction, there will be many notions of session
at different levels. It is important therefore to be clear with our
terminology.

![](Session_Architecture.jpg)

Intra Personal Zone Relations (Sessions)[¶](#Intra-Personal-Zone-Relations-Sessions)
------------------------------------------------------------------------------------

A single user will have many PZPs, on different devices, but only a
single PZH, hosted on the web.

PZPs need to be installed securely on devices [PZP installation
bootstrap](.html), however once this is done a long term relationship
now exists between that PZP and the PZH. We will call this an "Intra
Personal Zone Pairing". This pairing shall be manifest by the PZP and
PZH having exchanged certificates. Section [Conceptual
Architecture](Conceptual%20Architecture.html) gives the details on the
certificate exchange.

The details of provisioning and later removing certificates (thereby
cancelling the pairing) can be found in
[Spec\_-\_Synchronisation](.html)

If a pairing exists between a PZP and a PZH they should try to enter an
active Intra Personal Zone Session with one another.

PZP-PZH sessions (Intra Personal Zone Sessions) always take place of the
publicly addressable internet. This is because one of the defining
characteristics of a PZH is that it is must be permanently addressable
on the internet. A PZP-PZH session takes place over a TLS connection,
assuring that the information exchanged in the session is secure. This
secure channel, once established is the route via which all
communications between PZH and PZP, in either direction, takes place.

Note: as an optimisation out of band "wakeup" notifications may be
required to issue PZH-\>PZP messages in a timely fashion. These out of
band notifications should only contain the bare minimum information to
request the PZP reactiviates the connection. No sensitive information
should be passed in the wakeup notifications, as they are not protected
by the TLS channel.

When and PZH and PZP session is active it means that messages can be
routed in either direction, within a reasonable time-frame. (In practice
less than a pre-stipulated time-out value)

A session is established when a PZP and PZH have successfully
authenticated.

When a session is successfully established between a PZP and a PZH, a
bidirectional channel of information is established across which all the
following may happen

1.  A PZP may authenticate/re authenticate against the PZH
2.  Outgoing webinos messages to external services (multiplexed through
    the PZP-PZH channel)
3.  Synchronisation traffic, of the following
    1.  webinos user identity information
    2.  webinos user data information
    3.  webinos PZP and PZH certificates
    4.  webinos policy
    5.  webinos friends identity information and certificates of their
        PZHs
    6.  webinos services tokens
    7.  webinos device identity tokens
    8.  webinos application identity tokens
    9.  webinos application data for synchronisation

External services relations (Sessions)[¶](#External-services-relations-Sessions)
--------------------------------------------------------------------------------

Individual webinos applications create "sessions" with webinos services.

All such sessions must be mediated by the PZP of the originating
application. In other words only application bound to a users PZP can
make user of webinos services. The originating users PZP will take care
of authentication and the user centric policy enforcement.

The application can connect to two types of service:

1.  anonymous service: this is a webinos service that is mediated by an
    un-authenticated personal zone
2.  PZ hosted service: that is a webinos service owned by someone. Note
    in this scenario the permission to access to the services, is
    mediates by two policy enforcement points, the requester of he
    service and the hoster of the service.

Much like intra zone sessions, there are distinct notions of "Pairing"
and "Binding".

If an application has been "paired" with a service, tokens may be
exchanged at the PZX level. This token exchange can be used by the
webinos infrastructure to short-cut authentication and permissions. The
active policies on any participating app-service flow, must still have
this permission granted

The process of binding an application with a service (irrespective of
whether it has been already paired), is akin to the notion of an intra
zone session as described above. Whist the session is active, in other
words whilst the binding is fixed then:

-   Messages can be routed bidirectionally, between app and service
    within a reasonable time frame (within a pre stipulated time-out
    value)

External service sessions can happen over the public internet or via the
local network

Public internet sessions to web hosted services will be mediated by the
PZH

Local webinos sessions to local device services (including also APIs
local to the WRT) are mediated by the PZP.

External service sessions can therefore be carried over a number of
physical networks and higher level protocols.

PZH to PZH sessions[¶](#PZH-to-PZH-sessions)
--------------------------------------------

In order route messages between applications and services on different
zones, it is sometimes necessary to route messages between two PZH's

(The exception to this, is where message takes place directly between
PZPs)

This session is also initiated and maintained using a TLS connection.

