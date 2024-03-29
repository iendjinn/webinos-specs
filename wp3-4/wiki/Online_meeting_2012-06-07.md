Online meeting 2012-06-07[¶](#Online-meeting-2012-06-07)
========================================================

Attendees[¶](#Attendees)
------------------------

Paolo Vergori (ISMB) <vergori@ismb.it>

Christian Fuhrhop fraunhofer.de

Martin Lasak fraunhofer.de

Habib Virji <habib.virji@samsung.com>

Claes Nilsson <claes1.nilsson@sonymobile.com>

ziran sun <ziran.sun@samsung.com>

Christos Ntanos <cntanos@epu.ntua.gr>

widlproc executable for Windows.[¶](#widlproc-executable-for-Windows)
---------------------------------------------------------------------

No update from Paddy. The new version of Visual Studio causes problem
for upgrading the widplproc executable. So currently windows users
cant't "test generate" html specifications on their local machine. For
those users modified widls have to be committed/pushed to the Redmine
API repository without previous local validation. This is not convenient
and might mean several commits/pushes. For each push error messages have
to be read, widl be corrected and a new commit/push has to be done. This
is not ideal but we need to start updating our API specifications so
windows users have to live with this until the widlproc is fixed.

Wrappers for referred APIs[¶](#Wrappers-for-referred-APIs)
----------------------------------------------------------

Development tool chain needs widl wrappers and we need to create full
widl wrappers for the referred APIs for which we don’t have that
already. Dom to provide tool and do the extraction work according to
<http://dev.webinos.org/redmine/issues/900>. All wrappers to use the
latest version of original specification.

Better background information and traceability for new webinos APIs[¶](#Better-background-information-and-traceability-for-new-webinos-APIs)
--------------------------------------------------------------------------------------------------------------------------------------------

</t3-4/wiki/New_proposed_Webinos_APIs>

We need to provide better background information and traceability for
new webinos APIs. This was a comment from the latest EU review. A
process for providing Scenarios and Use Cases as background information
to new APIs is proposed. See mail
<https://listen.fokus.fraunhofer.de/sympa/arc/webinos-wp3-ml/2012-06/msg00021.html>.
Paolo stated that this process does not suit all APIs, e.g. the oAuth
API, and Christian meant that the need for some APIs are obvious. Claes
stated that most important is that we provide some traceable background
information/motivation for new APIs that we specify and implement and
suggests that this process is followed when appropriate. Other means to
provide background information is also ok if this suits better.

webinos core management api - Habib[¶](#webinos-core-management-api-Habib)
--------------------------------------------------------------------------

Habib requests an API for things like:

-   Path towards webinos storage
-   Webinos PZP id
-   Webinos PZH id
-   Webinos connected PZP's online and offline status
-   Webinos connected PZH's online and offline status
-   Error status - (communication failure, connecting to pzh failure,
    authentication failure)
-   Retrieving Application ID.
-   Webinos logging mechanism
-   Webinos service capability broadcast
-   PZH & PZP configuration parameters
-   Remote management provisioning
-   Personal device management
-   QoS based discovery

Some of this is implemented in task 4.1 but it is not well specified and
could be considered as a Q&D solution. So we need to work on this a
provide a well specified API.

[Action Habib to provide background, requirements etc for a Webinos core
management API](http://dev.webinos.org/redmine/issues/903)

API specification alignment with task 4.1 API implementations and prestudy on further work[¶](#API-specification-alignment-with-task-41-API-implementations-and-prestudy-on-further-work)
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

</t3-4/wiki/API_specification_alignment_with_task_41_API_implementations>

-   Context API: Christos has updated the wiki with implementation notes
    and suggestions for improvements for this API. [Action Christos to
    initiate an e-mail review of improvements proposed and if no
    objections update specification
    accordingly.](http://dev.webinos.org/redmine/issues/880)

<!-- -->

-   Events API: Andre proposes simplifications to the API. Does not seem
    controversial. [Action Andre to update specification according to
    simplifications proposed](http://dev.webinos.org/redmine/issues/881)

<!-- -->

-   Messaging API: Webinos Messaging API is based on WAC Messaging API.
    WAC has now added 'isInSync' attribute and 'sync()' method to
    MsgAttachment interface. We should add this our API as well. If no
    objections on mailing list [Action Christian to add 'isInSync'
    attribute and 'sync()'
    method](http://dev.webinos.org/redmine/issues/904)

<!-- -->

-   NFC API: There is a lot of activity on NFC in W3C, B2G, Tizen etc.
    Action Claes to ask Hans, Stefano and Dave on their view on webinos
    NFC API taking activities around NFC in W3C, B2G, etc into
    consideration.

<!-- -->

-   Payment API: The Payment API is currently limited. It works for
    SIM/Mobile subscription payment methods but not for general credit
    card payment. However, for now Christian proposes to leave this API
    as is.

<!-- -->

-   Sensors API: [Action Claes to update API according to proposal at
    wiki](http://dev.webinos.org/redmine/issues/885). In addition Ziran
    has [Action to add proposed additional sensor types to Sensor
    API](/t3-4/wiki/New_proposed_Webinos_APIs#Sensor-API-proposed-additional-sensor-types).
    This is based on MWC pulse meter demo.

<!-- -->

-   Service Discovery API: Alexander has updated wiki and proposes to
    remove createService. [Action Anders to discuss createService and
    long-lived relations with
    Service](http://dev.webinos.org/redmine/issues/905).

<!-- -->

-   Service Disovery versus Device Discovery API: Ziran has provided
    input on implementation of discovery in task 4.1. See
    <https://listen.fokus.fraunhofer.de/sympa/arc/webinos-wp3-ml/2012-05/msg00074.html>.
    [Action Ziran to investigate need for Device Discovery
    API](http://dev.webinos.org/redmine/issues/906)

<!-- -->

-   TV API: [Action Martin to update TV
    API](http://dev.webinos.org/redmine/issues/907)

<!-- -->

-   Vehicle API: [Action Simon to update Vehicle
    API](http://dev.webinos.org/redmine/issues/908)

AOB[¶](#AOB)
------------

No task 3.4 meeting next week. Claes on vacation 13-15 June.

Next task 3.4 meeting in Ghent June 20

