Policy Management and Identity Current State[¶](#Policy-Management-and-Identity-Current-State)
==============================================================================================

Current decisions made:[¶](#Current-decisions-made)
---------------------------------------------------

-   Widget access control requirements expressed in config xml
-   Additional access request/ handling errors will be done using
    Javascript APIs. *TODO*
-   When an app is running, if a specific API is used (e.g. "camera.xyz"
    or an XHR), this also triggers the PEP to check whether any
    additional policies apply or obligations are required (e.g. user
    prompts or otherwise)
-   Access to remote scripts or APIs is dependent on them being
    "packaged" correctly.
-   P3P Policies to be referenced from application feature request
    statements in the config xml file

### In the background, policies are enforced:[¶](#In-the-background-policies-are-enforced)

-   A distributed XACML style system with caching of policies on each
    device, as per UNICTs architecture
-   The subject of XACML back-end policies will be the application
    unique identifier, which is synonymous with the application itself.
    Option '0' from the options page.
-   New or updated policy assertions will be communicated through a
    synchronised policy repository
-   Any policy updates received should only be interpreted from
    whitelisted devices or if signed by trusted users.

### On the device:[¶](#On-the-device)

-   Users have an interface to view policy settings. We will produce
    some very simple example GUIs
-   Users have some simple methods of applying straightforward policies
    (e.g. "turn off location data")
-   APIs and data can be tagged so that it fits into categories that
    specific policies apply to. E.g. "Work data" or
    "location-information". This implies a local (and perhaps
    synchronised) database of webinos objects in the runtime stating at
    least the IRI and applicable tags.

### Identification:[¶](#Identification)

-   All "objects" have an IRI. This includes data, applications,
    application functionality, extensions, everything.
-   A webinos user identity is defined in the polito architecture
    document. These are linked to other identities elsewhere (possibly
    partial identities and assertions?). More work needed here in how to
    manage users locally and what a app developer will see.
-   Devices need to belong to particular defined "groups" (or "local
    clouds" or "zones"). Each user will probably have a "owned devices"
    group but also may belong to others such as "known devices" or
    "friends devices" or similar.

Open issues:[¶](#Open-issues)
-----------------------------

-   Same-origin security model. How are we allowing XHR requests from
    apps to other domains? There may be some CORS solutions...
-   What will the javascript APIs for access control information look
    like to developers? Beyond just a try/catch error handling - how are
    current policy settings queried? E.g. policy.canAccess("...")? Maybe
    very similar to the DeviceStatusManager in WAC?
-   Can we include delegation in the policy framework?
-   Can we issue short-lived credentials for sharing device features
    between devices? OAUTH? We need to go through this with the IDM
    group.
-   How do we package scripts properly? \<script\> tag or another
    "widget"?
-   How do we specify and protect policies on the device, particularly
    those relating to operator/content provider/manufacturer policies?

Plan[¶](#Plan)
--------------

...

