API landscape[¶](#API-landscape)
================================

This section is an overview of existing API standardization and
collaboration projects.

World Wide Web Consortium (W3C)[¶](#World-Wide-Web-Consortium-W3C)
------------------------------------------------------------------

The [World Wide Web Consortium](http://www.w3.org/ "W3C") is an
international community where Member organizations, a full-time staff,
and the public work together to develop Web standards. W3C's mission is
"to lead the Web to its full potential". W3C is the most important
organization for standardizing web technology and an extensive set of
APIs for web application developers have been specified by W3C.

**W3C Web Applications (Web Apps) Working Group**

The W3C Web Applications WG provides specifications that enable improved
client-side application development on the Web, including specifications
both for application programming interfaces (APIs) for client-side
development and for markup vocabularies for describing and controlling
client-side application behavior.

This WG hosts a number of API specifications that are core for the web
as an application execution environment. APIs that are implemented in
all browers are for example XMLHTTPRequest and Document Object Model
(DOM). Other important APIs created by the Web Apps WG that are deployed
in modern browers are for example Web Workers, Web Messaging, File
Reading, Server-Sent Events and Web Sockets. The Web Apps WG has also
created a set of specifications for installable web applications, Web
Widgets, that for example are core specifications in web runtime
platforms such as [WAC](http://www.wacapps.net/web/portal/wac-2.0-spec).

See [Web Apps WG
charter](http://www.w3.org/2010/webapps/charter/Overview.html) and [Web
Apps WG Web Site](http://www.w3.org/2008/webapps/). A full list of the
WG's publications and their status can be found at [Web Apps WG
publications](http://www.w3.org/2008/webapps/wiki/PubStatus).

**W3C Device APIs and Policy (DAP) Working Group**

The mission of the Device APIs and Policy Working Group is to create
client-side APIs that enable the development of Web Applications that
interact with device hardware, services and applications such as the
camera, microphone, system sensors, native address books, calendars and
native messaging applications. Devices in this context include desktop
computers, laptop computers, mobile Internet devices (MIDs), cellular
phones, TVs, cameras and other connected devices.

A full list of API specifications created by the WG is here: [DAP
Roadmap](http://www.w3.org/2009/dap/#roadmap).

The DAP specifications that so far has got most implementation attention
are the Contacts API for which there are experimental implementations
and the HTML Media Capture API, which for example will be supported in
Android 3.0.

Previously a framework for the expression of security policies that
govern access to security-critical APIs was included in the deliverables
of the WG but according to the [new proposed DAP
charter](http://www.w3.org/2010/11/DeviceAPICharter.html) this is now
left out of the DAP WG deliverables. It is proposed to rename the WG to
"Device APIs Working Group". However, this does not mean that the WG no
longer addresses privacy and security as the group also aims at crafting
APIs that are both secure and privacy-enabling by design, based on the
current Web browser security model. This entails reusing existing
browser-based security metaphors where they apply and looking into
innovative security and privacy mechanisms where they don’t.

Furthermore, the new charter expands the set of APIs that should be
delivered by the WG. For example APIs for device and service discovery
is now inluded in the charter.

DAP's public web site is here: [W3C DAP](http://www.w3.org/2009/dap/).

**W3C Geolocation Working Group**

The mission of the Geolocation Working Group is to define a secure and
privacy-sensitive Geolocation API for accessing location information
from device GPS receiver or network positioning information as well as a
Device Orientation Event specification for using device orientation
information originating from device accelerometer, magnetometer and
gyro.

The Geolocation API is currently implemented in major modern web
browsers and according to public information the Device Orientation
Event specification is at least under implementation for iOs, Android
and Chrome.

See the [Geolocation WG
Charter](http://www.w3.org/2008/geolocation/charter/charter-2).

**W3C Web Real-Time Communications (Web-RTC) Working Group**

The mission of the recently formed Web Real-Time Communications Working
Group is to define client-side APIs to enable Real-Time Communications
in Web browsers. APIs specified by the WG will enable streaming access
to device capabilities, e.g camera and microphone, and API functions for
establish peer-to-peer connections between Web browsers, independent of
the network protocols used to establish the connections between peers.

See [Web-RTC Working Group
Charter](http://www.w3.org/2011/04/webrtc-charter.html) and [Web-RTC web
site](http://www.w3.org/2011/04/webrtc/)

**Other W3C actvities creating APIs for web applications**

-   The [HTML5 specification](http://www.w3.org/TR/html5/) contains a
    number of APIs for web applications, e.g. an API for playing of
    video and audio to be used with the video and audio elements, an API
    that enabling offline Web applications and a drag & drop API.

<!-- -->

-   The [Web Notifications API](http://www.w3.org/TR/notifications/) is
    an API for displaying simple notifications to the user.

<!-- -->

-   The [Web Events Working Group](http://www.w3.org/2010/webevents/)
    develops specifications for physical multitouch interface events.

<!-- -->

-   The [HTML Speech Incubator
    Group](http://www.w3.org/2005/Incubator/htmlspeech/) investigates
    the feasibility of integrating speech technology in HTML5.

Web Hypertext Application Technology Working Group (WHATWG)[¶](#Web-Hypertext-Application-Technology-Working-Group-WHATWG)
--------------------------------------------------------------------------------------------------------------------------

[WHATWG](http://www.whatwg.org/) is a community of people interested in
evolving the Web. It focuses primarily on the development of HTML and
APIs needed for Web applications. The WG was founded by individuals of
Apple, the Mozilla Foundation, and Opera Software in 2004, due to
concerns on the W3C’s direction with HTML and XHTML.

WHATWG has provided major input to the W3C HTML5 specification as well
as to other specifications relating to web applications, e.g. Web
Workers , Web Storage, the Web Sockets API, and Server-Sent Events.

Wholesale Application Community (WAC)[¶](#Wholesale-Application-Community-WAC)
------------------------------------------------------------------------------

The [Wholesale Applications
Community](http://www.wacapps.net/web/portal "WAC") is an open, global
alliance formed from the world's leading telecoms operators. WAC will
unite a fragmented applications marketplace and create an open industry
platform that benefits the entire ecosystem, including applications
developers, handset manufacturers, OS owners, network operators and end
users.

WAC is based on W3C web technology such as HTML5, JavaScript, DOM and
web widgets. In addition WAC has specified a set of APIs providing
access to hardware and software device capabilities as well as a
security policy framework to control the access to the sensitive device
APIs.

Full list of WAC specifications can be found here:

-   [WAC 1.0](http://specs.wacapps.net/1.0/dec2010/)
-   [WAC 2.0](http://www.wacapps.net/web/portal/wac-2.0-spec)

PhoneGap[¶](#PhoneGap)
----------------------

[PhoneGap](http://www.phonegap.com/) allows developers to build
applications with web technology that are wrapped into native
applications suited for the target platform giving access to APIs
provided by the native platform. The following table lists the APIs
available for the platforms supported by PhoneGap: [PhoneGap supported
feature](http://www.phonegap.com/features). For API documentation see
[PhoneGap API reference](http://docs.phonegap.com/).

Nokia/Symbian Web Runtime environment[¶](#NokiaSymbian-Web-Runtime-environment)
-------------------------------------------------------------------------------

The [Nokia/Symbian Web
Runtime](http://library.forum.nokia.com/index.jsp?topic=/Web_Developers_Library/GUID-A359B122-CB52-492C-8C0D-0062ED0A6A89.html "WRT")
provides an application environment for web widgets that includes a set
of device APIs, [Symbian Platform Services
2.0](http://library.forum.nokia.com/index.jsp?topic=/Web_Developers_Library/GUID-A359B122-CB52-492C-8C0D-0062ED0A6A89.html).

