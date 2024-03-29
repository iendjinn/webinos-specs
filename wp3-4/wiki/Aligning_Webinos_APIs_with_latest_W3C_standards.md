Aligning Webinos APIs with latest W3C and other standards[¶](#Aligning-Webinos-APIs-with-latest-W3C-and-other-standards)
========================================================================================================================

This page list potential actions on APIs related to W3C evolution on
standards since task 3.2.

Video streams and video element[¶](#Video-streams-and-video-element)
--------------------------------------------------------------------

As part of the new media capture API (getUserMedia) and the work on
WebRTC, there are
[discussions](http://lists.w3.org/Archives/Public/public-media-capture/2012Mar/0048.html)
on how to assign the content of a video stream to a video element; we
should align with the outcome of these discussions in the TV API.

Web Intents for service discovery[¶](#Web-Intents-for-service-discovery)
------------------------------------------------------------------------

Google and Mozilla has been promoting Web Intents for quite some time
and a W3C Web Intents task force is running. Google is editing a [draft
Web Intents
specification](http://dvcs.w3.org/hg/web-intents/raw-file/tip/spec/Overview.html).
As part of task 8.1 webinos is impacting the standard to support local
and dynamic service discovery, for example in a home network. For more
information see [WP8.1 Web Intents
page](/wp8-1/wiki/Web_Intents).

We should consider if Webinos should switch to a Web Intents based
service discovery mechanism.

W3C Gallery API.[¶](#W3C-Gallery-API)
-------------------------------------

Webinos refers to the [W3C Gallery
API](http://dev.w3.org/2009/dap/gallery/) but this API has been
[shelved](http://lists.w3.org/Archives/Public/public-device-apis/2012Feb/0004.html).

We should consider if we should replace the Gallery API or propose
improvements to the API so it can be lifted to an active specification
again. One idea that was mentioned for that API was to use a Web Intents
approach. See proposal from Samsung on a [Web Intents based Gallery
API](https://dvcs.w3.org/hg/dap/raw-file/16185b62381d/gallery/index.html).

NFC API[¶](#NFC-API)
--------------------

W3C is launching an NFC Working Group. See [Near Field Communications
(NFC) Working Group
Charter](http://www.w3.org/2012/05/nfc-wg-charter.html). We should plan
on switching to the W3C API, by late 2012 or early 2013. More details on
the [W3C NFC
Wiki](http://www.w3.org/wiki/Near_field_communications_(NFC))

Event handling APIs[¶](#Event-handling-APIs)
--------------------------------------------

Align webinos event based APIs with event handling according to [W3C
Battery Status
API](http://dvcs.w3.org/hg/dap/raw-file/tip/battery/Overview.html)?

Align with W3C Sensor APIs[¶](#Align-with-W3C-Sensor-APIs)
----------------------------------------------------------

Intel and Telefonica have been editing a [Sensor
API](http://dvcs.w3.org/hg/dap/raw-file/tip/sensor-api/Overview.html)
that is similar to Webinos Sensor API. However, there has been a shift
to separate specifications for each of the sensors, with simple DOM
events. The DAP WG is likely to combine these with Web Intents for
access to off device sensors, and for selection between multiple sensors
on the same device.

Currently W3C DAP has specified the following sensor, actuator and
device status APIs:

-   [Vibration API](http://www.w3.org/TR/2012/CR-vibration-20120508/)
-   [Proximity
    events](http://dvcs.w3.org/hg/dap/raw-file/tip/proximity/Overview.html)
-   [Network Information
    API](http://dvcs.w3.org/hg/dap/raw-file/tip/network-api/Overview.html)
-   [Battery Status
    API](http://dvcs.w3.org/hg/dap/raw-file/tip/battery/Overview.html)

REST APIs[¶](#REST-APIs)
------------------------

Consider switching to REST APIs for some webinos APIs (Vehicle, TV,
Sensors…)

W3C DAP APIs does not cover installed web applications[¶](#W3C-DAP-APIs-does-not-cover-installed-web-applications)
------------------------------------------------------------------------------------------------------------------

See [Installing web apps - Browser vs System level
security](http://lists.w3.org/Archives/Public/public-device-apis/2012Feb/0046.html)

W3C System Level APIs WG[¶](#W3C-System-Level-APIs-WG)
------------------------------------------------------

W3C launches a new working group on system level APIs, see [Draft
charter for W3C System Applications
WG](http://www.w3.org/2012/05/sysapps-wg-charter.html). In addition, new
work on application packaging is chartered to take place in the Web Apps
WG. We should consider tracking/influencing their work using our WP 8.1
budget.

