Policy Management Meeting 15th March 2011[¶](#Policy-Management-Meeting-15th-March-2011)
========================================================================================

Attendees:[¶](#Attendees)
-------------------------

-   Salvatore
-   Andrea
-   John

Topics of discussion:[¶](#Topics-of-discussion)
-----------------------------------------------

-   Salvatore's policy architecture. We went through and discussed the
    [proposed
    architecture](http://dev.webinos.org/redmine/attachments/download/428/policy_management__architecture.odp)
    . Comments:
    -   PAP and PDP split into two sections: one local and one remote.
        The local PAP will cache policies and have policies referring to
        local resources. The remote PAP and PDP will be synchronised by
        the Webinos Agent.
    -   Addressing other devices will be done through the overlay
        network - need to get more feedback on this. Special
        requirements for policy messages? E.g. accountability and
        identity requirements?
    -   Negotiation of credentials is an open question. Suggestion to
        look at:
        [PERMIS](http://sec.cs.kent.ac.uk/download/ModularPermisConcPracExpRevised.pdf)
        , [PrimeLife extensions to
        XACML](http://spdp.dti.unimi.it/papers/wisg09-ADPPS.pdf) and
        [Access Negotiation within
        XACML](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.118.7718&rep=rep1&type=pdf)
    -   Need to define which policies are synchronised.
    -   Revocation will need some more thought - how to revoke a policy
        on an infrequently online device?
    -   Will be turned into PlantUML at some stage

<!-- -->

-   Effort allocation
    -   John busy for the rest of this week, but to add PM allocations
        to the wiki.
    -   Public holiday in Italy later this week
    -   Not sure about effort from Stefano

<!-- -->

-   Agenda for WP3 meeting (to be sent by John)
    -   Time/effort allocation
    -   Current progress and activities
    -   Need for feedback on current architecture
    -   Planned activities: John to look at synchronisation, Salvatore
        to look at policy use cases / tasks.

Actions[¶](#Actions)
--------------------

-   John to look into policy synchronisation
-   John to add expected effort allocation to the wiki
-   John to email Nick with details for the conference call.
-   Salvatore to look at a concrete example of using the proposed policy
    in a use case.
-   Salvatore (?) to get feedback from others on proposed architecture?
    (TBC)

