Online meeting 2011-03-31[¶](#Online-meeting-2011-03-31)
========================================================

Attendees[¶](#Attendees)
------------------------

Sven Lachmund <lachmund@docomolab-euro.com>\
Marco, Stefano (ISMB) <gavelli@ismb.it>\
Habib Virji <habib.virji@samsung.com>\
Claes Nilsson <claes1.nilsson@sonyericsson.com>\
André Paul <andre.paul@fokus.fraunhofer.de>\
Ziran Sun <ziran.sun@samsung.com>\
Stefano Vercelli <stefano.vercelli@telecomitalia.it>\
Michael Vakulenko <michael@visionmobile.com>\
Daniel Coloma <dcoloma@tid.es>\
Matthias Faeth <matthias.faeth@tno.nl>\
Anders Isberg <anders.isberg@sonyericsson.com>\
Simon Isenberg <simon.isenberg@bmw.de>\
Katerina (NTUA) <ktouriki@epu.ntua.gr>\
Christian Furhop <christian.fuhrhop@fokus.fraunhofer.de>

General view on progress[¶](#General-view-on-progress)
------------------------------------------------------

No comments

Walk through open Tasks[¶](#Walk-through-open-Tasks)
----------------------------------------------------

See [Redmine WP3.2
issues](/t3-2/issues)

[Task 184 on Nick asynchronous versus synchronous
APIs](http://dev.webinos.org/redmine/issues/184): No progress, Nick not
present at meeting.

[Task 175 on Stefan Andersson/SEMC to review Aims for Security and
Privacy APIs](http://dev.webinos.org/redmine/issues/175): No progress.

Task 174 on Claes to investigate status for Application Launcher API in
W3C: Done. According to DAP phone meeting 2011-03-30 there is a decision
to not have the App Launcher in the charter. URI schemes are considered
enough. Andre stated that for web widgets an application launcher API
might be needed, for example for launching applications on remote
devices.\
[New task 188 on Andre on Application Launcher for
Widgets](http://dev.webinos.org/redmine/issues/188)

[Task 173 on Andre to conduct payment API
investigation](http://dev.webinos.org/redmine/issues/173): There are no
specific requirements in Webinos on a payment API. The GSMA OneAPI
Payment RESTful API is a potential solution for which JS wrappers could
easily be created. In addition there are multiple vendors of proprietary
payment method APIs are available today so it is not clear whether we
need this. Investigation to continue and we need a decision if a payment
API should be included in the scope of Webinos.

[Task 172 on Nick and Stefano to Investigate need for a specific Gallery
API](http://dev.webinos.org/redmine/issues/172): No progress.

[Task 171 on Claes to check handling of binary data in W3C File
APIs](http://dev.webinos.org/redmine/issues/171): Done. Binary data is
supported.

[Task 170 on Fraunhofer to investigate route forward for messaging
API](http://dev.webinos.org/redmine/issues/170): Alexander at Fraunhofer
suggests the WAC 2.0 messaging module as the usage of tel: and sms: (and
similar) URIs is too limited. While there aren't any particular
requirements just for messaging, there are use cases/stories that
include messaging (listed in Application Data APIs). The WAC 2.0
messaging module might be a good alternative as it provides:

-   Single API for sms, mms and email.
-   Sending, receiving and finding/reading messages (incl. attachments).

The W3C Messaging API is currently too limited as it does not support
receiving messages.

[Task 169 on Hans to investigate route forward for Bar Code
API](http://dev.webinos.org/redmine/issues/169): Fraunhofer commented
that ZXing Java API is not strictly specified and a one-to-one Java API
to JavaScript API translation is not possible. Fraunhofer (Alexander?)
to elaborate on this.\
[New Task 189 on Alexander to investigate rout forward for Bar Code
API](http://dev.webinos.org/redmine/issues/189)

[Task 168 on Simon to investigate route forward for Vehicle
API](http://dev.webinos.org/redmine/issues/168): Simon will provide
input next week.

[Task 167 on Stefano Vercelli to elaborate on DeviceInteraction API and
investigate Google Chrome APIs to access UI
functionality](http://dev.webinos.org/redmine/issues/167): Even thought
this seems useful functionality we don't have any specific requirements
on interaction with the user through beeps, vibrations etc. Claes
suggested that until we see clear requirements in Webinos we should have
low priority on this API and if we support it we should stick to simple
interaction such as vibrations and beeps.

[Task 166 on Dirk Thatmann to Provide input on TV and STB control
API](http://dev.webinos.org/redmine/issues/166): The main proposal is to
create of profile of the OIPF DAE JavaScript API for apps on a TV/STB.

[Task 165 on Stefano V to investigate W3C HTML Media Capture API versus
W3C Media Capture API](http://dev.webinos.org/redmine/issues/165): The
Media Capture API provides a little more functionality by the possible
to state options for the media capture. e.g. upper limit of images user
can take or maximum duration of a single video clip in seconds. Notice
that both APIs require the W3C File API
(<http://www.w3.org/TR/FileAPI/>). There are some ambiguities in the
specifications, e.g. not clear if the pictures/audios/videos are saved
on the filesystem. Stefano to send a mail with questions the the W3C DAP
public mailing list (<public-device-apis-request@w3.org>).

Claes stated that the HTML Media Capture specification is under
implementation for Android 3.0. See
<http://developer.android.com/sdk/android-3.0.html>. There are currently
no known implementations of the Media Capture API.

[Task 163 on Stefano to provide input on selection of Device Orientation
API](http://dev.webinos.org/redmine/issues/163): Stefano's main concern
with the W3C DeviceOrientation event specification is that it is still
an editor's draft. However, there are several implementations in
progress as stated on the wiki. (This was not mentioned at the meeting
but Claes offers to take an action to contact the editors of the
specification to get their view on the stability of the specification.
Task 163 updated and assigned to Claes.

[Task 162 on Daniel to investigate tool for auto-generating API stubs
from widls](http://dev.webinos.org/redmine/issues/162): Tool exists and
it is customized for Webinos. Daniel will send a mail with information
on the tool to the Webinos WP3 mailing list.

Access to remote APIs[¶](#Access-to-remote-APIs)
------------------------------------------------

Stefano has proposed an RPC mechanism where the underlying communication
mechanism (web sockets, XHR, etc) is hided to the developer. This has a
relation with overlay networking. Andre has also ideas on this. Claes
has set up a wiki page to be used to state ideas and brainstorming
around this issue: [Access to APIs on remote
device](/t3-2/wiki/Access_to_APIs_on_remote_devices)

[New Task 190 on Andre to state proposals for access to APIs on remote
devices](http://dev.webinos.org/redmine/issues/190)

-----------End of meeting-------------------

