Online meeting 2011-04-21[¶](#Online-meeting-2011-04-21)
========================================================

Attendees[¶](#Attendees)
------------------------

Christian Fuhrhop (Fraunhofer FOKUS)\
Alexander Futasz (Fraunhofer FOKUS)\
Ronny Graefe (DTAG)\
Matthias Faeth (TNO)\
Marco, Stefano (ISMB)\
Habib Virji (Samsung)\
Claes Nilsson (SonyEricsson)\
Simon Isenberg (BMW)\
Anders Isberg (SonyEricsson)\
Ziran Sun (Samsung)

Agenda for WP 3.2 meeting in Berlin[¶](#Agenda-for-WP-32-meeting-in-Berlin)
---------------------------------------------------------------------------

Wednesday is the "WP 3.2 day" and we will also have a one hour slot at
the Thursday. For agenda see
<http://79.125.104.127/redmine/projects/wp3-1/wiki/WP_3_Berlin_Meeting_May_3-5>.

Access to APIs on remote devices.[¶](#Access-to-APIs-on-remote-devices)
-----------------------------------------------------------------------

See
<http://79.125.104.127/redmine/projects/t3-2/wiki/Access_to_APIs_on_remote_devices>
and e-mails.\
Paul not present so discussion postponed to berlin.

IDL Tool.[¶](#IDL-Tool)
-----------------------

See
<http://79.125.104.127/redmine/projects/t3-2/wiki/IDL_Tool_Chain_instructions>
and mails.

Nick not present but Alexander stated there is a git repository that
holds the tools. Instructions on how to use the tool needs improvements.
Alexander to send a mail to Nick on this.

TV and STB control API ([Task 166](http://79.125.104.127/redmine/issues/166))[¶](#TV-and-STB-control-API-Task-166)
------------------------------------------------------------------------------------------------------------------

A TVMediaElement interface, that inherits from and extends the
HTMLMediaElement, to support TV video broadcast streams which are mapped
as channels, is specified. The API supports listing, setting and
switching these channels.

All to review and prepare for discussion in Berlin.

Bar code reading.[¶](#Bar-code-reading)
---------------------------------------

The proposed conclusion is a JavaScript port of the ZXing Java library.
This was accepted by the meeting and means that bar code reading is out
of scope for WP 3.2.

Generic sensor API.[¶](#Generic-sensor-API)
-------------------------------------------

See proposed API by Claes,
[SensorAPI.widl](http://79.125.104.127/redmine/attachments/506/GenericSensorAPI.widl)
and notes at [Task 164](http://79.125.104.127/redmine/issues/164)

A new DOM 3 event is proposed. The proposal is inspired by W3C
DeviceOrientation event, Battery Stataus event and the Android sensor
API. Note that this needs to be complemented by some kind of sensor
discovery mechanism. To be reviewed by all and discussed in Berlin.

Vehicle API[¶](#Vehicle-API)
----------------------------

See [Vehicle API
wiki](http://79.125.104.127/redmine/projects/t3-2/wiki/Vehicle_API). At
this page Simon has stated vehuicle data to be exposed by the API and
there is a proposal for an event based API a la DeviceOrientation and
Battery status events. Simon stated that an event based approach may not
be the best solution for vehicle data as the browser may be flooded with
events and will make an alternative proposal.

Payment API[¶](#Payment-API)
----------------------------

Christian stated that it is not yet decided if we need a payment API.
This is to be discussed in Berlin and a decision has to be taken.

• Further walk through proposed APIs for phase 1:
<http://79.125.104.127/redmine/projects/t3-2/wiki/APIs_for_WP32_phase_1>\
• Walk through open tasks:
<http://79.125.104.127/redmine/projects/t3-2/issues>

