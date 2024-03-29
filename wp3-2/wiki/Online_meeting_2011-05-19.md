Online meeting 2011-05-19[¶](#Online-meeting-2011-05-19)
========================================================

Attendees[¶](#Attendees)
------------------------

Hans <hans@ambiesense.com>\
Marco, Stefano (ISMB) <gavelli@ismb.it>\
Habib Virji <habib.virji@samsung.com>\
John Lyle <john.lyle@comlab.ox.ac.uk>\
Simon Isenberg <simon.isenberg@bmw.de>\
Ronny Graefe <ronny.graefe@t-systems.com>\
Claes Nilsson <claes1.nilsson@sonyericsson.com>\
George Voulgaris <george@visionmobile.com>\
Michael Vakulenko <michael@visionmobile.com>\
Daniel Coloma <dcoloma@tid.es>\
ziran sun <ziran.sun@samsung.com>\
Christian Fuhrhop <gotofame@fokus.fraunhofer.de>\
Andre Paul\
Dominique Hazael-Massieux <dom@w3.org>

June 30 delivery[¶](#June-30-delivery)
--------------------------------------

Wiki page prepared: [WP3.2
deliverable](http://79.125.104.127/redmine/projects/t3-2/wiki/WP_32_Deliverable)

Please review and check your responsibilities.

-   Assure that API investigation information you are responsible for is
    accurate for the report: [API investigations per API
    category](http://79.125.104.127/redmine/projects/t3-2/wiki/Wiki#API-Categories)
-   API specifications of your responsibility should be created and
    pushed to the Git repository: [Webinos API specifications Git
    repository](http://dev.webinos.org/specifications/draft/)
-   Provide input to other sections of your responsibility.

Deadline May 30 as we need to review prior to Sophia Antipolis meeting.
Also note that June 2 is a public holiday in Sweden and that June 2 and
3 are free days at SEMC. (This also applies to June 6, the Swedish
national day, which we poor Webinos guys can’t make use of due to the
Sophia Antipolis meeting :-) )

Daniel offered to be editor (with input/help from Alexander, Dieter and
Nick) on the sectio [Tools for API
specifications](http://79.125.104.127/redmine/projects/t3-2/wiki/Tools_for_APIs_specifications)

API patterns and guidelines[¶](#API-patterns-and-guidelines)
------------------------------------------------------------

[API guidelines](http://79.125.104.127/redmine/issues/194) – Daniel

[Webinoscore
API](http://dev.webinos.org/specifications/draft/webinoscore.html) –
Claes.

Comments by e-mail from Dom and Dave.

The conclusions were:

-   Section 3: “Function only” or “Interface” callbacks in asynchronuos
    APIs.\
    “Function only” is the standard method here which we should use.
    However, “Interface callbacks” provide for greater extensibility and
    could be used if we can’t solve the problem with “Function only”
    callbacks.

<!-- -->

-   Section 3.2: Decide on “Asynchronous Methods Return Values”, i.e.
    “void” or “pending operation”. Both types of return values are
    allowed. This depends on the needs of the API specified. Also note
    that we are not making a global definition of "pending operation” as
    the semantics of the "cancel()" method depends on the actual API and
    can not be globally defined.

<!-- -->

-   Section 4: Decide on error handling options. There should be no
    common/global definition of error codes. Each specification should
    specify the error codes that are needed. (However, I don't think we
    have an agreement on "exception error codes" vs "callback error
    codes", i.e. whether they are common or not within a specification.
    My personal view is that they are diffeernt things and in the sensor
    API I have specified SensorException and SensorCBError as different
    interfaces)

Regarding [Webinoscore
API](http://dev.webinos.org/specifications/draft/webinoscore.html) the
conclusions mean that this specification remains very thin and just
defines that the webinos interface is part of the window global object.

Payment API[¶](#Payment-API)
----------------------------

[Payment API](http://dev.webinos.org/specifications/draft/payment.html)
– Christian.

Referring to e-mail discussion initiated by Dom.

This API was questioned by Dom as local resources (e.g. on-device
hardware or services) are not accessed and the API could be implemeneted
as a pure JS wrapper around the GSMA OneAPI RESTful payment API. Such a
wrapper is best provided by JS library developers. Dom also statedt that
we should have an impementation of this library prior to publishing as a
specification.

Christian meant that there are political reasons for including the API
in the deliverable, to show how Webinos can be used in a commercial
environment.

The conclusion was that the Payment API will be included in the 3.2
delivery and that Christian should state, e.g. in the specifcation
header, that this is a proposal/first attempt that not yet has been
implemented.

Event handling APIs – Stefano D’Angelo[¶](#Event-handling-APIs-–-Stefano-D’Angelo)
----------------------------------------------------------------------------------

Event is basically a message that is sent to a local or remote entity.
The event handling API should be agnostic to whether the entity to
communicate with is local or remote. This is related to service
discovery and could be seen as an extension to the service discovery
API.

An example use case for event handling is the advertisment that a new
Webinos service is available.

A low level eventing API inspired by the DOM event model is proposed by
Stefano. See wiki page: [Informal low level event handling API
attempt](http://79.125.104.127/redmine/projects/t3-2/wiki/Informal_low_level_event_handling_API_attempt).
It is proposed that the API should support the following methods:

-   Send event
-   Forward event
-   Add event listener
-   Remove event listener

The conclusion was that Stefano should coordinate with Anders Isberg and
Ziran Sun as this relates to discovery. The goal should be creation of a
tangible Event handling API specification to be included in the WP 3.2
delivery.

Application Execution APIs – Michael Vakulenko.[¶](#Application-Execution-APIs-–-Michael-Vakulenko)
---------------------------------------------------------------------------------------------------

See slide 7 in [Application Execution APIs
investigation](http://dev.webinos.org/redmine/attachments/download/542/Webinos_T3.2_Execution_API_-_v0.01.ppt)
for proposed APIs for phase 1.

Three APIs proposed:

-   Launch installed Webinos application API
-   Check policies on launching Webinos applications (to be coordinated
    with John L)
-   Check if webinos application is installed in device

Michael plans to provide draft API specifications prior to June meeting.

Discovery API[¶](#Discovery-API)
--------------------------------

Anders Isberg’s proposal [ServiceDiscovery
API](http://dev.webinos.org/specifications/draft/servicediscovery.html)

Not dealt with as Anders on vacation.

Context adaptation APIs – George Gionis[¶](#Context-adaptation-APIs-–-George-Gionis)
------------------------------------------------------------------------------------

George not on call but Ronny is working on a User profile API. First
draft planned to be published tomorrow.

AOB[¶](#AOB)
------------

WP 3.2 slot at June meeting. Proposed is:

Tuesday 15:00-17:00 Task 3.2\
Wednesday 09:30-12:30 Task 3.2

Claes suggested a short common status report and the rest of time work
in small groups for API review and discusions.

