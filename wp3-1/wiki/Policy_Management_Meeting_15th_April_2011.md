Policy Management Meeting 15th April 2011[¶](#Policy-Management-Meeting-15th-April-2011)
========================================================================================

Attendees[¶](#Attendees)
------------------------

-   Salvatore
-   Davide
-   Andrea
-   Dieter
-   John

Decisions[¶](#Decisions)
------------------------

-   The subject of XACML back-end policies will be the application
    unique identifier, which is synonymous with the application itself.
    Option '0' from the options page.
-   P3P Policies to be referenced from application feature request
    statements in the config xml file
-   Policy protection may require attestation, so we need to make sure
    this gets into 3.2 APIs

Actions[¶](#Actions)
--------------------

-   John to contact IDM and discuss:
    -   How identity should be expressed in policies - e.g. what level
        of authentication might be expressed, what identities will
        actually look like
    -   How applications will express identity requirements
    -   How identity should be negotiated for privacy
-   Salvatore to investigate XACML request structure
-   Salvatore to provide example XACML policies
-   John to investigate XACML delegation
-   John to investigate how remote script access control will be defined
-   Dieter to look into javascript APIs as part of context management to
    work out how policies will be handled in Javascript
-   Dieter to provide examples of wireframes for policy GUIs.
-   Andrea to... investigate attestation API?

Context considerations[¶](#Context-considerations)
--------------------------------------------------

-   Hierarchy of context discussed: you may need access to some context
    data in order to gain access to other context data. How should this
    be expressed and managed?
-   Frequency of access: how do you define how often a piece of
    information will be accessed, and what do policies look like here?
    -   Suggestion by Davide that context management component should
        push updates to client applications.
    -   Comment by John: simplest alternative would be the best one,
        users unlikely to know upfront about how often they want their
        location checked, so either "constant" or "on command",
        possibly?

Security considerations[¶](#Security-considerations)
----------------------------------------------------

-   Protection of policies on the device
-   Avoid the device being cracked and betraying handset manufacturer or
    operator policies
-   Synchronise policy updates wherever possible - what about devices
    which are rarely used?

Next meeting[¶](#Next-meeting)
------------------------------

Wednesday at 2pm BST / 3pm CEST.\
Skype again unless someone else participates who can't use it.

