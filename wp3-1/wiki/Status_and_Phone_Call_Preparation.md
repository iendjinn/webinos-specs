WP3 Status and Phone Call Preparation[¶](#WP3-Status-and-Phone-Call-Preparation)
================================================================================

Task 3.1 Work Areas[¶](#Task-31-Work-Areas)
-------------------------------------------

User ID and Data Management[¶](#User-ID-and-Data-Management)
------------------------------------------------------------

### Progress made (with resources expended)[¶](#Progress-made-with-resources-expended)

So far we have achieved (approximately 7.5 PM):

-   investigated in relevant state-of-the-art
-   defined an initial architecture for authentication
-   created use cases to cover the typical cases in which authentication
    is required
-   created sequence diagrams to describe the high level flow of
    messages in these use cases
-   created activity diagrams to draw the big picture of interaction
    with other subtopics
-   built liaisons with other subtopics (Discovery, Overlay Network,
    Privacy & Security, Policy Management)
-   identified user data which is required for identification and
    authentication and which is to be synchronised among all the devices
    of the user
-   defined an initial architecture of where to store user data and how
    to synchronise it

The essentials at a very brief glance:

-   Authentication is different depending on the environment
    -   within a personal zone, authentication is done by using
        pre-shared keys
    -   between devices and services on the Internet, authentication is
        done using an Identity Provider
-   The Identity Provider (IDP) is hosted by any 3rd party who operates
    as certification authority. It can issue identifiers and tokens. The
    tokens are used for Single Sign-on (SSO)
-   Each personal zone has one Personal Zone Hub (PZH) which controls
    identification, addressing and authentication in the zone
    -   The PZH is accessible on the Internet
    -   The PZH has a unique address, represented by a URI
    -   Additional services can be used (e.g. WebFinger) to obtain the
        unique address from some other information (e.g. an email
        address of the user)
    -   The PZH stores
        -   a list of all the devices belonging to the zone
        -   all identifiers of the user and the devices
        -   policies
    -   The store in the PZH is synchronised into a local data cache on
        each device of the zone
    -   Each device has a Personal Zone Proxy (PZP) which has the
        functionality of the PZH in the case that the device cannot
        access the Internet and thus cannot access the PZH
-   Authentication is two way: first user authenticates to one of his
    devices, then this device authenticates to other
    devices/apps/services on behalf of the user

For details, see all the wiki pages on [User Identity and Data
Management](User%20Identity%20and%20Data%20Management.html).

### Planned next steps (actions) + anticipated resources[¶](#Planned-next-steps-actions-anticipated-resources)

Planned to be done during the Berlin meeting (0.2 PM):

-   done Sort out architecture details
-   done Ensure the same common understanding
-   done Decide on the most fundamental open issues
-   in progress Adjust architecture to the decisions
-   half done Synchronise with other sub-topic groups as needed
-   in progress Draft a first set of initial APIs

Planned to be done after the Berlin meeting (May + June; 5 PM):

-   Call with discovery and messaging to go over detailed flows- Nick
-   Finalise all background research work for deliverable - Sven on
    return
-   Update sequence diagrams to align with new architecture - Andrea
-   create intro section draft for deliverable - Nick
-   Frame the anonymised discovery problem, for discussion with 3.5 -
    Andrea
-   First draft if widl api - Nick \*

### Decisions that need to be made – and communicated[¶](#Decisions-that-need-to-be-made-–-and-communicated)

-   Decide on fundamental architecture design: will we have PZP and PZH?
    How is addressing done? - still oustanding - proposal in draft
-   How to identify users, devices, apps, services? Do we need to
    identify all these entities? - still oustanding - proposal in draft
-   How do applications specify their requirements for authentication
    and identity? E.g. how do they state that they need the user to be
    "logged in"? We need to walk-through some examples and work out what
    happens when users have multiple identities or want to remain mostly
    anonymous. ([Issue](Issue.html) 9)
    -   draft concept dicussed at berlin - shall be written up in draft
-   Should the app request and get credentials or is it webinos which
    does all the identification and authentication under the hood?
    ([Issue](Issue.html) 10) In other words, on which layer does
    authentication live in webinos?
    -   application requests - runtime satisfies - to be written up
-   How to authenticate users on devices with limited UI or on devices
    which are used by multiple people (e.g. TV)? ([Issue](Issue.html)
    11)
-   Which security/usability trade-offs are we willing to accept? Some
    design decisions increase usability on the cost of security. One of
    them is the introduction of the PZP and PZH which requires storing
    credential and other sensitive data on each device of the user.
    -   no simple answer
-   Resolve the privacy discovery dilema

### Link to preliminary deliverable structure for this work area[¶](#Link-to-preliminary-deliverable-structure-for-this-work-area)

[Draft Deliverable Structure](Draft%20Deliverable%20Structure.html)

Policy Management[¶](#Policy-Management)
----------------------------------------

### What we decided in Berlin:[¶](#What-we-decided-in-Berlin)

-   We need to investigate the use of POWDER in WAC and whether it is
    sufficient for expressing privacy policies in webinos. Is it
    sufficient for users and applications? If not, we should use Dave's
    suggested reduced P3P work.
-   Policy specification is largely independent of the "in zone" and
    "out of zone" discussion. However, being "in zone" is a
    pre-requisite for many policies to apply.
-   Policy synchronisation needs more work, in particular handling
    conflicts. We decided to make the structure of policy storage as
    fine-grained as possible so the impact is limited
-   Yes, we need to work through policies that refer to non-webinos
    devices.
-   Access control decisions should trigger new "events"
-   Obligation policies will not be specified in XACML but rather will
    be implementable as event handlers
-   Delegation policies: we're not going to do them in the first phase.

### Planned next steps (actions)[¶](#Planned-next-steps-actions)

-   Policy examples & workflows for cross-device interaction, including
    non-webinos devices. – *Davide, Salvatore*
-   Policy examples & workflows for outsourced policy specification –
    *Davide, Salvatore*
-   Policy examples & workflows for updates to applications and update –
    *Davide, Salvatore*
-   Policy synchronisation – *John*
-   Investigation of Powder/P3P policies for privacy – *Davide,
    Salvatore*
-   Policy GUI specification & guidelines – *John*
-   Workflow for checking application integrity and identity – *John*
-   Standardising error messages as a result of "access denied" events:
    WAC approach probably sufficient. -- Krishna: will add the data
    required
-   Privileged applications – *Krishna* (based on earlier email)

<!-- -->

-   Set of examples of privileged applications, then some of the
    privileges they need access to and possibly even identify examples
    of what the APIs might look like.
-   How we specify which sources of privileged applications are
    trusted - e.g. perhaps only a device manufacturer. This also needs
    to fit into the general scheme of how applications are trusted with
    respect to who signs them.
-   Come up with examples of policies for them. So, for example, what
    kind of policies are required for : \* An application installer \* A
    process viewer \* A policy management application (e.g. viewing
    existing user policies)
-   In addition, working on how different authorities might be involved,
    possibly looking at the WAC specifications for guidance. Some
    platforms have privileged applications provided by the manufacturer
    or operator. Salvatore to provide guidance on the structuring of
    XACML policies. Simon to give some examples of privileged apps.

### Open questions[¶](#Open-questions)

-   How do we package scripts properly? \<script\> tag or another
    "widget"?
-   How do we specify and protect policies on the device, particularly
    those relating to operator/content provider/manufacturer policies?
-   Remote management: further thoughts needed on how to implement

### Link to preliminary deliverable structure for this work area[¶](#Link-to-preliminary-deliverable-structure-for-this-work-area)

[Draft Deliverable Structure](Draft%20Deliverable%20Structure.html)

Device, Application and Service Discovery[¶](#Device-Application-and-Service-Discovery)
---------------------------------------------------------------------------------------

### Progress made (with resources expended)[¶](#Progress-made-with-resources-expended)

Approx spent man months 7.5 PM.

-   State of art analysis for different technologies relevant to (3.0PM)
-   High level diagram defined (0.50 PM)
-   Functional Model & APIs (0.50 PM)
-   Application Discovery (2 PM)
-   Collaborated with Overlay Network on Local discovery demo. (0.75 PM)
-   Working on discovery demos using XMPP, DHT (0.75PM)

### Planned next steps (actions) + anticipated resources[¶](#Planned-next-steps-actions-anticipated-resources)

Major work left is remote discovery part and how to represent service
data.

-   Remote discovery mechanisms, e.g. XMPP, DHT - how it will fit into
    "Personal Zone" architecture (1 PM)
-   Application discovery (1 PM)
-   Service discovery - features and format (1 PM)
-   Naming and Addressing (0.50 PM)
-   Security Aspects (0.50 PM)
-   USB discovery code (0.5PM)

### Decisions that need to be made – and communicated[¶](#Decisions-that-need-to-be-made-–-and-communicated)

-   How event handling works with service advertisement & notification?
    ( to communicate with event handling)
-   How should the device ID be represented to application and how it is
    mapped to user ID (to communicate with IDM)
-   Expose availability and capability on the network based on policy
    (to communicate with Policy management)
-   Find device based on certain criteria: descriptions of device &
    services – properties & Context, e.g. social proximity. (to
    communicate with Context Management)
-   How does the webinos runtime expose capabilities from non-webinos
    devices in it's LAN? A webinos enabled device may proxy services
    provided by non-webinos devices, e.g. devices that are attached
    using shortrange connectivity (eg. a Bluetooth connected GPS
    receiver).
-   Do we really need application IDs?
-   Use of XMPP server for local webinos server and remote webinos
    server ?
-   Is there a need of a server mode for local connections or will
    ad-hoc p2p connection be sufficient?
-   What information (security, policies, etc) is stored locally and
    what is stored on the webinos server and how is this information
    synchronized (see Identity & User Data work area)

Web application packaging, handling and Web Runtime specification[¶](#Web-application-packaging-handling-and-Web-Runtime-specification)
---------------------------------------------------------------------------------------------------------------------------------------

The web application specification ([Webinos\_Core](.html)
[Web\_application\_packaging\_handling\_and\_Web\_Runtime\_specification](.html))
is divided into two main parts. First, the definition of what a webinos
application is (from a technical point of view, packaging, application
interface and distributed application definition) and secondly the
definition of application specific webinos web runtime environment
requirements (e.g, application life cycle and web technologies to be
supported by the runtime).

### Progress made (with resources expended)[¶](#Progress-made-with-resources-expended)

-   The current draft of the webinos application packaging specification
    is based on the W3C widget specification ("zipped ressource files
    and a xml based configuration and meta data file"). (1.1 PM)
    -   A number of new xml elements were added whereas some of them
        were taken from the Task 2.3 requirements and otheres were
        introduced to support webinos specific application features.
    -   The related w3c widget JavaScript application interface
        specification is extended to cover the added elements
    -   extension to the w3c packaging to contain so called child
        applications (application packages within a main application
        package) which can be installed on other devices in order to
        work together are defined (including automatic or programmatic
        deployment of child applications)
-   Definition of how JavaScript functions can be exposed to other
    applications or between child and main application. (1.1 PM)
-   Specifying how (remotely) hosted applications can be executed. (1.1
    PM)
-   Draft specifications of the application life-cycle handling and web
    standards to be supported by webinos web runtimes (0.6 PM)
-   Demo Implementation of child application approach for distributing
    applications (0.5 PM)

### Planned next steps (actions) + anticipated resources[¶](#Planned-next-steps-actions-anticipated-resources)

-   editorial: currently some parts of the specifications are only
    bullet point lists and some of the new elements are only briefly
    described (no examples of use yet) (0.7 PM)
-   based on the meeting outcome the distributed application sections
    must be adapted and completed (1.0 PM)

<!-- -->

-   editing of specification for deliverable based comments of other
    partners (0.5 PM)
-   reviewing and commenting on specifications by other partners (0.8
    PM)

### Decisions that need to be made – and communicated[¶](#Decisions-that-need-to-be-made-–-and-communicated)

### Link to preliminary deliverable structure for this work area[¶](#Link-to-preliminary-deliverable-structure-for-this-work-area)

[Specification](Specification.html)

'Privileged applications'[¶](#Privileged-applications)
------------------------------------------------------

### Progress made (with resources expended)[¶](#Progress-made-with-resources-expended)

• Investigations made in the areas of BONDI, JavaScript and Android.\
• JavaScript privileged API’s identified for Browser Implementation.\
• Security, Permissions, Privileges, Access Controls areas addressed
with respect to Android, BONDI and JavaScript.\
• Use Cases and Requirements identified related to Privileges and Policy
Management.\
• Created Use cases, Requirements for Engine diagnose API (Similar to).\
• Produced sequence diagrams in connection to Policy Management Data.\
• Granting permissions, authorization, authentication, Manifest File
(Android) and Privileges to a specific user/application identified in
Android, BONDI and JavaScript.\
• Conclusion reached to that there are similar issues that needs to be
addressed in Policy Management so merged with Policy Management.

Total resources expended \~4.0PM

### Planned next steps (actions) + anticipated resources[¶](#Planned-next-steps-actions-anticipated-resources)

• It will be a Sub Task now in the Policy Management.\
• Considering Policy management from the perspective of an User,
Operator or Device manufacturer. We need to consider how authorities and
certificate hierarchies will work.\
• Bring in some data from Content Adaption and Content Awareness,
Extension Handling, Cross Domain Platforms with Privileged Apps and
Services.

Some Issues to look into:\
• Where do webinos installers, policy managers and device settings apps
sit in the webinos architecture? Do they need special consideration?\
• How do proprietary applications (E.g. those installed by the device
manufacturer) get installed and how do users know their provenance (e.g.
why they were installed, who trusts them)\
• How are application certificates, developer certificates, and general
root certificates handled?

Total resources estimated \~2.0PM

### Decisions that need to be made – and communicated[¶](#Decisions-that-need-to-be-made-–-and-communicated)

• Privilege apps and services to Look into issues like Trust boundary,
Identity and Integrity checks, Engine and HW management and some
critical info of the Engine\
• Access sensitive API's of vehicle, mobile, setup box\
• How to protect Runtime Enviroment from Hacks?\
• The Applications to be signed and confirmed by the Device Manufacturer
when using Sensitive API's and Critical data\
• To Monitor Engine data, mobile and setup box\
• To use Cryptographic methods, Encryption code for Security purposes

Case 1 is enough to implement things like dashboard, installer,
launcher, and policy manger. However, in our opinion could be useful to
allow both kind of solutions, because case 2 allows direct control over
API access by the API provider. E.g., a car manufacturer can write
engine monitoring APIs and allow to access them only via the car
manufacturer signed applications.

### Link to preliminary deliverable structure for this work area[¶](#Link-to-preliminary-deliverable-structure-for-this-work-area)

</wp3-1/wiki/%27Privilege_Apps_and_Services_Usecases_Requirements_Sequence_Diagram%27>

Specification Doc:
</wp3-1/wiki/31_Deliverable_Specifications_Privileged_Apps>\
more data linked to the Policy Management Group

Analytics / Metrics[¶](#Analytics-Metrics)
------------------------------------------

### Progress made (with resources expended)[¶](#Progress-made-with-resources-expended)

To be added.

### Planned next steps (actions) + anticipated resources[¶](#Planned-next-steps-actions-anticipated-resources)

To be added.

### Decisions that need to be made – and communicated[¶](#Decisions-that-need-to-be-made-–-and-communicated)

To be added.

### Link to preliminary deliverable structure for this work area[¶](#Link-to-preliminary-deliverable-structure-for-this-work-area)

To be added.

Event handling (subscription/storing/forwarding)[¶](#Event-handling-subscriptionstoringforwarding)
--------------------------------------------------------------------------------------------------

### Progress made (with resources expended)[¶](#Progress-made-with-resources-expended)

-   First draft architecture - 0.25 PM
-   XMPP for Event Handling state of the art analysis - 0.15 PM
-   Event ontology (format), taxonomy (types) and basic/generic
    handling - 0.45 PM
-   Event-based RPC - 0.15 PM
-   Publication/subscription mechanism - 0.3 PM
-   Application-level event generation and listening - 0.3 PM
-   Demo/prototype implementation - 0.5 PM
-   Notifications - 0.10 PM
-   Project management/coordination - 0.3 PM
-   General specification review and "normalization" - 0.25 PM

Total: 2.75 PM

### Planned next steps (actions) + anticipated resources[¶](#Planned-next-steps-actions-anticipated-resources)

-   Complete open tasks - 0,50 PM
    -   Demo/prototype implementation - 0.15 PM
    -   Project management/coordination - 0.1 PM
    -   General specification review and "normalization" - 0.25 PM

<!-- -->

-   New tasks - 1 PM
    -   Event caching - 0.25 PM
    -   Device-level event routing - 0.25 PM
    -   Network-level event routing - 0.25 PM (XMPP?)
    -   Check for privacy/security issues - 0.25 PM

Total: 1.50 PM

### Decisions that need to be made – and communicated[¶](#Decisions-that-need-to-be-made-–-and-communicated)

-   Is it ok to require that all webinos apps use UTF-8 encoding?
    (otherwise we have to implement encoding translations and it all
    gets very messy)
-   The [foundations
    spec](/wp3-1/wiki/Spec_-_Foundations#Exposing-Application-Functionalities-as-Service-to-other-Applications)
    seems to suggest that the WRE "registers" the service for an
    application by reading its static manifest - is this the only way to
    create a service? (in event handling we to address entities that may
    be created at runtime, e.g. pub/sub nodes...)
-   Publication/subscription needs some well-defined, transferable and
    easy-to-work-with policy representation...
-   Are we going to use XMPP for network-level event routing? (this has
    several implications in practice)
-   To which extent do we expect/desire/require to have Webinos on the
    "servers"? (i.e., can we avoid/reduce XMPP \<-\> Webinos events
    mapping?)
-   ~~Is page "[Webinos architecture](.html)" where we have to write
    stuff about several WP 3.1 areas by 20/05?~~
-   ~~It's very unlikely to have a complete spec by 31/05. Stuff that I
    expect to be in good shape by then: event format, RPC,
    publication/subscription, application-level event handling,
    device-local messaging, API attempt. Stuff that I don't expect to be
    ready: caching/storing/forwarding, network-level event exchange,
    security/policy considerations, UML diagrams.~~
-   ~~What is a service? (this is especially related to RPC and
    publication/subscription - push vs pull services)~~
-   ~~How is the WRE structured? (browser + server and microkernel-like
    arrangement debates)~~
-   ~~Who defines event handling and event-based APIs (3.1 vs 3.2)?~~
-   ~~What about i18n? (not so obvious in some cases, e.g. remote
    notifications)~~
-   ~~Is URI ok for event types (and/or for generic identifiers)? And
    SHA-256 for event identifiers?~~
-   ~~Is it acceptable to require JavaScript objects with non-standard
    lifetime? (i.e., using something that prevents the garbage collector
    to destroy a given object - this would allow cross-referencing among
    events, simplifying things quite a bit)~~
-   ~~W.r.t. the PendingOp vs id vs void asynch method return value
    debate, it would be nice to support event un-sending and/or response
    ignoring, so that it gets easy to cancel operations everywhere else,
    but it's not easy business and could impact performance...
    opinions?~~
-   ~~I would propose not to use DOM events, but something lighter that
    can optionally be wrapped into the DOM eventing model... anybody
    against that?~~

### Link to preliminary deliverable structure for this work area[¶](#Link-to-preliminary-deliverable-structure-for-this-work-area)

A "normalized"/"formalized" version of the current content of the [Draft
Architecture](/wp3-1/wiki/Event_handling_%28subscriptionstoringforwarding%29#Draft-architecture)
section on the wiki page should be fine.

Browser plug-in / extension handling[¶](#Browser-plug-in-extension-handling)
----------------------------------------------------------------------------

### Progress made (with resources expended)[¶](#Progress-made-with-resources-expended)

-   state-of-the-art browser plug-ins and extensions (2.25 PM)
    -   [Netscape Plug-in API
        (NPAPI)](%20Netscape%20Plug-in%20API%20(NPAPI).html)
    -   [Pepper API (PPAPI)](Pepper%20API%20(PPAPI).html)
    -   [Google Native Client
        (NaCl)](Google%20Native%20Client%20(NaCl).html)
    -   [Chrome Extensions](%20Chrome%20Extensions.html)
    -   [Node.js Addons](.html)
-   initial high level architecture (0.5 PM)
-   proposal on parts to be specified (0.3 PM)
-   [\#320](http://dev.webinos.org/redmine/issues/320 "Proposal for technical solution (New)")
    [Recommendation for technical
    solution](/wp3-1/wiki/Recommendation_for_extensions_in_webinos)

### Planned next steps (actions) + anticipated resources[¶](#Planned-next-steps-actions-anticipated-resources)

-   Finalize state-of-the-art for FireBreath, js-ctypes (0.1 PM)
-   Revisit and fine-tune architecture (0.3 PM)
-   Finalize components to be specified (0.4 PM)
    -   Coordindate with discorvery
    -   Coordinate with application packaging
    -   Coordinate with policy management\
        \*Proposal for technical solution
-   Write specification (1.5 PM)

### Decisions that need to be made – and communicated[¶](#Decisions-that-need-to-be-made-–-and-communicated)

-   ~~Are we targeting 3rd party developers to build extensions/plugin?
    Or are extensions integrated by the device manufacturers/platform
    provider?~~
    -   ~~If we target some kind of 3rd party developers, we need to
        agree on one (or more) technical solutions (NPAPI, Node.js
        addons, Addons to the JS-Engine), how extensions are developed,
        in order to incorporate policy or discovery mechanisms for all
        extensions.~~
    -   ~~If we target device manufactures/platform provider, we leave
        it up to them, how they integrate extensions to the webinos
        runtime and how it interacts with the rest of system. In this
        cases we would only specify how an app developer can make use of
        an extension (Some JavaScript API or some stuff in the
        manifest).~~\
        Consensus: Targeting 3rd party developers as well

<!-- -->

-   ~~Agree on a common understanding what extension will look like. Are
    we talking about plug-ins in the common browser sense? Or do we have
    something comparable to Node.js addons and js-ctypes in mind like
    the
    [Glossary](/wp-0/wiki/Glossary#Extension)
    suggests - adding functionality to the js-runtime?~~
    -   ~~The standard for plug-ins is NPAPI and might be replaced by
        PEPPER some day. The NPAPI/PEPPER will then have its own window
        inside the webapplication, where it can draw things in it. The
        plugin would be able to expose it's own API.\
        This would mean the extension developer would have to follow the
        rules which are exposed on him by the NPruntime. The
        specification would be more or less a refer to the NPAPI
        documentation.~~
    -   ~~Analyzing [the requiremenets relevant for the extension
        handling](/wp3-1/wiki/Browser_plug-in__extension_handling#Relevant-requirements-for-plug-in-and-extension-handling)
        suggests to follow a Node.js/js-ctypes approach~~
-   Agree on one Recommendation:
    </wp3-1/wiki/Recommendation_for_extensions_in_webinos#Recommendation>

### Link to preliminary deliverable structure for this work area[¶](#Link-to-preliminary-deliverable-structure-for-this-work-area)

[specification plug-in/extension handling](.html)

Overlay networking model[¶](#Overlay-networking-model)
------------------------------------------------------

### Progress made (with resources expended)[¶](#Progress-made-with-resources-expended)

As a rough estimate, something like 3 PM in total so far. Don't have
data at finer granularity.

-   Study of local discovery mechanisms
    -   multicast DNS
    -   SSDP for UPnP
    -   SLP
    -   USB
    -   Bluetooth
-   Implementation of discovery mechanisms as a scriptable NPAPI plugin
-   Initial investigation of dynamically loadable service adapter
    modules
    -   As binary library files plus JavaScript modules
-   Exploration of API choices
    -   Object defined in JavaScript library (supplied by 3rd party)
    -   Simple call backs (limited to one handler)
    -   DOM object with DOM events (bubbling/capture, multiple
        listeners)
-   Authentication for accessing services
    -   Datagram followed by HTTP as a common pattern
    -   Requesting multiple permissions at same time for usability
    -   Enabling users to review/revoke recorded decisions
    -   Trust delegation model
-   Multicast messages for local area communication
    -   easy to implement and avoids need for server
    -   use cases include games, chat
-   Personal Zones as basis for wide area discovery, messaging
    -   Authenticating device as part of zone
    -   Synchronization across zone
    -   Support for NAT traversal
    -   Social proximity (traversing distributed social graph)
    -   Permissions and authentication for access to context/services,
        e.g. access to your friend's devices
    -   Dealing with shared devices and "family zones"
    -   Distributed search (DHTs) and ranking by social relevance
    -   Lookup based on email address: DNS-SD, Web Finger
    -   Privacy friendly search - user profiles and trusted search
        agents
-   Exploration of mechanisms for traversing NAT
    -   social agent rather than just NAT traversal
    -   UDP keep alives in place of TCP for reduced server load
    -   SMS for waking up dormant connections over cellular networks
    -   Tunnel events over shared connection

### Planned next steps (actions) + anticipated resources[¶](#Planned-next-steps-actions-anticipated-resources)

-   Further work on Discovery mechanisms
    -   Zigbee
    -   Firewire
    -   Implementation of wide area discovery mechanisms
    -   Taxonomy of services for easier authoring
    -   Visibility of brokers (Web Introducer)
-   Further work on service adapters
    -   media streaming use case for Bluetooth
    -   robot control use case (control + streaming + NAT traversal)
    -   USB example (to be selected)
-   Further work on authentication
    -   role of biometrics for user authentication
    -   mutual authentication
    -   zero knowledge proofs
    -   white and black lists
-   Personal Zones
    -   Initial implementation (including NAT traversal)
-   Device coordination
    -   strong, weak and none (see definitions)

### Decisions that need to be made – and communicated[¶](#Decisions-that-need-to-be-made-–-and-communicated)

-   Avoid decisions ahead of implementation experience
-   Running code makes communication of ideas much easier

### Link to preliminary deliverable structure for this work area[¶](#Link-to-preliminary-deliverable-structure-for-this-work-area)

Document methodology, vision, exploratory studies, implementation
experience, choices available, next steps, and links to specifications.

Context Awareness and Adaptation[¶](#Context-Awareness-and-Adaptation)
----------------------------------------------------------------------

### Progress made (with resources expended)[¶](#Progress-made-with-resources-expended)

Based on the data reported roughly 6pm have been spent on this area -
yet almost roughly 2pm correspond to the participation to the project
meeting in Torino.

Progress made

-   Merging the Context Management and Context-Driven Adaptation areas
    and scoping objective (0,5 pm) - **DONE end of March**
-   Mapping aspects of the new area to underlying context related
    requirements (0,5 pm) - **DONE end of March**
-   State of the art Analysis (2,5 pm) - **DONE mid April**
    -   Analysis of relevant EU research projects on aspects of context
        awareness (more than 20 projects have been reviewed on webTV,
        mobiles, e-Accessibility, context models, etc)
    -   Review of standards and technologies for structuring context
        data (IDEAL 2, Activity Streams, RDF/RDFs, microFormats)
    -   Review of available technological solutions in support of
        context awareness aspects (Android Fragments API, Volantis
        Mobile Content Framework, etc)
-   Identifying Items to be delivered by end of June and assign to
    Partners (0,25 pm)- **DONE May 5th**
-   Creating a whitepaper on webinos Context Model (0,25 pm) - **DONE
    May 9th** [available at "The WEBINOS Federated Context Model for
    Describing Social Activity Across Connected
    Devices"](available%20at%20"The%20WEBINOS%20Federated%20Context%20Model%20for%20Describing%20Social%20Activity%20Across%20Connected%20Devices".html)

### Planned next steps (actions) + anticipated resources[¶](#Planned-next-steps-actions-anticipated-resources)

The items that are envisaged to be delivered within the next 2 months
are:

-   Webinos Context Model (context objects, their attributes and
    relationships in the context model) - **LAUNCHED May 5th**
    [available at "Objects and Relationships in the Webinos Context
    Model"](available%20at%20"Objects%20and%20Relationships%20in%20the%20Webinos%20Context%20Model".html)
-   Form and representation of the Context Model (i.e. RDFa)
-   Storage facility of Context Data (in coordination to the work done
    in other Areas)
-   An additionall architecture to context for collecting Analytics Data
-   Access layer to context data along with a set of permissions
    regulating access to different pieces of context data by different
    entities.

### Decisions that need to be made – and communicated[¶](#Decisions-that-need-to-be-made-–-and-communicated)

Coordinate with the work done in other areas to avoid redundancies and
mis-alignment. In particular

-   User ID and Data Management for creating the user profile and
    acquiring context data (what protocols we actually adopt i.e.
    Portable Contacts, XRD, open social, FOAF).
-   What is the context acquisition mechanism, we need to ensure
    transparency among the many endpoints webinos has (one user, many
    devices, apps across devices) - we should re-use existing open
    approaches such as the open graph protocol
-   Privacy for allowing access to context data in alignment with the
    webinos privacy framework
-   Device Application and Service Discovery for supporting context
    reasoning functions (adaptations and social proximity)\
    .

### Link to preliminary deliverable structure for this work area[¶](#Link-to-preliminary-deliverable-structure-for-this-work-area)

tbd

