Online meeting 2012-05-10[¶](#Online-meeting-2012-05-10)
========================================================

Attendees[¶](#Attendees)
------------------------

Christian Fuhrhop <gotowebinos@fokus.fraunhofer.de>

Claes Nilsson <claes1.nilsson@sonymobile.com>

Stefano Vercelli <stefano.vercelli@telecomitalia.it>

Paolo Vergori (ISMB) <vergori@ismb.it>

Marco Gavelli <gavelli@ismb.it>

Karishma Vinayak - Antenna <gotowebinos@fokus.fraunhofer.de>

Christos Ntanos <cntanos@epu.ntua.gr>

Krzysztof Wajtknecht <kwajtknecht@antennasoftware.com>

Simon Isenberg <simon.isenberg@bmw.de>

Ziran Sun <ziran.sun@samsung.com>

Which "frozen" revisions of Webinos APIs do we need?[¶](#Which-frozen-revisions-of-Webinos-APIs-do-we-need)
-----------------------------------------------------------------------------------------------------------

See mail
<https://listen.fokus.fraunhofer.de/sympa/arc/webinos-wp3-ml/2012-05/msg00064.html>.

When the specifications has been aligned with what we really implemented
in task 4.1 we will continue the work to improve specifications, align
with progress in W3C and elsewhere etc. The question is if we should
create a revision of the API specification repository after all APIs
have been aligned with what we really implemented in task 4.1. The
reason for this would be to have a version available to developers that
really reflects the 4.1 implementation as the APIs from task 3.2 may not
be 100% correct compared to the implementation.

The conclusion was that we should decide that when we see the result of
changes needed on specifications to be aligned with task 4.1
implementation at
</t3-4/wiki/API_specification_alignment_with_task_41_API_implementations>.

Update all task 3.2 APIs according to latest W3C widl-specification.[¶](#Update-all-task-32-APIs-according-to-latest-W3C-widl-specification)
--------------------------------------------------------------------------------------------------------------------------------------------

-   Dom has migrated 8 APIs,
    <http://dev.webinos.org/specifications/new/>.

<!-- -->

-   widlproc executables are in place for Linux and Mac users meaning it
    is possible for those users to generate API specifications that
    fullfill the latest W3C widl-specification. Paddy is working on
    widlproc for Windows.

API specification alignment with task 4.1 API implementations and further work on APIs[¶](#API-specification-alignment-with-task-41-API-implementations-and-further-work-on-APIs)
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

See
</t3-4/wiki/API_specification_alignment_with_task_41_API_implementations>

-   Context API: Christos explained this API. Generally the current API
    specification is not detailed enough, it is too generic so the task
    4.1 implementation had to detailj things that was not stated in the
    specification. [AP Christos to coordinate with Dieter on further
    work with the Context
    API](http://dev.webinos.org/redmine/issues/888)

<!-- -->

-   Events API: Christian to check with Andre.

<!-- -->

-   AppLauncher API: Christian checks with Andre if he could take
    ownership.

<!-- -->

-   Messaging API: [AP Stefano to provide feedback on
    implementation](http://dev.webinos.org/redmine/issues/889)

<!-- -->

-   NFC API: Stefano owner. [AP to document feedback on implementation
    and proposed further
    work](http://dev.webinos.org/redmine/issues/890)

<!-- -->

-   Payment API: Christian is owner of this API and has provided
    implementation feedback and other suggestions for this API at the
    wiki. Further work on the APi is much related to the webinos
    architecture so this is a joint effort with task 3.3. It also might
    be good to talk to Dave as he has been prototyping payment using NFC
    and a Payment API.

<!-- -->

-   Sensors API: Claes owner and implementation feedback and other
    suggestions for this API is stated at the wiki. There is currently
    discussions going on in W3C on Sensor APIs. A set of simple sensor
    specific APIs is proposed. These APIs typically provide access to
    in-device sensors such as proximity and ambient light sensors.
    However, we also must consider external sensors as we have use cases
    for accessing a sensor in another device, for example getting the
    location from another device. In addition we must be able to access
    typical "not-in-device" sensors such as pulse meters (for which we
    had a demo at MWC). So discovery is important and the current
    webinos Sensor API leverages the webinos Discovery API. Another
    option is to create sensor APIs based on Web Intents discovery.
    [Action Claes to define how to take the Sensor API further
    considering W3C activities on Sensor
    APIs](http://dev.webinos.org/redmine/issues/885).

<!-- -->

-   Discovery API: Alexander implemented this in task 4.1 so there is an
    [action on him to state deviations in the implementation compared to
    the specification and state other suggestions for further work on
    this API based on implementation
    experiences](http://dev.webinos.org/redmine/issues/883). Ziran
    states that there are two parts of the discovery implementation in
    task 4.1:
    -   Service Discovery coupled with RPC (assume this implements
        webinos Service Discovery API)
    -   Device Discovery exposed to web developers (we have no API
        specification for this?)\
        Claes requested documentation on the current discovery
        implementation to get a better understanding on how we should
        progress on discovery and Ziran got an [action to briefly
        document current discovery API implementation done in task
        4.1](http://dev.webinos.org/redmine/issues/891).\
        Another question is potential alignment of this API with ongoing
        standardization in W3C or elsewhere. We have to consider Web
        Intents, see for example 8.1 wiki on this,
        </wp8-1/wiki/Web_Intents>
        and maybe also Opera/CableLabs proposal,
        <http://people.opera.com/richt/release/specs/discovery/Overview.html>.

<!-- -->

-   TV API: Martin owner and has provided suggestions for improvements.

<!-- -->

-   User profile API. Ronny owner and he has promised to come back with
    feedback at the end of week 19, i.e. this week.

<!-- -->

-   Vehicle API: Simon owner. No more suggestions in addition to what is
    already stated at the wiki.

<!-- -->

-   Widget API: Christian to talk to Andre. There are [feedback from
    Dom](http://dev.webinos.org/redmine/issues/878) based on his work
    with migrating this API to the latest widl-specification. Who should
    be owner of further work on this API, Paul or Paddy?

<!-- -->

-   "Wrapper APIs" based on referred APIs from W3C and WAC. Assuming we
    should continue to use wrappers the best approach would be to align
    the webinos wrappers with the latest version of the referred
    original specification from W3C or WAC. For the Contacts API
    Christian is doing this. For the Media Capture API nothing should be
    done as the proposal is that it should be superseeded by the new
    getUserMedia API. Actions for other APIs to be defined.

Aligning Webinos APIs with latest W3C and other standards[¶](#Aligning-Webinos-APIs-with-latest-W3C-and-other-standards)
------------------------------------------------------------------------------------------------------------------------

Please review and provide any other suggestions on this matter at this
wiki page: [Aligning Webinos APIs with latest W3C and other
standards](/t3-4/wiki/Aligning_Webinos_APIs_with_latest_W3C_standards).

Other[¶](#Other)
----------------

Everyone to execute their Actions stated at
</t3-4/issues>

Next meeting moved to Wednesday May 16 at 11.00 as May 17 is a public
holiday in several European countries (and Hans, an extremely important
day in Norway! :-) )

