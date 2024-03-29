Online meeting 2012-04-19[¶](#Online-meeting-2012-04-19)
========================================================

Attendees[¶](#Attendees)
------------------------

André Paul <andre.paul@fokus.fraunhofer.de>\
Krzysztof Wajtknecht <kwajtknecht@antennasoftware.com>\
Claes Nilsson <claes1.nilsson@sonyericsson.com>\
Andreas Botsikas <abot@epu.ntua.gr>\
Wei Guo (Samsung) <wei6.guo@partner.samsung.com>\
Ronny Gräfe (DTAG) <ronny.graefe@t-systems.com>\
Martin Lasak <martin.lasak@fokus.fraunhofer.de>\
Marco N/A\
Paolo Vergori - Michele Morello (ISMB) <vergori@ismb.it>\
H Myrhaug <hans@ambiesense.com>\
Simon Isenberg <simon.isenberg@bmw.de>\
ziran sun <ziran.sun@samsung.com>

Resource overview.[¶](#Resource-overview)
-----------------------------------------

The task 3.4 wiki is here:
</t3-4/wiki>.

**Action for all partners to fill in the table under "Resources" with
estimated effort in PM and workarea.**

Goals and work plan review.[¶](#Goals-and-work-plan-review)
-----------------------------------------------------------

There were no comments on the goals and work plan.

Tools and process for API specification generation[¶](#Tools-and-process-for-API-specification-generation)
----------------------------------------------------------------------------------------------------------

There has been a discussion on the mail list on the tool used for
creating our API specifications. A switch to W3C ReSpec has been
proposed in order to more "easy to read" and "W3C looking"
specifcations.

The decision is that initially we will continue to use the same tools as
for the phase 1 API specifications, i.e. widlrpoc. See “Tool Setup and
Usage”:
</t3-2/wiki/Tool_Setup_and_Usage>.
However, not that we use the “newwebidl” branch for task 3.4
specifications as stated below. The reason is that we are so far
dependent on the widlproc based tool chain not only for specification
creation but also for generation API stubs and SDK input.

This needs to be discussed more. Which is the main target audience for
Webinos API specifications? Webinios partners and webinos developers or
a wider audience? So we may re-consider this approach and use another
tool to create more easy to read specifications for a broader use. In
addition, API specifications that we submit as input proposal to W3C
have to be re-written into W3C format using ReSpec.

For phase 2 specifications we will use a branch “newwebidl” from the
phase 1 API specification Redmine repository:
</t3-2/repository/show?rev=newwebidl>

The updated html-generated API specifications will be placed here:
<http://dev.webinos.org/specifications/new/>

Update all task 3.2 API according to latest W3C widl-specification[¶](#Update-all-task-32-API-according-to-latest-W3C-widl-specification)
-----------------------------------------------------------------------------------------------------------------------------------------

See wiki [API specification update due to new W3C widl
specification](/t3-4/wiki/API_specification_update_due_to_new_W3C_widlspecification)
.

Dom has started to do the migration and some specifications are ready
for review. The tool chain currently only supports generation of
HTML-specifications on Linux machines.

Actions:

-   **Claes:** [Discuss with Dom and Paddy on process for migrating API
    specifications to latest W3C
    widl-specifcation](http://dev.webinos.org/redmine/issues/861)

<!-- -->

-   **Simon:**[Review Vehicle API updated to latest
    widl-specification](http://dev.webinos.org/redmine/issues/862)

<!-- -->

-   **Alexander:** [Review TV API updated to latest
    widl-specification](http://dev.webinos.org/redmine/issues/863)

<!-- -->

-   **Christian:** [Review Payment API updated to latest
    widl-specification](http://dev.webinos.org/redmine/issues/864)

Task 3.2 APIs to remove[¶](#Task-32-APIs-to-remove)
---------------------------------------------------

Martin has proposed thatMedia capture API should be removed from the
Webinos delivery. It should be replaced by GetUserMedia.

**Action for all to consider if more APIs should be removed from the
Webinos delivery and state that at the wiki:** [APIs to
remove](/t3-4/wiki/Task_32_APIs_to_remove).

API specification alignment with task 4.1 API implementations[¶](#API-specification-alignment-with-task-41-API-implementations)
-------------------------------------------------------------------------------------------------------------------------------

It is important that our API specifications get aligned with what we
actually implemented in task 4.1. At the wiki [API specification
alignment with task 4.1 API
implementations](/t3-4/wiki/API_specification_alignment_with_task_41_API_implementations)
all phase 1 APIs are listed. For each API I have stated the assumed
responsible editor.

**Action for all API specification editors / API implementors to
coordinate and to state responsible editor and specification updates
need based on current webinos implementation.**

New proposed APIs[¶](#New-proposed-APIs)
----------------------------------------

So far two new APIs have been proposed, Bluetooth API and Actuator API.
See wiki [New proposed
APIs](/t3-4/wiki/New_proposed_Webinos_APIs)

Actions:

-   **Ziran**: Place information on proposed Bluetooth API at the 3.4
    wiki page on [New proposed Webinos
    APIs](/t3-4/wiki/New_proposed_Webinos_APIs)
-   **Paolo**: Place information on proposed oAuth API 3.4 at the wiki
    page on [New proposed Webinos
    APIs](/t3-4/wiki/New_proposed_Webinos_APIs)
-   **Andre**: [Place information on proposed Actuator API 3.4 wiki
    page](http://dev.webinos.org/redmine/issues/865)
-   **All**: Consider new APIs to include in the webinos phase 2
    delivery and state that on wiki page [New proposed Webinos
    APIs](/t3-4/wiki/New_proposed_Webinos_APIs)

Aligning Webinos APIs with latest W3C and other standards[¶](#Aligning-Webinos-APIs-with-latest-W3C-and-other-standards)
------------------------------------------------------------------------------------------------------------------------

**Action for all to consider alignment with latest W3C and other
standards and state this on the wiki page:** [Aligning Webinos APIs with
latest W3C and other
standards](/t3-4/wiki/Aligning_Webinos_APIs_with_latest_W3C_standards)

Other[¶](#Other)
----------------

No other busines.

