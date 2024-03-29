[Back to User Identity and User Data
Management](Back%20to%20User%20Identity%20and%20User%20Data%20Management.html)

20110428 conf call on User Identity Management[¶](#20110428-conf-call-on-User-Identity-Management)
==================================================================================================

Date: 28 Apr 2011\
Time: 09:30 - 10:30 CEDT\
Bridge: PowWowNow, *Enhanced Access*, PIN: 312806, [Dial-in
numbers](http://pdf.powwownow.com/pdf/GBR_en_pwn-dial-in-numbers.pdf)

Agenda:

-   Discussion of authentication architecture details in the light of
    the personal zone proxy which was discussed in the [previous conf
    call](previous%20conf%20call.html)

Action Items:

-   Polito, DOCOMO: update sequence diagrams and, if needed, create new
    use cases
-   Sven: update activity diagrams
-   all: establish group meeting of User Identity and Data Management,
    ideally with Discovery, during Berlin meeting

Decisions (for details see the discussion below):

-   we have both PZP (for communiction of user's own devices and among
    friends) and IDP on the Internet for publicly accessible services
-   additional indirection in addressing is solved by WebFinger

Attendees:

-   Christian Schaefer
-   Sven
-   Andrea
-   Katrin
-   Steffen
-   Habib

Discussion:

-   user registration
    -   no central component which manages identities --\> simplifies
        registration
    -   But how do personal zones trust another? How to access zones of
        my friends?
-   addressing
    -   start from identities I know (Facebook, email addresses, ...)
    -   I could connect to anyone but I had to send a request (e.g.
        Linked-in) and if accepted by the recipient we are connected
        -   always approval from both sides
        -   it is weak as anyone could create a Facebook account for me
        -   what would a new user be allowed to access on my device when
            connected for the first time? Policy required!
-   SSO
    -   no way to establish trust relation between personal zone and an
        online shop
    -   friend relationships on social networks (SN) can be used to
        establish some level of trust
    -   different services are differently sensitive. If strong trust is
        required the NS-based approach is too weak
    -   provide both personal zone and centralised IDP
        -   which one is preferred is based on policy
        -   ordinary user does not understand that and does not want to
            bother with writing policies --\> risk!
-   Location of the personal zone proxy (PZP)
    -   one of the devices hosts the PZP --\> device must be always on?
    -   device start-up: first look for proxy, if there is no proxy
        start-up your own one --\> PZP roams
    -   security problem: all devices should know all shared secrets and
        credentials rather than only one, i.e. sensitive data is stored
        everywhere
    -   but allows free forming of individual local networks; there can
        be more than one PZP active at the same time if there is more
        than one disjoint (local) networks of the same user
-   Authentication Architecture (AA)
    -   having IDP locally is not useful as tokens are to be used across
        personal zones --\> implies central authority
    -   MNO or SN are candidates to host IDP
    -   separation makes sense:
        -   PZP for accessing own devices, devices of friends and
            dynamic local network forming
        -   IDP on the Internet when accessing publicly accessible
            services on the Internet (e.g. a shop)
    -   adds complexity and implementation effort but our previous
        architecture was not that far from what we have now
        -   e.g. the local data cache was there before and now we extend
            it by the proxy which is a local Web server which has access
            to these data
-   addressing
    -   there is an additional indirection: for a user's identifier
        (e.g. email addr), the PZP address needs to be found.
        Thereafter, the PZP is contacted to determine the user's device
        which is to be contacted for the given communication purpose
        -   protocols such as SIP and XMPP cannot be used in this
            setting
    -   WebFinger: uses email addresses to derive additional info, e.g.
        the address of the personal zone
        -   Google has an implementation where address data and other
            info of a user can be accessed if permission is given
    -   advantage: no additional identifier to be memorised by the user
    -   webinos needs to operate a WebFinger server where users can
        register their email addresses and PZP addresses
-   Decisions of today
    -   we have both PZP and IDP
    -   additional indirection in addressing is solved by WebFinger
-   Next steps
    -   sequence diagrams to be updated based on the existing use cases
    -   different people should develop use cases and diagrams to see if
        understanding of the matter is the same
    -   update of activity diagrams
    -   API: it makes sense to see how far other APIs already defined
        for webinos are relevant for us. Device interaction, user
        profile, messaging are potential candidates relevant for user
        identity and data management.
    -   API: as a first idea of APIs for authentication we can/should
        use the Facebook authentication API
        -   we cannot come up with any API definition until basic
            decisions on the architecture are made
    -   We'll try to have a session on IDM on Wed in the Berlin meeting
    -   goal for the Berlin meeting: decide on the fundamental design of
        identification, addressing, authentication and discovery in
        order to be able to focus our work and to flesh out the details
        afterwards

Next meeting: conf call on Mon 2 May 2011, 11:00 - 12:00 CEDT

