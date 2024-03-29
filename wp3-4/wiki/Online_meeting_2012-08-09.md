Online meeting 2012-08-09[¶](#Online-meeting-2012-08-09)
========================================================

Attendees[¶](#Attendees)
------------------------

    christian.fuhrhop, Andre Paul, Alexander Futasz, Martin Lasak / Frauhofer

    Simon Isenberg    simon.isenberg@bmw.de

    Stefano Vercelli    stefano.vercelli@telecomitalia.it

    Habib Virji    habib.virji@samsung.com

    Claes Nilsson    claes1.nilsson@sonymobile.com

    ziran sun    ziran.sun@samsung.com

    Eelco Cramer    eelco.cramer@tno.nl

    Krishna    krishna.bangalore@in.tum.de

Personal Zone API[¶](#Personal-Zone-API)
----------------------------------------

-   Some attributes enabling UI adaption overlap with Device Status API.
    As we shouldn't have redundant APIs there is an **Action on Habib to
    remove those attributes from the Perzonal Zone API and submit input
    to Christian so that he can add those attributes to the Webinos
    Device Status API.**

<!-- -->

-   More motivations for the Perzonal Zone API was requested and there
    is an **Action on Habib to add more motivation to the Perzonal Zone
    APi in
    </t3-4/wiki/Core_Management_API_and_Use_Cases>**

<!-- -->

-   Alexander raised that there is a security issue with exposing PZP id
    and name to developers. **Action Habib to contact John on this
    issue**

Created <http://dev.webinos.org/redmine/issues/929> to track these
actions.

Device Status API[¶](#Device-Status-API)
----------------------------------------

-   There is an **Action on Christian to add the Webinos specific
    Aspects from the [Phase 1 device status
    vocabulary](http://dev.webinos.org/specifications/draft/vocabulary.html)
    into the phase 2 device status API as well as other new Aspects that
    we discover a need for**.

<!-- -->

-   **Action Christian to remove the link to the WAC devicestatus module
    on <http://dev.webinos.org/specifications/new/> as we now have our
    own device status API.**

Created <http://dev.webinos.org/redmine/issues/930> to track these
actions.

Duplicated abstract and introduction sections in Webinos API specifications[¶](#Duplicated-abstract-and-introduction-sections-in-Webinos-API-specifications)
------------------------------------------------------------------------------------------------------------------------------------------------------------

-   This seems to be an effect of the updated specification toolchain
    due to the new W3C widl specification. **Action Claes to e-mail Dom
    on this issue**.

Error callbacks[¶](#Error-callbacks)
------------------------------------

-   Each specification must have a unique name for it's error callback
    and should as much as possible, re-use DOMError objects in error
    callbacks instead of minting new errors for each API. For example
    see <http://dev.webinos.org/specifications/new/tv.html#::TVErrorCB>
    in the TV Control API.\
    **Action for all editors to, if not already done, update error
    callbacks accordingly**

Synchronous methods[¶](#Synchronous-methods)
--------------------------------------------

-   It is not possible to implement synchronous API methods with the
    current implementation with Web Socket communication between WRT and
    PZP. **Action Andre to contact Nick on plans for synchronous
    communication between WRT and PZP**

Messaging API[¶](#Messaging-API)
--------------------------------

Decided to remove the "synchronisable interface" as we see no use cases
for it.

Sensor API[¶](#Sensor-API)
--------------------------

Claes has a list up updates to be done and when done there is an
**Action on Stefano V to add support for M2M sensors**,
<http://dev.webinos.org/redmine/issues/931>.

Object Synchronization API[¶](#Object-Synchronization-API)
----------------------------------------------------------

Martin has added this API to enable and manage application
synchronization. **Action for Martin to provide background information**

