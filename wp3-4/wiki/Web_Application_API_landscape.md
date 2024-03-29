Web Application API landscape[¶](#Web-Application-API-landscape)
================================================================

This page provides an overview of existing API standardization and
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

**W3C Device APIs (DAP) Working Group**

The mission of the Device APIs Working Group is to create client-side
APIs that enable the development of Web Applications that interact with
device hardware, services and applications such as the camera,
microphone, system sensors, native address books, calendars and native
messaging applications. Devices in this context include desktop
computers, laptop computers, mobile Internet devices (MIDs), cellular
phones, TVs, cameras and other connected devices. See the [DAP WG
charter](http://www.w3.org/2011/07/DeviceAPICharter).

A full list of API specifications created by the WG is here: [DAP
Roadmap](http://www.w3.org/2009/dap/#roadmap).

Given the sensitive nature of the data and sensors to which these APIs
grant access, the Working Group also aims at crafting APIs that are both
secure and privacy-enabling by design, based on the current Web browser
security model. This entails reusing existing browser-based security
metaphors where they apply and looking into innovative security and
privacy mechanisms where they don’t.

DAP's public web site is here: [W3C DAP](http://www.w3.org/2009/dap/).

**W3C System Applications Working Group**

The System Applications Working Group is chartered to define a runtime
environment, security model, and associated APIs for building Web
applications with comparable capabilities to native applications. This
requires stronger integration with the host platform than is the case
for traditional web pages.

The main distinction between the scope of the DAP WG ("APIs for browser
based Web Applications), and the System Applications WG ("APIs for
System Web Applications") is the security model. Browsers are designed
to cope with the user visiting untrusted web sites, necessitating a
cautious approach to security that narrowly limits what a particular
website can do. The line is drawn at "more harmful than what is
tolerable inside a sandbox". The contrast between the two contexts can
be illustrated by comparing a) an application with limited access to
specific fields in the user's contacts, and b) an application that
implements a contacts manager, where the application is entrusted with
the ability to access, create, delete and update entries. See [System
Applications WG Draft
charter](http://www.w3.org/2012/05/sysapps-wg-charter.html).

**W3C Web Intents task force**

Web Intents is a service discovery mechanism and light-weight RPC system
between web apps, modeled after the similarly-named API in Android. In
W3C a joint DAP WG / Web Apps WG task force is running. See [W3C Web
Intents wiki](http://www.w3.org/wiki/WebIntents) and [W3C Web Intents
public mailing list
archive](http://lists.w3.org/Archives/Public/public-web-intents/).

Google is the main driving player for Web Intents and is editor of the
[W3C draft Web Intents
specification](http://dvcs.w3.org/hg/web-intents/raw-file/tip/spec/Overview.html).
They also manage the [webintents.org site](http://webintents.org/) that
contains use cases and examples of Web Intents services.

In addition Sony has provided the [Web Intents Addendum - Local Services
specification](http://w3c-test.org/dap/wi-addendum-local-services/) that
defines how Services on Web Intents enabled UPnP and mDNS devices can be
discovered and accessed.

Web Intents based APIs are under development within W3C and currently
there are the following drafts:

-   [Pick Media Intent](http://w3c-test.org/dap/gallery/) (Web Intents
    based Gallery API)

<!-- -->

-   [Pick Contacts Intent](http://w3c-test.org/dap/contacts/) (Web
    Intents based Contacts API)

For more information on Web Intents see the "Web Intents for webinos
investigation" section in this delivery.

**W3C Geolocation Working Group**

The mission of the Geolocation Working Group is to define a secure and
privacy-sensitive Geolocation API for accessing location information
from device GPS receiver or network positioning information as well as a
Device Orientation Event specification for using device orientation
information originating from device accelerometer, magnetometer and
gyro.

The Geolocation API is currently implemented in major modern web
browsers and according to public information the Device Orientation
Event specification is at least implemented in iOs browser, Android
browser, Chrome, Firefox for Android and Opera Mobile for Android.

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

<!-- -->

-   The Near Field Communications (NFC) Working Group is being chartred.
    NFC is a form of short range wireless communication in which NFC
    devices such as mobile can communicate with each other over a
    typical distance of 4cm or less. See [W3C NFC WG draft
    charter](http://www.w3.org/2012/05/nfc-wg-charter.html).

<!-- -->

-   The Audio Working Group is chartered to develop specifications which
    define a client-side script API adding more advanced audio
    capabilities than are currently offered by audio elements. See [W3C
    Audio WG charter](http://www.w3.org/2011/audio/charter/).

<!-- -->

-   The Web Web Cryptography Working Group defines a high-level API
    providing common cryptographic functionality to Web Applications.
    See [W3C Web Web Cryptography Working Group
    charter](http://www.w3.org/2011/11/webcryptography-charter.html)

For more information on W3C standards for Web Applications on Mobile see
[Standards for Web Applications on Mobile: current state and
roadmap](http://www.w3.org/2012/05/mobile-web-app-state/). This document
summarizes the various technologies developed in W3C that increase the
capabilities of Web applications, and how they apply more specifically
to the mobile context.

Web Hypertext Application Technology Working Group (WHATWG)[¶](#Web-Hypertext-Application-Technology-Working-Group-WHATWG)
--------------------------------------------------------------------------------------------------------------------------

[WHATWG](http://www.whatwg.org/) is a community of people interested in
evolving the Web. It focuses primarily on the development of HTML and
APIs needed for Web applications. The WG was founded by individuals of
Apple, the Mozilla Foundation, and Opera Software in 2004, due to
concerns on the W3C’s direction with HTML and XHTML.

WHATWG has provided major input to the W3C HTML5 specification as well
as to other specifications relating to web applications, e.g. Web
Workers, Web Storage, the Web Sockets API, and Server-Sent Events.

WHATWG is a [W3C Community
Group](http://www.w3.org/community/about/#cg).

Mozilla Web API / Firefox Mobile OS (Boot To Gecko)[¶](#Mozilla-Web-API-Firefox-Mobile-OS-Boot-To-Gecko)
--------------------------------------------------------------------------------------------------------

Mozilla has launched the [Boot to Gecko
project](http://www.mozilla.org/en-US/b2g/about/) to create a true
Web-based Mobile Platform, i.e. a browser based Operating System built
entirely on HTML5, Javascript and CSS without the need for an
intermediate OS layer.

The Boot to Gecko project is based on standard APIs but when standards
are missing (including telephony, SMS, camera, bluetooth, USB and NFC),
they are working with standards bodies and other vendors to create them.
This work is driven in the [Mozilla Web API
project](https://wiki.mozilla.org/WebAPI).

Tizen[¶](#Tizen)
----------------

[Tizen](https://www.tizen.org/) provides an operating system and
applications based on HTML5. The Tizen SDK and API allow developers to
use HTML5 and related web technologies to write applications that run
across multiple device segments including smartphones, tablets,
netbooks, in-vehicle infotainment devices, smart TVs, and more.

The Tizen project resides within the [Linux
Foundation](http://www.linuxfoundation.org/collaborate/labs/tizen).

Tizen both uses W3C API specifications and defines their own additional
APIs, e.g. Phone Call API, Bluetooth API, Media Content (Gallery) API
and NFC API. See [Tizen
documentation](https://developer.tizen.org/documentation).

Wholesale Application Community (WAC)[¶](#Wholesale-Application-Community-WAC)
------------------------------------------------------------------------------

The [Wholesale Applications Community](http://www.wacapps.net/ "WAC")
started as an open global alliance made up of leading communications
companies including network operators, device and network equipment
manufacturers, that was committed to make it easier for developers to
innovate by using operator network APIs delivered by a single
cross-operator API platform. Concentrating in Asia for now, WAC also
supports an HTML5 based application platform.

WAC has now been folded into the GSMA, the mobile industry trade body.
The technology side of WAC's work is being split off and bought by
[Apigee](http://www.zdnet.com/blog/gardner/sonoa-becomes-apigee-offers-new-and-rebranded-api-management-and-analysis-product-lines/3868),
an API management firm. As part of the deal, Apigee will continue to
develop the WAC web runtime and APIs and provide them back to the
operators as a managed service.

WAC's current focus is a [Payment
API](http://www.wacapps.net/payment-api) supporting operator billing
through users phone bill.

Full list of WAC specifications can be found here:

-   [WAC Specifications 2.1](http://specs.wacapps.net/)
-   [WAC 1.0](http://specs.wacapps.net/1.0/dec2010/)

PhoneGap[¶](#PhoneGap)
----------------------

[PhoneGap](http://www.phonegap.com/) allows developers to build
applications with web technology that are wrapped into native
applications suited for the target platform giving access to APIs
provided by the native platform. PhoneGap is now an Apache Foundation
project under the name
[Cordova](http://phonegap.com/2012/03/19/phonegap-cordova-and-what%E2%80%99s-in-a-name/).

The following table lists the APIs available for the platforms supported
by PhoneGap: [PhoneGap supported
feature](http://www.phonegap.com/features). For API documentation see
[PhoneGap API reference](http://docs.phonegap.com/).

Google Chrome extension APIs[¶](#Google-Chrome-extension-APIs)
--------------------------------------------------------------

Google Chrome Extensions are applications, created with html, css and
JS, that run inside the Chrome browser and provide additional
functionality, integration with third party websites or services, and
customized browsing experiences. These extensions can use a set of APIs
such as chrome.bookmarks and chrome.tab to interact with the browser.
See [Chrome APIs](http://developer.chrome.com/extensions/api_index.html)
and [Chrome experimental
APIs](http://developer.chrome.com/extensions/experimental.html).

Nokia/Symbian Web Runtime environment[¶](#NokiaSymbian-Web-Runtime-environment)
-------------------------------------------------------------------------------

The [Nokia/Symbian Web
Runtime](http://library.forum.nokia.com/index.jsp?topic=/Web_Developers_Library/GUID-A359B122-CB52-492C-8C0D-0062ED0A6A89.html "WRT")
provides an application environment for web widgets that includes a set
of device APIs, [Symbian Platform Services
2.0](http://library.forum.nokia.com/index.jsp?topic=/Web_Developers_Library/GUID-A359B122-CB52-492C-8C0D-0062ED0A6A89.html).

