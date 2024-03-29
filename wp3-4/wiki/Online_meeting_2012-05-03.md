Online meeting 2012-05-03[¶](#Online-meeting-2012-05-03)
========================================================

Attendees[¶](#Attendees)
------------------------

    Christian Fuhrhop    gotowebinos@fokus.fraunhofer.de

    Claes Nilsson    claes1.nilsson@sonymobile.com

    Paolo Vergori (ISMB)    vergori@ismb.it

    Simon Isenberg    simon.isenberg@bmw.de

    ziran sun    ziran.sun@samsung.com

    Andre Paul    andre.paul@fokus.fraunhofer.de

    John Lyle    john.lyle@cs.ox.ac.uk

    Nick Allott / Paddy Byers    paddy.byers@gmail.com

Resource overview.[¶](#Resource-overview)
-----------------------------------------

Action for all partners to fill in the wiki table under
[Resources](/t3-4/wiki#Resources)
with estimated effort in PM and workarea. Still missing input from
Antenna, Deutsche Telecom, Ercim, IBBT, Impleo, Polito, Samsung, TIS,
TNO, TUB, UniCT, VisionMobile.

Update all task 3.2 APIs according to latest W3C widl-specification.[¶](#Update-all-task-32-APIs-according-to-latest-W3C-widl-specification)
--------------------------------------------------------------------------------------------------------------------------------------------

See
</t3-4/wiki/API_specification_update_due_to_new_W3C_widlspecification>.

Dom is leading migration. He has already migrated Applauncher, TV,
Vehicle and Payment APIs and will continue to with context, webinos core
and widget.

We do not want to spend time on migrating APIs that we have abandoned
will not implement. Any more API to add to
</t3-4/wiki/Task_32_APIs_to_remove>?
Looking at the table at
</wp4/wiki/Delivery_status>
implementation status is missing for several APIs. An e-mail check gave:

Attestation module (John) - Probably removed\
Authentication module (John) - Probably kept\
User Profile module (Ronny) - Claes to check with Ronny\
Events Module - Implemented and much used

Still need to decide how we deal with referred APIs from W3C and WAC.

API specification alignment with task 4.1 API implementations[¶](#API-specification-alignment-with-task-41-API-implementations)
-------------------------------------------------------------------------------------------------------------------------------

See
</t3-4/wiki/API_specification_alignment_with_task_41_API_implementations>

We need input here. Each API must have an owner/editor that is
responsible for keeping the APi up to date with our implementation!
Please provide feedback at this wiki page!

New proposed APIs[¶](#New-proposed-APIs)
----------------------------------------

See
</t3-4/wiki/New_proposed_Webinos_APIs>

Pulse meter API:\
Current approach is that a low level Bluetooth API will not be specified
by Webinos. Instead new sensor types for which we have use cases will be
added to the Webinos Sensor API. It is the implementation of the Sensor
API that accesses the different sensors using the relevant low level
protocols, e.g. Bluetooth.

[Action Ziran to add proposed additional sensor types to Sensor
API](http://dev.webinos.org/redmine/issues/874)

Aligning Webinos APIs with latest W3C and other standards[¶](#Aligning-Webinos-APIs-with-latest-W3C-and-other-standards)
------------------------------------------------------------------------------------------------------------------------

See
</t3-4/wiki/Aligning_Webinos_APIs_with_latest_W3C_standards>

Discussion on Gallery API. A new version of the W3C Gallery API, which
is based on Web Intents, has been submitted to W3C DAP. We must start an
investigation on Web Intents and Webinos. However, we also must consider
the new System Level API working group that currently is formed within
W3C. The work in this group will probably be very relevant to webinos.

[Action Claes to review proposed charter for the new W3C System Level
API working group and initiate discussion on how Webinos should work
with this group](http://dev.webinos.org/redmine/issues/875)

[Action Claes to start a prestudy on Web Intents for
Webinos](http://dev.webinos.org/redmine/issues/876)

Other[¶](#Other)
----------------

Everyone to execute their Actions stated at
</t3-4/issues>

