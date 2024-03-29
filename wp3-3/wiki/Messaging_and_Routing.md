Messaging and routing[¶](#Messaging-and-routing)
================================================

-   [Messaging and routing](#Messaging-and-routing)
    -   [1. Introduction](#1-Introduction)
    -   [2. Technical Formal
        Specification](#2-Technical-Formal-Specification)
        -   [2.1 PZH Address Resolving](#21-PZH-Address-Resolving)
            -   [2.1.1 OpenID attribute
                exchange](#211-OpenID-attribute-exchange)
            -   [2.1.2 DNS NAPTR](#212-DNS-NAPTR)
            -   [2.1.3 WebFinger](#213-WebFinger)
            -   [2.1.4 webinos.org central
                lookup](#214-webinosorg-central-lookup)
        -   [2.2 Routing](#22-Routing)
            -   [2.2.1 Routing Models](#221-Routing-Models)
            -   [2.2.2 Addressing / Entity Naming for
                Messaging](#222-Addressing-Entity-Naming-for-Messaging)
            -   [2.2.3 Routing Algorithm](#223-Routing-Algorithm)
        -   [2.3 Message Object](#23-Message-Object)
            -   [2.3.1 Generic Message
                Object](#231-Generic-Message-Object)
            -   [2.3.2 Delivery Notification Message
                object](#232-Delivery-Notification-Message-object)
            -   [2.3.3 RPC Message Object](#233-RPC-Message-Object)
            -   [2.3.4 PROP Message Object](#234-PROP-Message-Object)
    -   [3. JavaScript APIs](#3-JavaScript-APIs)
    -   [4. Dependencies on other
        components](#4-Dependencies-on-other-components)
        -   [4.1 Policy Enforcement](#41-Policy-Enforcement)
    -   [5 References](#5-References)
        -   [5.1 JSONRPC2.0](#51-JSONRPC20)

Scope:

Webinos messaging and routing specifies interfaces for message creating
and routing in webinos system. These interfaces shall be generic enough
to be used from both webinos core and application levels.

1. Introduction[¶](#1-Introduction)
-----------------------------------

Webinos messaging and routing defines interfaces to create, address,
route and handle messages among addressable entities and network
interfaces in webinos system. The interfaces are specified in a very
generic fashion in a sense that there is no need to have knowledge of
the specific messaging protocols being used under. The operations of
routing, however, rely on the interconnect technology abstraction and
NAT traversal capabilities provided by the overlay networking system
(see [Architecture\_Overview](.html)) to enable easy and consistent
communication with the external networks.

The interfaces support both Point-to-Point (PTP) and Publish/Subscribe
(Pub/Sub) messaging models. Due to the significant differences between
these two models, methods of handling are specified separately where
required.

This specification describes the interfaces from the following aspects:

-   Message object
-   Message routing

The interfaces specified will be used by webinos core entities, e.g.
Personal Zone Hubs (PZHs) and Personal Zone Proxies (PZPs), and
applications. A set of JavaScript inter-application messaging APIs
wrapped from these interfaces are exposed to applications to allow them
to send or forward messages to other entities, whether local or remote,
and to receive messages addressed to themselves or to the addressable
entities they control (e.g., a service created by the application) in a
seamless way. Details on JavaScript APIs can be found in section 3. It
is followed by discussions of dependencies on other components in
webinos system.

2. Technical Formal Specification[¶](#2-Technical-Formal-Specification)
-----------------------------------------------------------------------

### 2.1 PZH Address Resolving[¶](#21-PZH-Address-Resolving)

When a connection needs to be established to a PZH the connecting entity
(PZH, PZP) only has an OpenID user identity to start with. As outlined
in [Entity Definitions](.html) the receiving PZH is expected to be part
of a different internet domain quite often. Still, the user identity
must be resolved to the PZH URI that in its turn can be addressed using
regular DNS A of AAAA record lookup.

Resolving an OpenID user identity to a PZH URI SHALL be done by
following these steps, in the given order:\
1. OpenID attribute exchange method, specified at <http://openid.org>
with attribute 'webinos-pzh'\
2.

As soon as one step succeeds, the resolving party MUST NOT try following
steps.

In the following sections the steps are outlined in more detail.

#### 2.1.1 OpenID attribute exchange[¶](#211-OpenID-attribute-exchange)

An OpenID may optionally contain attributes. If it does contain an
attribute named 'webinos-pzh' it SHALL contain a full URI to the PZH.

#### 2.1.2 DNS NAPTR[¶](#212-DNS-NAPTR)

When a user has DNS control over the internet domain to which his OpenID
identifier belongs he can use DNS NAPTR [RFC2915]. This can be used to
resolve the PZH address. The NAPTR allows a rewrite of the user
identifier to the PZH address using DNS. An example NAPTR for webinos
would look like this:

    someprovider.com.  IN NAPTR 100 10 "U" "http+I2L" "!(.+)@(.+)!https://\2/\1!".

The rewrite regexp is simplified for readability (e.g., it does not do
rigorous validation of the identifier). In the example an OpenID
identifier from someprovider.com (e.g., <fred@someprovider.com>) is
rewritten to the PZH address <http://someprovider.com/fred>. If the
domain part of the PZH is different, the rewrite rule would change to
e.g.:

    someprovider.com.  IN NAPTR 100 10 "U" "http+I2L" "!(.+)@(.+)!https://otherprovider.com/\1!".

Bear in mind that this last setup may reguire changes to a domains DNS
records when doing user administration.

The "U" flag indicates that the next step is not a (direct) DNS lookup.
The "http+I2L" service field indicates that the protocol to be used for
the result is HTTP and the URI resolves to a URL [RFC2483].

When DNS NAPTR is user for resolving OpenID URIs, the record SHALL
contain a "http+I2L" service field. If user@domain OpenID identifiers
are resolved, the service field record SHALL contain "http+I2L". In
addition, DNS NAPTR used for webinos purposes SHALL be compliant.

#### 2.1.3 WebFinger[¶](#213-WebFinger)

For users that have no administrative DNS-level access to their domain
but do control the entire website space of their OpenID-referenced
domain, WebFinger (<http://webfinger.org>) might be an option. It is
enabled by adding a `http://example.com/.well-known/host-meta` file to
the website, that defines a template on how to find the webfinger
information for a user. This user specific information could then
contain a webinos link like so:

\<Link rel=\`<http://webinos.org/spec/1.0>'\
ref=\`<http://phz.example.org/profile/joe.smith'/>\>

When WebFinger support is chosen, a link statement SHALL be used where
the rel value equals `http://webinos.org/spec/1.0` and where the ref
value contains the full URI to the users' PZH.

#### 2.1.4 webinos.org central lookup[¶](#214-webinosorg-central-lookup)

While the webinos project is running, a WebFinger service will be
maintained on `webfinger.webinos.org`.

If all else fails and the `webfinger.webinos.org` domain has an A and/or
AAAA record of its own, `webfinger.webinos.org` MAY be used for
resolving PZHs. If `webfinger.webinos.org` does not have an A or AAAA
record, callers MUST refrain from calling the default http server.

### 2.2 Routing[¶](#22-Routing)

At a conceptual level, the webinos routing system SHALL provide a
complete end-to-end routing path between service/application instances
as shown in the following diagram, either within a personal zone or
cross personal zones.

![](end_end_routing.png)

It is required that

-   Each entity involved in the routing is addressable, either via a
    name or address.
-   Each entity is able to establish communication session(s) or
    channel(s) with its routing neighbour(s).

At implementation level, Webinos core components, PZPs and PZHs, SHALL
have routing manager functionality for creating and maintaining routing
table, checking and dispatching messages.

#### 2.2.1 Routing Models[¶](#221-Routing-Models)

Message propagation and routing in Webinos are performed in one of two
ways:

-   Point-to-point routing. The sending application explicitly specifies
    the destination to which it is sending the message. There is a
    relatively tight coupling between the sending application or process
    and the receiving party.

![](http://dev.webinos.org/redmine/attachments/2346/point-to-point.png)

-   Publish-subscribe routing. The sending application does not know the
    destination to which it is sending the message, but instead assigns
    the responsibility for managing who receives the message to the
    middleware. The middleware defines a list of topics on which the
    message creator publishes messages. In contrast to a point-to-point
    communication, in a publish/subscribe model, a copy of the message
    is processed for each of the logical subscriptions.

![](http://dev.webinos.org/redmine/attachments/2347/sub-pub.png)

#### 2.2.2 Addressing / Entity Naming for Messaging[¶](#222-Addressing-Entity-Naming-for-Messaging)

The addressing and entity naming for messaging are inspired by the
[Entity Naming for Messaging discussions in
WP4](/wp4/wiki/Entity_Naming_for_Messaging).

##### Entities overview

The following entities need a name so they can be addressed:

![](entities.png)

and they are ordered as depicted in the following figure:

![](entity-order.png)

##### Names

User Identities take the form\

    user@domain.ext

PZPs have, globally unique, friendly names:\

    laptop
    mobile

\
which are provisioned when webinos is first installed on a certain
device.

Where possible, we use Uniform Resource Names (URNs) constructed
according to [RFC 2141](https://tools.ietf.org/html/rfc2141).

For services, this would be:\

    urn:services-webinos-org:calender
    urn:services-webinos-org:geolocation

At a later stage, third parties may of course extend webinos and add
services from other name spaces.

Service Instances receive an automatically generated name, like\

    A0B3

\
which need to be unique within the scope of the PZP they are running in.
PZHs are informed of all running services on all connected PZPs.

A Service Instance is addressed by a combination of the service URN and
the automatically generated name. This way it is human readable to which
kind of service a message is being sent. The URN is also used by service
discovery to identify the service type of a service that is discovered.

##### Messaging

The interface between the PZP and the PZH is aggressive up, meaning as
soon as the PZP has network connectivity it will try to connect to the
PZH.

To send a message to a service from somebody else the complete name is
constructed like so:\

    other_user@her_domain.com                        <-- name of user identity (PZH?)
      |
      +-- laptop                                     <-- name of the PZP
            |
            +-- urn:services-webinos-org:calender    <-- service type
                  |
                  +-- A0B3                           <-- service implementation

##### Sessions

As soon as an application or a service binds to another service, they
implicitly create a session, to which they receive a reference. The
session object stores all names (plus the resolved addresses) so the
callers do not have to do that themselves. Replying to a message is
simply done through the session.

#### 2.2.3 Routing Algorithm[¶](#223-Routing-Algorithm)

##### Message validation

The message metadata shall be checked at both sender/publisher and
receiver/subscriber sides to ensure validity, well-formedness and
consistency.

Message validation failure MAY result in automatic generation and
sending of delivery notification messages by the checking party if it's
not the message source and the message requires delivery notification.
This kind of behaviour, however, is implementation-defined. Failure to
validate a message SHALL prevent the message from being further
processed.

Errors during the validation phase when the message source is local
SHALL, instead, result in appropriate exceptions being thrown at the
application-level.

##### Route Determination

The route determination decides how each recipient is to be reached. In
the route determination phase the routing manager SHALL check the
recipient and determine whether it is local or remote. In the former
case, it SHALL ensure that the recipient actually exists and is
reachable upon policy restrictions and, if this condition does not hold
true, it SHOULD automatically generate and send a delivery notification
message to inform the message source. In the latter case it SHALL
determine whether the recipient is reachable within the local networks
the device is connected to or not, and also which network interface is
going to be used to reach the recipient, so that this information is
available in the policy enforcement phase.

Route determination for messages SHALL be performed once per recipient,
so that individual failures SHALL only affect one message/recipient
combination. Failures during the route determination phase SHALL prevent
the message from being further processed for that message/recipient
combination.

##### Application-level routing

The message handling functionality exposed to the application, at the
lowest level, consists of a restricted set of conceptually simple
operations: generating and sending messages, or forwarding them, and
registering listeners for incoming messages.

This implies that the message routing manager SHALL be able to somehow
create the JavaScript representations of incoming message objects and to
properly trigger the execution of the relevant listener callbacks.

Each application SHALL be allowed to handle messages from/to addressable
entities that it "owns" (e.g., the application itself, the services it
exposes), obviously according to the constraints imposed by local policy
rules and authorizations, hence it SHALL be able to both receive
messages directed to any addressable entity that it owns and to
send/forward message on the behalf of any addressable entity it owns.

Other than that, at this level, the behaviour of the system is highly
dependent on the actual webinos inter-application messaging API
specification, hence that document is to be considered the reference for
determining whether a given implementation is in conformance or not.

##### Network-level routing

The network-level routing algorithm SHALL be based on the defined
addressing scheme.

Each routing entity SHALL register itself with its parent node and child
node if the other parties have not registered themselves with this
routing entity. A successful registration process SHALL result in an
entry or record in local routing table for both parties that registering
and being registered with.

On receiving a message, the receiver checks if itself is the message
destination. If so, based on the message type, correspondent handler
functions/callbacks MAY be called. For example, if a JSON RPC type of
message is received, the following procedure May happen:

-   Message destination calls rpchandler to handle the message.
-   RPC result is packed within a new message object. Return route back
    to message origin follows the same routing rule as any message
    experienced.
-   When RPC result is received by the message origin, if a callback was
    defined during creating message, this callback will be executed.

In the case that the message receiver is not the final destination, the
receiver SHALL forward the message. When there is no routing information
about the final destination available at this message receiver, it SHALL
look up the routing table for the next available hop to the destination.

### 2.3 Message Object[¶](#23-Message-Object)

#### 2.3.1 Generic Message Object[¶](#231-Generic-Message-Object)

Each message results in the creation of a message object. A generic
message object is defined here. Any user or system specified message
object will be a subclass of the generic message object. The generic
message object includes the following attributes:

  ----------------- ------------------------------------------------------------------------------------------------------------------------------ --------------- ---------------------------------------------------------------------------------
  **Attribute**     **Description**                                                                                                                **Mandatory**   **Data type**
  type              Identifies the message type and determines payload semantics                                                                   Yes             String that matches the following regular expression: [\_a-zA-Z][\_a-zA-Z0-9]\*
  from              Represents the entity that originally sent the message                                                                         Yes             Addressable entity object reference
  to                destination entity                                                                                                             Yes             addressable entity object reference
  id                Message identifier                                                                                                             Yes             String identifying the message
  timestamp         Moment in time in which the message is generated by the original message source                                                No              A suitable date/time representation with millisecond precision or better
  expires           Moment in time past which the message is no more valid or meaningful                                                           No              A suitable date/time representation with millisecond precision or better
  deliveryReceipt   Indicates whether the sending entity wants to be notified by the receiving entities about the result of the message delivery   No              Boolean value
  payload           Message type-specific data                                                                                                     No              String
  ----------------- ------------------------------------------------------------------------------------------------------------------------------ --------------- ---------------------------------------------------------------------------------

This specification does not demand the usage of a specific serialization
for transmitting messages, yet it presupposes that:

-   the actual serialization has a one-to-one mapping with Unicode code
    points for addresses and payload data;
-   a one-to-one mapping between addressable entities and address
    strings is defined.

The 'id' attribute is used by the sender to track if a response or error
message that it might receive is in relation to that message.

It is up to the sender of the message whether the value of the 'id'
attribute is unique only within the current session or is globally
unique.

#### 2.3.2 Delivery Notification Message object[¶](#232-Delivery-Notification-Message-object)

The delivery notification protocol is part of the core webinos message
handling protocol and it provides a handful of ICMP-like functionality
to the system.

A delivery notification message SHOULD be generated when an entity
receives or is about to receive an message having the "deliveryReceipt"
attribute specified as true. The notification message MAY be generated
at the destination of message delivery or at the router on the path when
there is issue to pass the message on, e.g. message validation fails or
the router couldn't find next hop to deliver the message.

The Delivery notification message object is a subclass of generic
message object. In order for a delivery notification message to be
considered valid, the following attributes MUST be set as hereby
described:

  ----------------- -------------------------------------------------------------------------------------------------------------------------------
  **Attribute**     **Valid values**
  type              "deliveryNotification"
  to                The "to" MUST be the entity that this notification was generated or, if none, the entity is specified by the Source attribute
  id                Reference to the message because of which this notification was generated
  deliveryReceipt   false
  payload           String
  ----------------- -------------------------------------------------------------------------------------------------------------------------------

The Payload attribute MUST be specified as one of the following values:

  ------------------ ----------------------------------------------------------------------------------------------------------
  **Value**          **Meaning**
  "ok"               Message successfully delivered
  "duplicate"        A message with the same ID was already delivered to the recipient
  "invalid"          The recipient got an invalid message (e.g., transmission error)
  "badDestination"   The intended recipient is unknown or unreachable
  "expired"          The message expired before the actual delivery, according to its "Expiry timestamp" attribute
  "refused"          The message could not be received because of lack of authorization and/or policy settings
  "noReference"      The recipient does not hold a local reference to the message specified by the "In response to" attribute
  ------------------ ----------------------------------------------------------------------------------------------------------

#### 2.3.3 RPC Message Object[¶](#233-RPC-Message-Object)

The RPC Message Object message object is also a subclass of generic
message object. It basically wraps\
[JSONRPC2.0](JSONRPC2.0.html) objects and batches into webinos messages,
hence concepts, terminology, payload syntax and semantics, and behaviour
are meant to be aligned with that specification.

A JSON-RPC 2.0 request object or request batch is wrapped into a webinos
RPC request message that, in order to be considered valid, MUST have the
following attributes set as hereby described:

  --------------- ----------------------------------------------
  **Attribute**   **Valid values**
  type            "JSONRPC20Request"
  id              Identity of the RPC request message
  payload         JSON-RPC 2.0 request object or request batch
  --------------- ----------------------------------------------

When an entity offering RPC interfaces receives an RPC request message
that does not contain a notification or a notification-only batch and
said entity is a primary recipient of that message, it SHOULD generate
and send an RPC response message, possibly according to specific policy
rules.

Similarly to webinos RPC request messages, a JSON-RPC 2.0 response
object or response batch is wrapped into a webinos RPC response message
that, in order to be considered valid, MUST have the following
attributes set as hereby described:

  --------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Attribute**   **Valid values**
  type            "JSONRPC20Response"
  to              The "to" set MUST contain only a reference to the entity specified by the "to" attribute in the RPC request message because of which this RPC response message was generated
  id              Reference to the RPC request message because of which this RPC response message was generated
  payload         JSON-RPC 2.0 response object or response batch
  --------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Note**: the JSON-RPC 2.0 specification states that notifications MUST
NOT be replied to, and the same holds true for this specification;
nevertheless it is still possible to use the "deliveryReceipt" attribute
to be informed about the delivery of an RPC request message, even if it
contains a notification or a notification-only batch.

This protocol is meant to be automatically handled by the WRT without
requiring any extra effort on the developer side: the message Handling
API and the routing manager SHALL prevent applications from creating and
receiving messages whose type is "JSONRPC20Request" or
"JSONRPC20Response", while it SHALL be possible to expose RPC interfaces
by describing them in the config.xml file, as specified in the
Foundations section of this specification, and the WRT SHALL
automatically create functions with corresponding names into the local
JavaScript object that represents a discovered service, mapping calls to
those functions to asynchronous RPC requests and responses operated via
this protocol.

#### 2.3.4 PROP Message Object[¶](#234-PROP-Message-Object)

PROP message type is created by webinos for TLS session set-up and
communications between webinos core components. It MUST have the
following attributes set as hereby described:

  --------------- -------------------------------
  **Attribute**   **Valid values**
  type            "Prop"
  to              destination entity
  id              Reference to the Prop message
  payload         Prop message body
  --------------- -------------------------------

3. JavaScript APIs[¶](#3-JavaScript-APIs)
-----------------------------------------

The message handling functionality SHALL be available to application and
third-party developers through the webinos App2App Messaging API.

See the API specification for further details:
<http://dev.webinos.org/specifications/new/app2app.html>

4. Dependencies on other components[¶](#4-Dependencies-on-other-components)
---------------------------------------------------------------------------

### 4.1 Policy Enforcement[¶](#41-Policy-Enforcement)

policy enforcement, to ensure that local policy settings allow for the
message to be further processed;\
Policy enforcement of messages coming from remote sources SHALL be
performed once per local recipient, so that individual failures SHALL
only affect one message/recipient combination. Failures during the
policy enforcement phase SHALL prevent the message from being further
processed for that message/recipient combination.

Local policy rules are also implementation-defined, hence not described
in this specification. Again, if the local policy prevents the message
from being delivered and the message source (forwarding source, or, if
none, original source) does not reside on the device and the message has
the "Delivery notification wanted" attribute specified as true, a
"refused" delivery notification message SHOULD be automatically
generated by the WRT and sent back to the source.

5 References[¶](#5-References)
------------------------------

### 5.1 JSONRPC2.0[¶](#51-JSONRPC20)

<http://www.jsonrpc.org/specification>

