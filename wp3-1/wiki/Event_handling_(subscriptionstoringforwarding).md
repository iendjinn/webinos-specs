Event handling (subscriptionstoringforwarding)[¶](#Event-handling-subscriptionstoringforwarding)
================================================================================================

Partners Involved in this Theme[¶](#Partners-Involved-in-this-Theme)
--------------------------------------------------------------------

According to the [minutes from Turin](minutes%20from%20Turin.html)

-   ISMB (Primary)
-   Samsung
-   W3C
-   TNO

*Security and privacy contacts: Samsung, W3C.*

Requirements[¶](#Requirements)
------------------------------

  ------------------ ------------------ ------------------ ------------------
  **ReqID**          **Requirement**    **XMPP**           **Notes**

  NM-DEV-FOKUS-001   It SHALL be        Yes                
                     possible to                           
                     exchange                              
                     information                           
                     between multiple                      
                     entities in terms                     
                     of events.                            

  NM-DEV-FOKUS-002   It SHALL be        Yes                Where should the
                     possible to                           subscribtion be
                     subscribe to                          stored? (online /
                     certain event                         offline scenario)
                     types in order to                     
                     get notified if                       
                     the related event                     
                     occurs.                               

  NM-DEV-FOKUS-003   It SHALL be        Yes                
                     possible to                           
                     subscribe to                          
                     events that are                       
                     created by a                          
                     specific event                        
                     source in order to                    
                     get notified about                    
                     any event that                        
                     occours at the                        
                     related event                         
                     source.                               

  NM-DEV-FOKUS-004   It SHALL be        Yes                
                     possible to                           
                     unsubscribe from                      
                     notifications                         
                     about a certain                       
                     event.                                

  NM-DEV-FOKUS-005   It SHALL be        Yes                
                     possible to                           
                     specifiy a time                       
                     frame that defines                    
                     until when an                         
                     event should be                       
                     deliverd to its                       
                     destinations                          
                     before it is                          
                     marked as outdated                    
                     and no further                        
                     deliveries are                        
                     tried.                                

  NM-DEV-FOKUS-006   The event source   Yes                Only by 1-to-1
                     SHALL be able to                      messaging.
                     specifiy that it                      
                     will be informed                      
                     about successfull                     
                     or unsuccessfull                      
                     event delivery.                       

  NM-DWP-ISMB-001    Incoming and       Yes                
                     outgoing messages                     
                     that are yet to be                    
                     delivered SHALL be                    
                     cached.                               

  NM-USR-ISMB-002    The user SHALL be                     Handled by the
                     notified of remote                    run-time
                     requests that did                     
                     not originate from                    
                     intervention of                       
                     the user himself                      
                     or that                               
                     necessarily                           
                     require the user                      
                     to authenticate                       
                     himself, according                    
                     to user                               
                     preferences.                          

  NM-DWP-ISMB-003    When an event      Yes                Using pub-sub
                     source publishes                      
                     an event, the                         
                     Webinos system                        
                     SHALL distribute                      
                     it to all                             
                     subscribed and                        
                     authorized                            
                     destinations.                         

  NM-DWP-ISMB-004    The Webinos system                    Handled by the
                     SHALL start/awake                     run-time.
                     applications                          
                     invoked by/waiting                    
                     for an event, when                    
                     it occurs, in a                       
                     controlled manner.                    

  NM-USR-ISMB-005    Notifications MAY  Yes                
                     involve asking the                    
                     user for some                         
                     input or allowing                     
                     the user to                           
                     initiate some                         
                     action from within                    
                     the notification                      
                     context.                              

  NM-DWP-ISMB-006    The Webinos system Yes                
                     SHALL be able to                      
                     retrieve Metadata                     
                     about an occurring                    
                     event.                                
  ------------------ ------------------ ------------------ ------------------

**Event description**

  ------------------ ------------------ ------------------ ------------------
  **ReqID**          **Requirement**    **XMPP**           **Notes**

  NM-DEV-FOKUS-101   Events MUST be     Yes                
                     distinguishable in                    
                     order to decide if                    
                     the same event                        
                     occoured multiple                     
                     times or the same                     
                     event was                             
                     delivered multiple                    
                     times.                                

  NM-DEV-FOKUS-102   An event SHALL     Yes                
                     provide                               
                     information about                     
                     its type in order                     
                     to distinguish                        
                     between different                     
                     events.                               

  NM-DEV-FOKUS-103   The event type of  Yes                
                     an event SHALL be                     
                     either one of the                     
                     predefined events                     
                     or an arbitrary                       
                     application                           
                     specific event                        
                     type.                                 

  NM-DEV-FOKUS-104   An event MAY       Yes                In XMPP an event
                     provide                               MUST provide
                     information about                     information about
                     its source, i.e.,                     its source.
                     about the entity                      
                     that created the                      
                     event, in order to                    
                     allow replies.                        

  NM-DEV-FOKUS-105   An event MAY       Yes                
                     specify a set of                      
                     specific                              
                     destinations of                       
                     the event in order                    
                     to restrict the                       
                     visibility of the                     
                     event.                                

  NM-DEV-FOKUS-106   It SHALL be        Yes                
                     possible to                           
                     optionally attach                     
                     payload data to                       
                     events.                               

  NM-DEV-FOKUS-107   The payload data   Yes                But it is limited
                     MAY contain                           to only relative
                     arbitrary                             small pay-loads in
                     application                           XMPP. Larger
                     specific data.                        pay-loads should
                                                           be send
                                                           out-of-band.

  NM-DEV-FOKUS-108   Events SHALL       Yes                
                     provide                               
                     information about                     
                     the date and time                     
                     when the event                        
                     occured resp. when                    
                     the event was                         
                     created.                              

  NM-DEV-ISMB-101    Events MAY be      Yes                
                     associated with                       
                     event-specific                        
                     Metadata.                             
  ------------------ ------------------ ------------------ ------------------

**Predefined Event types**

  ------------------ ------------------ ------------------ ------------------
  **ReqID**          **Requirement**    **XMPP**           **Notes**

  NM-DEV-FOKUS-301   It SHALL be                           Documentation.
                     possible to                           
                     provide a list of                     
                     predefined events                     
                     to the developer.                     

  NM-USR-IBBT-001    It SHALL be        Yes                Handled by the
                     possible to notify                    runtime.
                     the user of newly                     
                     installed                             
                     applications on                       
                     the device the                        
                     applications were                     
                     installed on                          

  NM-USR-IBBT-002    It SHALL be        Yes                Handled by the
                     possible to notify                    runtime.
                     the user of                           
                     application launch                    
                     requests                              

  NM-USR-IBBT-003    It SHALL be        Yes                
                     possible to notify                    
                     the user of                           
                     available updates                     
                     for the Webinos                       
                     runtime and                           
                     applications                          

  NM-DWP-NTUA-001    The System MUST    Yes                However, should
                     set priorities on                     the system set
                     messages of                           priorities are
                     predefined                            should the user or
                     notification                          applications set
                     categories, based                     the priority?
                     on the current                        
                     contextual                            
                     information of the                    
                     device                                

  NM-DEV-NTUA/Ambies The application    Yes                
  ense-002           Developer SHALL be                    
                     able to subscribe                     
                     his application to                    
                     specific                              
                     contextual changes                    
                     of a webinos                          
                     device, in order                      
                     to change                             
                     Applications                          
                     behavior. He MUST                     
                     also be able to                       
                     detect and handle                     
                     changes in context                    
                     by using multiple                     
                     context sources                       
                     for the same                          
                     context.                              

  NM-DEV-NTUA-003    The User MUST be   Yes                
                     able to confirm                       
                     the contextual                        
                     information where                     
                     an application                        
                     subscribes                            
  ------------------ ------------------ ------------------ ------------------

Messaging[¶](#Messaging)
------------------------

By messaging in Webinos we mean all signalling (notifications, data,
queries, context changes, capabilities, service discovery, etc.) that is
needed for Webinos and Webinos applications to operate.

Messaging in Webinos roughly falls apart into 3 different categories.

1.  Messages and notifications needed for management of the Webinos
    cloud.
2.  Messages and notifications about changes in the personal Webinos
    that are of interest for applications.
3.  Messages and notifications originated from applications that can be
    reused by other applications.
4.  Messages and notifications originated from applications meant for
    entities that are not managed by Webinos.

Although the last category of messages does exist, and it is by
definition out-of-scope for the Webinos project, it is good to take this
category into account when discussing the requirements for messaging.

State of art[¶](#State-of-art)
------------------------------

**SIP**

**Pros**

-   Protocol independent of (server) infrastructure
-   Application controlled routing

**Cons**

-   Initialization only
-   Large traffic overhead
-   Weak standard, federation (interconnect) poses problems
-   telco only

**XMPP**

**Pros**

-   Extensible through XEP
-   Federated by nature
-   XMPP also in Javascript
-   Multiple simultaneous resources
-   Many (open source) implementations, also of XEPs
-   Large user base & community

**Cons**

-   TCP/IP only
-   server centric

Answers on XMPP comments in the minuts.[¶](#Answers-on-XMPP-comments-in-the-minuts)
-----------------------------------------------------------------------------------

Is there overlap between XMPP and the work of the W3C working groups on
Web Event, Web Notifications and Real-time Communications?

From what I understand, the W3C WGs are working on APIs that can be used
by web applications to access capabilities that are provided within the
browser. They are not about specifying the underlying protocols that are
used, by the runtime, to communicate over networks. Hence HTTP is not
specified by W3C but by the IETF. The underlying protocols are litarly
put out-of-scope by the real-time communication WG in section 1.2:

"The definition of the network protocols used to establish the
connections between peers is out of scope for this group; in general, it
is expected that protocols considerations will be handled in the IETF."

Our suggestion is to use XMPP as the underlying transport protocol for
communication of messages and events between Webinos enabled entities.
From my perspective the applications that are developed for the Webinos
run-time should be agnostic on the underlying protocols but should use
the W3C APIs where possible. The Webinos run-time itself should know
about the underlying protocols.

In the future, WebSockets can be used to transport XMPP over
back-and-forth between Webinos runtime and server. In current
state-of-the-art this is done via BOSH (Bidirectional-streams Over
Synchronous HTTP specified in XEP-0124).

State of the Art technologies[¶](#State-of-the-Art-technologies)
----------------------------------------------------------------

  ------------------------------------------------------------------------------------------ ---------------------------------- ------------------------ ------------- -----------
  Technology                                                                                 Analysis                           Scope                    Assigned to   Status
  XMPP                                                                                       [XMPP for Event handling](.html)   Network-level routing    ISMB          Completed
  SIP                                                                                        TBD?                               Network-level routing    ?             TBD?
  MQTT                                                                                       TBD?                               Network-level routing    ?             TBD?
  PubSubHubbub                                                                               TBD?                               Network-level routing    ?             TBD?
  WebSockets                                                                                 TBD?                               Network-level routing?   ?             TBD?
  Web Notifications                                                                          TBD                                Notifications            ?             TBD
  [Desktop Notifications Specification](http://www.galago-project.org/specs/notification/)   TBD                                Notifications            ?             TBD
  ------------------------------------------------------------------------------------------ ---------------------------------- ------------------------ ------------- -----------

Draft architecture[¶](#Draft-architecture)
------------------------------------------

[Event handling deliverable](.html) (work in progress)

*Feedback welcome. Put comments inline with you name/company and using
block quotes (e.g., \> Stefano/ISMB: blah blah blah.).*

### Overview[¶](#Overview)

The event handling area is concerned with data exchange in terms of
events among non-human addressable entities (e.g., applications,
services, devices).

It relies on webinos' overlay networking model and
device/service/application discovery facilities to provide means for
communicating, and provides mechanisms to describe, encapsulate, send
and process event data.

The proposed architecture employs a simple but easily extensible design,
and defines the core protocols for relatively advanced features such as
RPC and publication/subscription functionality.

### Actors[¶](#Actors)

Addressable entities, as specified by the requirements, include:

-   devices;
-   device features;
-   applications;
-   services;
-   application instances;
-   service instances. (?)

Furthermore, we do also require that PubSub nodes (see below) MUST be
addressable.

> Stefano/ISMB: a PubSub kind-of-thing is not explicitly mentioned in
> the requirements, should it be added?

### Event format[¶](#Event-format)

Each event MUST contain:

  -------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ------------------------------------------------------------------------------------------------------------------- ---------------------------
  Field          Description                                                                                                                                                                                                                                                                                                                                                    JS representation                                                                                                   Transmitted as
  Type           identifier for the event type - this field does also determine the semantics of the payload field, if present                                                                                                                                                                                                                                                  string other than "any" (reserved) and that would be a valid identifier in JS (regexp: [\_a-zA-Z][\_a-zA-Z0-9]\*)   string
  Source         the original entity sending the message                                                                                                                                                                                                                                                                                                                        proxy object                                                                                                        address string
  Destinations   the entities that the event is originally sent to - each destination must also be associated with a destination type that specifies whether the destination is a primary recipient (like 'To:' in emails), a secondary recipient (like 'Cc:' in emails) or that the recipient is meant to receive a "blind carbon copy" of the event (like 'Bcc:' in emails)   3 arrays of proxy objects                                                                                           3 sets of address strings
  -------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ------------------------------------------------------------------------------------------------------------------- ---------------------------

and MAY optionally contain:

  ------------------------------ ------------------------------------------------------------------------------------------------------------------------------------------------ ------------------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Field                          Description                                                                                                                                      JS representation                     Transmitted as
  ID                             identifier of this specific event                                                                                                                SHA-256 hash string                   string
  In response to                 identifier of the original event that this event is a response to                                                                                SHA-256 hash string                   string
  Generation timestamp           moment in time in which the event is generated by the original event source                                                                      Date object                           string indicating milliseconds since 1970/01/01 (UTC) formatted in base 10 (i.e., à la printf("%u", milliseconds)![;)](/redmine/plugin_assets/redmine_wiki_extensions/images/wink.png)
  Expiry timestamp               moment in time past which the event is no more valid/meaningful                                                                                  Date object                           string indicating milliseconds since 1970/01/01 (UTC) formatted in base 10 (i.e., à la printf("%u", milliseconds)![;)](/redmine/plugin_assets/redmine_wiki_extensions/images/wink.png)
  Delivery notification wanted   flag indicating that the event source wants to be notified by the event destination(s) about the result of the event delivery (default: false)   boolean value                         "true" or "false"
  Cacheable                      flag indicating whether the event should be stored and forwarded later if a destination is currently unavailable (default: false)                booelan value                         "true" or "false"
  Forwardings                    list of forwardings (may be partial) the event was subject to                                                                                    ordered array of forwarding objects   ordered set of forwarding couples/triples ([source, destinations] or [source, destinations, timestamp])
  Payload                        event type-specific data                                                                                                                         string                                string
  ------------------------------ ------------------------------------------------------------------------------------------------------------------------------------------------ ------------------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Furthermore, if the event was forwarded, the event SHOULD contain the
source, destination and timestamp for each forwarding, and, in
particular, it MUST contain such information (the timestamp being
optional) w.r.t. the last forwarding.

> Stefano/ISMB: note on forwarding: in case we are concerned about the
> possibility of allowing applications to "synthesize" events claiming
> they come from an unaware source and asking for forwarding to the
> runtime, a simple way to prevent that would be to add to events one or
> more non JS-visible fields at the browser plugin level.

> Stefano/ISMB: requirement NM-DEV-FOKUS-108 is questionable, in that it
> is not clear why every event needs a generation timestamp and what's
> the difference between event occurrence and event generation; it
> doesn't even link to any use case and in the notes you read "Just an
> example"... the current architecture makes event generation timestamps
> optional instead, that means that the requirement should probably be
> changed.

Applications SHALL be allowed to act on the behalf of the entities they
"own", i.e., they can generate events whose source is the owned entity
and they will receive the events whose destination is the owned entity.

> Stefano/ISMB: How that ought to be implemented in a secure and
> reliable way is heavily dependent on a number of very high level
> issues that go well beyond the scope of this area.

The event identifier is determined by performing a SHA-256 hash on the
one-to-one string serialization hereby described; the event ought to be
serialized into a string with format using the "transmitted as"
representation and using no characters for unspecified fields:

> type|source|{to\_dest\_1|to\_dest\_2|...|to\_dest\_n}{cc\_dest\_1|cc\_dest\_2|...|cc\_dest\_n}{bcc\_dest\_1|bcc\_dest\_2|...|bcc\_dest\_n}|in-response-to|generation-timestamp|expiry-timestamp|delivery-notification-wanted|cacheable|payload

> Stefano/ISMB: this has the following implications:
>
> the identifier need not to be transmitted, since it can always be
> determined from the content of the event object itself - it may
> however be transmitted to perform an extra integrity check
>
> special care should be put when performing stateful RPC or secure
> communication: since two different events with same content will lead
> to the same ID, the following countermeasures should be taken not to
> confuse them:
>
> -   if it is reasonable to assume that two or more such events cannot
>     be generated by the same source within 1 ms, requiring the use of
>     the timestamp is sufficient to ensure that IDs will be different;
> -   otherwise, a sensible solution might be requiring some
>     state-related information to be present (e.g., requiring that the
>     "In response to" field is always specified and/or requiring the
>     use of a sequence counter in the payload).

### Delivery notifications[¶](#Delivery-notifications)

Delivery notifications have the type field set to
"deliveryNotification", **mandatory** "In response to" field set and
**mandatory** payload that indicates the delivery status of the event in
question.

The payload data can be: "delivered", "failed" or "cached".

### RPC messages[¶](#RPC-messages)

RPC messages have the type field set to "rpc" and **mandatory** payload
consisting of [JSON-RPC
2.0](http://groups.google.com/group/json-rpc/web/json-rpc-2-0) data.

In particular, responses (i.e., RPC messages containing Response
objects) MUST also have the "In response to" field set.

RPC messages cannot be sent to users and requiring user intervention to
determine the result of an RPC request is highly discouraged.

> Stefano/ISMB: Rationale: notifications and questions to the user are
> more likely to be stored and no assumptions could realistically be
> made on the user's behavior.

### Publication/subscription[¶](#Publicationsubscription)

Publication/subscription works by active entities publishing or
subscribing to "PubSub nodes", that are passive entities holding
collections of events.

Four kinds of actors are involved in the management of a node:

1.  provider (cardinality: 1): the active entity that logically manages
    the storage of the PubSub node and that "runs the node" (i.e.,
    receives and forwards messages from/to other involved actors).
2.  owner (cardinality: 1): the active entity that manages the lifecycle
    of the node and its configuration, including
    publication/subscription policy.
3.  publisher (cardinality: any): an entity that publishes content to
    the node.
4.  subscriber (cardinality: any): an entity that receives updates
    regarding the node content.

**N.B.**: the provider and the owner MUST be single entites, but that
doesn't mean they have to be single application instances. Indeed,
application/service types are single entites, but MAY (SHOULD/SHALL?)
refer to any number of instances.

> Stefano/ISMB: Actually, XMPP allows to have multiple owners for a
> PubSub node.

When a publisher publishes content to a PubSub node, the provider entity
SHALL try to transmit it to all subscribers.

In other words, PubSub nodes represent a further level of indirection
used to transmit data to "interested and authorized active entities"
without specifying them explicitly.

Note that PubSub nodes may be themselves publishers or subscribers to
other PubSub nodes; this provides a conceptually simple mean to do
collection and/or forwarding of events in a more complicated fashion
than with single PubSub nodes. The subscription of a node to another
node may only be requested by the owner of the subscribing node and MUST
be controlled/authorized by the provider entity in order to avoid
creating loops. Furthermore, the provider SHOULD ensure that a PubSub
node never contains two copies of the same event.

A discovery mechanism for PubSub nodes SHALL be provided.

> Stefano/ISMB: IMO the discovery mechanism should be formalized in the
> "device, service, application discovery" area. PubSub nodes may,
> hence, be services or part of (a) service(s).

#### PubSub node configuration[¶](#PubSub-node-configuration)

##### Persistence

-   Persistent nodes: meant to be alive until explicit destruction -
    e.g., RSS-like streams, if the owner entity is not present (e.g.,
    application/service crash, device disconnected) they continue to be
    available;
-   Temporary nodes: automatically destroyed by the provider when the
    owner is no more present - e.g., IPC among different
    application/service instances;

**N.B.**: "presence" means different things in different contexts and
w.r.t. different entities. Nevertheless we define presence of one entity
w.r.t. another as the logical conjunction of the entity existence and
availability - in other words, an entity is present to another entity if
it exists (e.g., an application instance exists as long as it runs) AND
there is a way to transport data between the two (e.g, connection -
direct or indirect) AND the policies of all involved entities (both
entities plus others in the middle, if any) allow for each other to
exchange presence information.

> Stefano/ISMB: in case XMPP is chosen, the WRE SHALL ensure that the
> following conditions are met:
>
> -   as soon as a new addressable entity becomes available, it SHALL
>     force broadcasting of its presence information (e.g., as per RFC
>     3921, it SHALL send a presence stanza with no type attribute to
>     the server);
> -   it SHALL keep track of remote temporary nodes created by active
>     entities running on it in order to ensure their destruction in
>     case of "sudden disconnection" as soon as the device regains
>     connectivity to the provider (XMPP lacks self-destruction of
>     PubSub nodes).
>
> At this point one serious problem remains: in case of "sudden
> disconnection" of the owner entity (whether temporary or not), the
> remote temporary nodes still exist and may even still allow
> subscriptions, publishing, etc. One possible solution to this problem
> is to have yet another remote proxy entity that is somehow guaranteed
> to be (almost) always connected to the provider, so that it appears as
> the owner of the node to the XMPP server, but it basically just
> forwards requests from the logical owner entity and manages the
> destruction of temporary nodes itself.
>
> Another (easier) option is to use BOSH to avoid node destruction in
> case of temporary connection losses.

##### Discoverability

The discoverability options for a PubSub node should be the same or
aligned with the discoverability options for services in Webinos.

> Stefano/ISMB: in a certain sense a PubSub node may actually be
> considered as a "passive service".

> Stefano/ISMB: discoverability options idea: open access, whitelist,
> blacklist, authorization request forwarded to the owner, special rules
> (e.g., discoverable if the discovering entity is a user in the
> "owner's roster", non discoverable by users, discoverable by
> applications).

##### Publication/subscription policy

The options for publishing/subscribing to a PubSub node should be the
same or aligned to those for accessing a service in Webinos.

> Stefano/ISMB: one more reason to consider PubSub nodes as services.
> This has interesting consequences w.r.t. the application/service
> distinction problem... idea: a service might be a passive entity
> managed by one or more applications, maybe?

*more configuration options?*

#### PubSub node requests[¶](#PubSub-node-requests)

##### Node creation

The requesting active entity, that in case of success will be the owner
of the newly created node, SHALL send an event to the provider entity,
optionally specifying:

-   the node persistence (i.e., persistent vs temporary, default:
    temporary);
-   the node identifier (default: automatically generated);
-   node configuration key/value pairs (see Node configuration, default:
    default configuration).

The request SHALL fail if (the following list is non-exhaustive):

1.  the requesting entity is known not to be an active entity;
2.  the receiving entity is not a provider of PubSub nodes;
3.  the requesting entity is not authorized to create PubSub nodes;
4.  the requested node identifier already exists.

Except in cases 1 and 2, if the request fails, the receiving entity
SHOULD report the error condition to the sender.

If, instead, the request was successful, the provider SHALL try to
notify the owner about the success in creating the node, along with the
assigned node identifier and SHALL be automatically given publishing
rights.

TODO: syntax of request, syntax/semantics of responses.

##### Node destruction

###### Case 1: the owner asks the provider for node destruction

The owner of a node sends a node destruction request to the node
provider. Such request shall specify the identifier of the node to be
destroyed.

The request SHALL fail if (the following list is non-exhaustive):

1.  the requesting entity is known not to be an active entity;
2.  the receiving entity is not a provider of PubSub nodes;
3.  the specified node does not exist;
4.  the requesting entity is not the node owner.

Except in cases 1 and 2, if the request fails, the receiving entity
SHOULD report the error condition to the sender.

If, instead, the request was successful, the provider SHALL try to
notify the owner about the success in destroying the node and SHOULD
notify all publishers and subscribers other than the node owner about
the destruction of the node.

TODO: syntax of request, syntax/semantics of responses.

###### Case 2: the node is automatically destroyed by the provider

In case the owner of temporary nodes becomes no more present, the
provider(s) of such nodes SHALL destroy them and SHOULD notify all
publishers and subscribers other than the node owner about the
destruction of the node.

TODO: syntax/semantics of destruction notification.

###### Case 3: the provider decides to destroy the node

The provider SHALL be able, in any moment and for whatever reason, to
destroy a PubSub node.

In those cases it SHOULD notify the owner, all publishers and
subscribers about the node destruction.

TODO: syntax/semantics of destruction notification.

##### Getting node configuration

The owner SHALL be able to retrieve the node configuration by sending a
node configuration retrieval request to the provider specifying the node
identifier.

The request SHALL fail if (the following list is non-exhaustive):

1.  the requesting entity is known not to be an active entity;
2.  the receiving entity is not a provider of PubSub nodes;
3.  the specified node does not exist;
4.  the requesting entity is not the node owner.

Except in cases 1 and 2 (and maybe 3 as well?), if the request fails,
the receiving entity SHOULD report the error condition to the sender.

If, instead, the request was successful, the provider SHALL send a
response to the sender containing a list of key/value pairs representing
all node configuration settings for the specified node.

TODO: syntax/semantics of key/value pairs, syntax of response.

##### Configuring a node

The owner SHOULD be able to configure the node by sending a node
configuration request to the provider, specifying:

-   the node identifier;
-   one or more node configuration key/value pairs.

Such key/value pairs represent a node configuration setting, where the
key serves as the configuration option identifier and value is the
requested settings and has option-specific syntax.

The request SHALL fail if (the following list is non-exhaustive):

1.  the requesting entity is known not to be an active entity;
2.  the receiving entity is not a provider of PubSub nodes;
3.  the specified node does not exist;
4.  the requesting entity is not the node owner;
5.  one or more key/value pairs are invalid;
6.  the requested settings are not supported;
7.  the request cannot be satisfied because of the provider's policy
    settings.

Except in cases 1 and 2 (and maybe 3 as well?), if the request fails,
the receiving entity SHOULD report the error condition to the sender.

If, instead, the request was successful, the provider SHALL try to
notify the owner about the success of the operation and SHOULD notify
those publishers and subscribers, other than the node owner, for which
that MAY have consequences in the usage of the node.

TODO: syntax/semantics of key/value pairs, detailed notification
behavior.

##### Getting affiliations

The owner SHOULD be able to request the status of affiliations (i.e.,
the list of publishers and subscribers) to the provider by sending an
affiliation retrieval request specifying the node identifier.

The request SHALL fail if (the following list is non-exhaustive):

1.  the requesting entity is known not to be an active entity;
2.  the receiving entity is not a provider of PubSub nodes;
3.  the specified node does not exist;
4.  the requesting entity is not the node owner.

Except in cases 1 and 2 (and maybe 3 as well?), if the request fails,
the receiving entity SHOULD report the error condition to the sender.

If, instead, the request was successful, the provider SHALL send a
response to the sender containing a list of key/value pairs where each
key represents an affiliated entity and the value represents the kind of
affiliation (publisher, subscriber or both) that the entity represented
by the key has w.r.t the node.

TODO: syntax of key/value pairs, syntax of response.

##### Setting affiliations

The owner SHOULD be able to modify affiliations to the node by sending
an affiliation change request to the provider, specifying:

-   the node identifier;
-   one or more node affiliation key/value pairs.

Such key/value pairs represent an entity affiliation to the node, where
the key represents an affiliated entity and the value represents the
kind of affiliation (none, publisher, subscriber or both) that the
entity represented by the key will have w.r.t the node.

The request SHALL fail if (the following list is non-exhaustive):

1.  the requesting entity is known not to be an active entity;
2.  the receiving entity is not a provider of PubSub nodes;
3.  the specified node does not exist;
4.  the requesting entity is not the node owner;
5.  one or more key/value pairs are invalid.

Except in cases 1 and 2 (and maybe 3 as well?), if the request fails,
the receiving entity SHOULD report the error condition to the sender.

If, instead, the request was successful, the provider SHALL try to
notify the owner about the success of the operation and SHOULD notify
those entities affected by the change.

TODO: syntax/semantics of key/value pairs, detailed notification
behavior.

##### Publish authorization

Entities SHALL be able to ask for publishing rights authorization to the
provider, specifying the PubSub node identifier.

The request SHALL fail if (the following list is non-exhaustive):

1.  the receiving entity is not a provider of PubSub nodes;
2.  the specified node does not exist;
3.  the node configuration does not allow the requesting entity to be
    granted publishing rights for that node.

Furthermore, according to the node's publication/subscription policies,
the request MAY be forwarded to the node owner and a notification about
that MAY be sent to the requesting entity.

Except in case 1, if the request fails, the receiving entity SHOULD
report the error condition to the sender.

If, instead, the request was successful, the provider SHOULD try to
notify the owner and the newly added publisher about the success of the
operation.

TODO: syntax of request, syntax/semantics of responses.

> Stefano/ISMB: this is different from XMPP, where the owner does add
> publishers to the node. However a mapping is still possible by
> requiring to have the owner's JID in the discoverable node metadata.
> IMO, our approach is generally better than XMPP's, since it allows to
> automatically assign or reject publish authorization, when the policy
> is configured in that way, thus reducing the complexity of the owner
> and the amount of generated traffic.

##### Subscription

Entities SHALL be able to ask for subscription to the provider,
specifying the PubSub node identifier.

The request SHALL fail if (the following list is non-exhaustive):

1.  the receiving entity is not a provider of PubSub nodes;
2.  the specified node does not exist;
3.  the node configuration does not allow the requesting entity to be
    subscribe to that node.

Furthermore, according to the node's publication/subscription policies,
the request MAY be forwarded to the node owner and a notification about
that MAY be sent to the requesting entity.

Except in case 1, if the request fails, the receiving entity SHOULD
report the error condition to the sender.

If, instead, the request was successful, the provider SHOULD try to
notify the owner and the newly added subscriber about the success of the
operation.

TODO: syntax of request, syntax/semantics of responses.

##### Publication

A publisher entity SHALL be able to publish content to a PubSub node by
sending a publishing request to the provider, specifying the PubSub node
identifier and the content to be published.

The request SHALL fail if (the following list is non-exhaustive):

1.  the receiving entity is not a provider of PubSub nodes;
2.  the specified node does not exist;
3.  the requesting entity is not a publisher for the specified node.

Except in case 1, if the request fails, the receiving entity SHOULD
report the error condition to the sender.

If, instead, the request was successful, the provider SHALL try to
notify the requesting publisher about the success of the operation and
SHALL try to forward the published content to all subscribers.

TODO: syntax of request, syntax/semantics of responses.

### Event routing[¶](#Event-routing)

#### Application/service instance-level routing[¶](#Applicationservice-instance-level-routing)

![](ev_instance_routing.png)

##### Event generation and listening

From the applicaiton/service developer point of view, the handling of
simple events reduces to two basic concepts: generating new events and
registering listeners for incoming events.

The event handling Javascript API will be asynchronous, hence the
application/service developer will provide callbacks implementing the
listeners and to be notified of the result of sending an event (success,
failure, cached, others?).

Event sources and event destinations will be in a 1:N relationship in
the general case, hence multiple listeners will be able to listen to the
same event.

###### Delivery notification

A delivery notifications is an event that is sent in response to another
event explicitly asking for it via the "Delivery notification wanted"
field (see Event format).

TBC

###### Event forwarding

TBD

##### PubSub node requests

The PubSub API will be built on top of the event handling API, that
implies, among other things, that it will be completely asynchronous.

An instance SHALL be able to become PubSub node provider if authorized
(e.g., stated in the application manifest - to be decided), and the WRE
shall provide a default and extensible/"hookable" PubSub API and
implementation to build upon, if needed.

> Stefano/ISMB: this is to gain better scalability, modularity,
> concurrency, security and reduce device-level traffic... on the other
> hand it makes no sense to have this "centralized" in the WRE, since,
> being the PubSub implementation completely event-based, it would be
> easy to build equivalent mechanisms at an application level. In other
> words it's way better to provide an extensible API/implementation
> rather than trying to force everybody to use a "closed" one, thus
> avoiding the risk of having people implementing their own incompatible
> mechanisms. In case moving PubSub traffic back and forth the provider
> application results too heavy, it should be possible to have the
> default mechanism implemented by the WRE, and overridden only if/when
> requested by the provider application itself.

##### Dispatcher

![](ev_instance_disp.png)

(dashed lines: PubSub node requests from/to other addressable entities)

FIXME: instance-specific PubSub nodes make no sense, those should be
removed from the drawing above.

The event dispatcher is a logical unit that represents the event
processing mechanism hidden to the application developer.

Its input and output event queues are meant to be provided by the event
handling Javascript implementation, while the routing part (i.e., the
actual moving of data from the application to the outside and viceversa)
is up to the browser plugin.

In particular, the browser plugin is expected to process events in the
browser's event loop (e.g., by adding a hook into that loop - the whole
process could either be done in native code or there could be a JS part
too - this, however, is abstracted away by the proposed design).

Event queues are needed in order for the API to be asynchronous (e.g.,
multiple sends between two event loop executions).

On instance destruction, events in the out queue will be forwarded,
while events in the in queue will either be discarded (messages to the
specific instance, messages to the application/service type while there
are other such application/service instances that have received the same
message) or put back into the WRE cache (all other cases).

##### API mockup

###### Basic eventing

webinos.Event = function(type, to, cc, bcc, from, respTo, timeStamp,
expireStamp, notifyMe, data, id)

> Event object constructor

webinos.addListener = function(cb, source, type)

> Adds a listener callback (cb) for events of the specified type (type)
> and generated by the specified source (source). If type or source (or
> both) is (are) null, no filtering w.r.t. that parameter is done (e.g.,
> if both are null, the listener callback catches all incoming events).
>
> Returns a string that uniquely identifies the listener.

webinos.removeListener = function(id)

> Removes the listener callback identified by the given id string.

webinos.sendEvent = function(evt, cb)

> Sends the evt event object; cb, if specified, is the callback for
> being notified of the sending status.

###### RPC

TBD

###### PubSub

TBD

#### Device-level routing[¶](#Device-level-routing)

![](ev_device_routing.png)

The WRE Browser Plugin handles events (creates events into in queues and
deletes them from out queues, calls Javascript callbacks) and routes
messages among applications/services/WRE and from/to "the outside".

Device-specific PubSub nodes and event cache are located in either the
HTML/JS part of the WRE, or in the Browser Plugin (which is more
convenient? – to be decided).

> Stefano/ISMB: IMO the Browser Plugin should be “as stateless and small
> as possible”, hence PubSub nodes and event cache should belong to the
> HTML/JS part.
>
> WRE HTML/JS could also be made of a number of separate “special
> services” rather than one big thing - there is a parallel to the OS
> development world: microkernel vs monolithic kernels.
>
> I tend to like a hybrid approach, where the browser plugin could just
> implement the kind of event-based IPC+networking described here, a
> limited set of relatively low-level device APIs that only the HTML/JS
> "daemons" belonging to the WRE can directly access, and another
> limited set of application/service-level APIs that need to be
> synchronous, hence cannot be event-based.
>
> Then, if all synchronous APIs are stateless, it means that all of the
> state is in Javascript form, hence easily serializable to, e.g., JSON.
> This could heavily simplify state/session management (e.g., state
> could be split in device-state-specific data and WRE/application-state
> data, that is the session).
>
> Then we would have all the benefits of microkernel-like systems
> (isolation of faulty components with the possibility to restart them
> on crash and/or to substitute them on the fly).

#### Network-level routing[¶](#Network-level-routing)

![](ev_net_routing.png)

Events will be routed according to the mechanisms/mappings specified in
the "overlay network" area.

> Stefano/ISMB: I advocate the use of XMPP since it is quite close
> already to what we want to do. The domain, user and device part would
> map to the JID, and would suffice to establish a connection, even if
> the parties don't have public IP addresses.
>
> It would make things like remote device/service/application discovery
> trivial to do (also because we would have the same addressing scheme
> for anything that's Webinos-enabled).
>
> Furthermore, it does support P2P communication already. We could
> either use their solution, that implies using Zeroconf, but I think it
> would be better to provide our own, which to me looks all but
> difficult to do and which would allow us to gain in integration (e.g.,
> we might want to use UPnP instead, or support both, or DPWS).

##### Client-server communication

TBD

##### P2P networks

TBD

##### NAT traversal

TBD

#### Caching (storing/forwarding)[¶](#Caching-storingforwarding)

TBD

External resources that may be of interest (or maybe not)[¶](#External-resources-that-may-be-of-interest-or-maybe-not)
----------------------------------------------------------------------------------------------------------------------

-   [The XMPP Standards Foundation](http://xmpp.org/)
-   [Professional XMPP Programming with JavaScript and
    jQuery](http://professionalxmpp.com/) - introductory book on JS XMPP
    programming
-   [Strophe.js](http://code.stanziq.com/strophe/) - an excellent
    JS-only XMPP implementation
-   [node.js](http://nodejs.org/) - if you manage to grasp a basic
    understanding of its reason of being, activate two or three neurons
    in your brain and connect a couple of dots, you might be enlightened
    on why event handling + RPC in JS might be a good idea
-   [W3C DOM Level 2 Events
    specification](http://www.w3.org/TR/DOM-Level-2-Events/) - W3C
    Recommendation (we can/should reuse part of its [IDL
    definitions](http://www.w3.org/TR/DOM-Level-2-Events/idl-definitions.html)
    for non-DOM events as well)
-   [W3C DOM Level 3 Events
    specification](http://www.w3.org/TR/DOM-Level-3-Events/) - W3C
    Working Draft
-   [W3C Server-Sent Events](http://dev.w3.org/html5/eventsource/) - W3C
    Editor's Draft
-   [W3C HTML5 Web Messaging](http://www.w3.org/TR/webmessaging/) - W3C
    Working Draft
-   [Dojo Topic System](http://docs.dojocampus.org/quickstart/topics) -
    a JS PubSub-kind-of-thing -
    [here](http://weblog.bocoup.com/publishsubscribe-with-jquery-custom-events)
    is an interesting benchmark comparing it to [a jQuery
    plugin](http://higginsforpresident.net/js/static/jq.pubsub.js) ...
    the main difference between the two is that the latter also deals
    with DOM and bubbling - the numbers do look promising (the former
    has timings \< 10us per event on both Firefox and Chrome!)
-   [pmrpc](http://code.google.com/p/pmrpc/) - JavaScript library for
    message passing, remote procedure call and publish-subscribe
    cross-contex communication in the browser
-   [JSON-RPC](http://json-rpc.org/) - lightweight remote procedure call
    protocol similar to XML-RPC using JSON syntax
-   [SOAPjr](http://www.soapjr.org/) - JSON-based SOAP-like thing
-   [JSON-WSP](http://en.wikipedia.org/wiki/Jsonwsp) - web-service
    protocol that uses JSON for service description, requests and
    responses
-   [JSON Schema](http://json-schema.org/)
-   [JSON Service Mapping Description
    Proposal](http://groups.google.com/group/json-schema/web/service-mapping-description-proposal)
-   [NotifyOSD](https://wiki.ubuntu.com/NotifyOSD)

Does not belong here / postponed / questionable stuff[¶](#Does-not-belong-here-postponed-questionable-stuff)
------------------------------------------------------------------------------------------------------------

### Notifications[¶](#Notifications)

Notification messages can be of two kinds: notification requests and
notification responses.

#### Notification requests[¶](#Notification-requests)

Notification requests have the type field set to *\<TO BE DECIDED\>*,
can only be directed to users and have **mandatory** payload consisting
of the JSON serialization of a notification object.

A notification object MUST contain:

  --------- ------------------------------------------------------------------ -------------------
  Field     Description                                                        JS representation
  Summary   Single line overview of the notification (e.g., "You have mail")   string
  --------- ------------------------------------------------------------------ -------------------

and MAY contain:

  -------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------------------------
  Field                Description                                                                                                                                                                                                                                                                                                           JS representation
  Replaces ID          Event ID of an existing notification that this notification is intended to replace (this also serves to cancel a previous notifications involving user interaction)                                                                                                                                                   hash string
  Urgency level        Integer value that specifies the notification urgency (0 = low, 1 = normal, 2 = critical)                                                                                                                                                                                                                             constant integer numeric value
  Category             URI that indicates the notification type                                                                                                                                                                                                                                                                              URI string
  Icon                 URI that points to the icon file or that embeds image data (using the "data:" URI scheme)                                                                                                                                                                                                                             URI string
  Body                 Longer notification text                                                                                                                                                                                                                                                                                              string containing HTML markup
  Actions              Keyword/description pairs of actions the user can choose, where the keyword is a string that identifies the action and the description is the string that is displayed to the user - there MUST always be a default action identified by keyword "default" and keywords MUST be unique within a notification object   associative array of keyword/description mappings
  Expiration timeout   number of milliseconds since the display of the notification at which the notification should automatically close                                                                                                                                                                                                     numeric value
  -------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------------------------

> Stefano/ISMB: should add human-readable name of the sender?

> Stefano/ISMB: Rationales:
>
> -   URIs for category: possibility to automatically get metadata for
>     unknown categories in the future (e.g., RDF data from the
>     specified URI);
> -   URIs for icons: known URIs will correspond to cached/stored
>     icons - no need to retrieve them again (it should be ok for
>     theming too, the URI points to the default icon, a local setting
>     overrides that), while unknown non-data URIs point to an image
>     that can be just downloaded.

The WRE is responsible for the handling and visualization of incoming
notifications.

> Stefano/ISMB: a (privileged?) API may be offered to intercept,
> interact and/or replace the WRE notification system...

The urgency level parameter does also give an indication on whether a
notification SHOULD be somehow logged/remembered (by default, it should
be the case if it is "normal" or "critical") or not.

> Stefano/ISMB: deliberate vagueness here.

#### Notification responses[¶](#Notification-responses)

Notification responses have the type field set to *\<TO BE DECIDED\>*,
can only be coming from users and have **mandatory** payload consisting
of just the chosen action keyword and **mandatory** "In response to"
field set to the original notification request identifier.

Such events SHALL always have the entity that sent the original
notification as the primary recipient and the receiving user as
secondary recipient, so that all devices owned by the user become aware
of the fact that a response was given (e.g., they can close the
notification).

Normally, responses to notification requests that are somehow
logged/remembered (e.g., having "normal" or "critical" as urgency level)
SHOULD be logged/remembered as well.

