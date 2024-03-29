Web Intents for webinos investigation[¶](#Web-Intents-for-webinos-investigation)
================================================================================

Introduction[¶](#Introduction)
------------------------------

Web Intents is a service discovery mechanism and light-weight RPC system
between web applications, modeled after the similarly-named API in
Android. Standardization is in progress and W3C runs a joint DAP WG /
Web Applications WG task force. See [W3C Web Intents
wiki](http://www.w3.org/wiki/WebIntents) and [W3C Web Intents public
mailing list
archive](http://lists.w3.org/Archives/Public/public-web-intents/).

Google is the main driving player for Web Intents and is editor of the
[W3C draft Web Intents
specification](http://www.w3.org/TR/2012/WD-web-intents-20120626/). They
also manage the [webintents.org site](http://webintents.org/) that
contains use cases and examples of Web Intents Services. Native support
for Web Intents is currently implemented in Chrome for desktop. However,
Google's plans for supporting Web Intents in Chrome for Android are
currently unclear. Current public information only describes a project
under Google Summer of Code 2012 for integrating Web Intents for Android
Intents, see [WebIntents on
Android](http://code.google.com/p/openintents/wiki/GSoC2012Ideas#WebIntents_on_Android).
The project can be followed at github, [openintents /
gsoc2012](https://github.com/openintents/gsoc2012).

Mozilla has also specified a similar concept called [Web
Activities](https://wiki.mozilla.org/WebAPI/WebActivities) and [Web
Activities: counter-proposal to Web
Intents](http://lists.w3.org/Archives/Public/public-web-intents/2012Jun/0061.html).

W3C is driving Web Intents as the standard for web based service
discovery and it is important to align webinos with Web Intents.
However, the concept is still not established enough for webinos to make
a complete shift to a Web Intents based architecture. Standardization is
in progress and the only existing browser native implementation is
Google Chrome for desktop. We do not yet know how the final standard
will look like. An example is Ian Hickson's proposal for merging the
W3C/Google and Mozilla concepts. See [register\*Handler and Web
Intents](http://lists.whatwg.org/htdig.cgi/whatwg-whatwg.org/2012-July/036719.html).

So far webinos activities on Web Intents have been to impact the
development of the standard in W3C. The webinos project is active in the
W3C Web Intents task force through several partners, Sony, W3C and
Telecom Institute Paris. One example is Sony's submission of the [Web
Intents Addendum - Local
Services](http://w3c-test.org/dap/wi-addendum-local-services/)
specification to support discovery and use of Services on Web Intents
enabled devices in local wifi networks.

This section of the task 3.4 delivery report provides basic information
on Web Intents and gives a high level suggestion for aligning webinos
with Web Intents, i.e. making webinos Services discoverable for Web
Intents enabled web applications.

Web Intents standardization overview[¶](#Web-Intents-standardization-overview)
------------------------------------------------------------------------------

### Web Intents basics[¶](#Web-Intents-basics)

The [W3C Web Intents specification](http://www.w3.org/TR/web-intents/)
is currently a working draft. All three editors are from Google.

The basic Web Intents concepts are:

-   An **Intent** is an action to be performed by a Service and is
    defined by:
    -   **Action**: a URI defining what to do (share, pick, view, etc)
    -   **Type**: the data type to perform the action on (image, url,
        json etc)

<!-- -->

-   A **Client** web app requests an Intent be handled, the User Agent
    allows the user to select which Service to use, and the Service
    performs the action of the Intent, possibly using data passed as
    input in the Intent.
    -   Client Web Apps requests an action to be performed by creating
        an Intent and issuing ”startActivity”.

<!-- -->

-   A **Service** is normally implemented as a web application. It lists
    the Intents it can handle and executes the action of the intent. A
    Service is defined by:
    -   Action it can handle.
    -   Type it can handle.
    -   A Service may return data as output to the Client

<!-- -->

-   Services must be registered prior to being available for Client web
    apps to use and there are several ways to register Web Intents
    Services, for example:
    -   Markup, the \<intent\> tag, is used by web pages that register
        Services. A Web page can register itself or another same domain
        web page as the Service handler.
    -   For the Chrome Web Intents implementation Services are
        registered through the [Chrome manifest
        file](http://code.google.com/chrome/extensions/manifest.html#intents)
    -   Dynamic Service registration based on local network service
        discovery is also specified according to [Web Intents Addendum -
        Local
        Services](http://w3c-test.org/dap/wi-addendum-local-services/).
        See the section below on local network service discovery.
    -   Registration/Unregistration through a JS API is also proposed.

### Web Intents based APIs[¶](#Web-Intents-based-APIs)

Web Applications can use Web Intents as a general service discovery
mechanism and Web Intents based APIs can be used to interact with the
service. However, there is still much to do in standardizing Web Intents
based APIs. Currently there are following W3C drafts:

-   [Pick Media Intent](http://w3c-test.org/dap/gallery/) (Web Intents
    based Gallery API)

<!-- -->

-   [Pick Contacts Intent](http://w3c-test.org/dap/contacts/) (Web
    Intents based Contacts API)

In addition the following pages deal with interaction patterns between
Client and Service applications but they don't specify tangible APIs:

-   [webintents.org](http://webintents.org/) Contains a list of intents
    that Google believes the majority of applications and services will
    use and data formats for interaction between Clients and Services.
    However, the level of detail is not enough for providing full
    interoperability between Clients and Services.

<!-- -->

-   [Web Intents payload data format for MIME
    types](http://www.w3.org/wiki/WebIntents/MIME_Types): Proposes
    payload data format clients must use, and services can expect, when
    using MIME type specifiers.

<!-- -->

-   [Web Intents payload data format for schema.org
    types](http://www.w3.org/wiki/WebIntents/schema.org_Types): Proposes
    payload data format clients must use, and services can expect, when
    using schema.org types are used.

Note that some Web Intents use cases require simple RPC APIs and some
use cases require APIs supporting a longer lasting relation between the
Client application and the Service application.

-   RPC APIs: Client sends payload data to the Service with intents
    attributes and Service returns data with the intents invocation
    method callback function. The W3C [Pick Media
    Intent](http://w3c-test.org/dap/gallery/) API and [Pick Contacts
    Intent](http://w3c-test.org/dap/contacts/) are examples of RPC-based
    APIs.

<!-- -->

-   Message channel based APIs/protocols: Web Intents allows a longer
    lasting relation between the Client and the Service by using an HTML
    message channel. On top of this message channel a high level
    protocols can run. For an example of the case when an HTML message
    channel between the Client and Service pages is used to run a high
    level protocol see slide 18 in the presentation [W3C Web Intents -
    Local Network Service
    Discovery](http://www.w3.org/wiki/images/2/2e/V4_W3C_Web_Intents_-_Local_UPnP_Service_Discovery.pdf).
    Here a high level "TV Control Protocol", independent of low level
    communication (for example UPnP) method and details, is used by the
    Client web application.

When comparing Web Intents with the [webinos Service Discovery
API](http://dev.webinos.org/specifications/new/servicediscovery.html) we
see that one advantage with the webinos API is that existing standard or
webinos JavaScript APIs are used to interact with the discovered and
selected Service. For Web Intents there is still much to be done in
defining the APIs/protocols to use between Clients and Services.

### Web Intents for local network service discovery[¶](#Web-Intents-for-local-network-service-discovery)

Web Intents is a general Service Discovery concept and Services, capable
of executing the requested Action, could be located "anywhere". This
means that Web Intents Services are not only static registered web
services but that they could also be dynamically discovered local
services, e.g. services on UPnP enabled devices in local wifi networks
or services in devices that are locally connected through Bluetooth or
any other short range communication method. These dynamic Services may
or may not have a UI.

To support discovery and usage of Web Intents Services on local network
devices Sony has provided the [Web Intents Addendum - Local
Services](http://w3c-test.org/dap/wi-addendum-local-services/)
specification that defines how Services on Web Intents enabled UPnP and
mDNS devices can be discovered and accessed. There is also a demo and a
presentation, see [WebIntents/SonyMobile - Local Network Service
Discovery](http://www.w3.org/wiki/WebIntents/SonyMobile_-_Local_Network_Service_Discovery).
The basic idea with this proposal is that UPnP and other common low
level service discovery mechanisms should be supported by the UA and
that this will be utilized by the UA's Web Intents implementation to
discover and dynamically register local network services.

The [W3C WebIntents/Home Discovery and Web
Intents](http://www.w3.org/wiki/WebIntents/Home_Discovery_and_Web_Intents)
also lists different use cases and solution proposals for "Home
discovery" with Web Intents.

In addition Opera and CableLabs have submitted an unofficial draft of an
API for discovery and access to local network services that is not based
on Web Intents, [Networked Service Discovery and
Messaging](http://people.opera.com/richt/release/specs/discovery/Overview.html).

### Web Intents and Sensor use cases[¶](#Web-Intents-and-Sensor-use-cases)

It is proposed to use Web Intents as a service discovery mechanism for
sensors and that a generic sensor API will be layered on top of Web
Intents. This work has not yet progressed in W3C so far but it is
important that webinos get involved as well.

### Demos[¶](#Demos)

-   Google's examples and demos at webintents.org:
    <http://examples.webintents.org/> and <http://demos.webintents.org/>
-   Sony Mobile simple Web Intents image picker demo: [SoMC Web Intents
    image picker
    demo](http://dl.dropbox.com/u/30360043/Web%20Intents%20File%20Picker%20V16/index.html)
-   Sony Mobile demo video on Web Intents for local service (UPnP)
    discovery. Use case is "select remote device for to play video and
    control playback". "Video of demo [Play video on remote device using
    Web
    Intents](https://docs.google.com/file/d/0B-2pb_m94nPxRGV5LTRvM0pLaUU/edit)

### Summary of links on Web Intents:[¶](#Summary-of-links-on-Web-Intents)

-   [W3C Web Intents specification](http://www.w3.org/TR/web-intents/)
-   [W3C Web Intents Addendum - Local
    Services](http://w3c-test.org/dap/wi-addendum-local-services/)
-   [Google Web Intents use cases, examples,
    etc](http://webintents.org/)
-   [W3C Web Intents wiki](http://www.w3.org/wiki/WebIntents)
-   [W3C Public W3C Web Intents maling list
    archive](http://lists.w3.org/Archives/Public/public-web-intents/)
-   [W3C wiki WebIntents/SonyMobile - Local Network Service
    Discovery](http://www.w3.org/wiki/WebIntents/SonyMobile_-_Local_Network_Service_Discovery)

Aligning webinos with Web Intents[¶](#Aligning-webinos-with-Web-Intents)
------------------------------------------------------------------------

### Goal[¶](#Goal)

The goal for aligning webinos with Web Intents is to allow web
application to discover and use standard Web Intents Services residing
"anywhere" in the cloud or in the local network as well as Web Intents
enabled webinos Services.

### Where does the User Agent Web Intents implementation reside?[¶](#Where-does-the-User-Agent-Web-Intents-implementation-reside)

Currently support for the Web Intents APIs are implemented in the
browser, either through a native implementation as in Chrome, or through
a JavaScript shim that is included in Client and Service web pages. The
list of registered Services is stored in local memory in the device in
which the browser is running. This model is not perfect for a
cross-device concept as webinos as user's should be able to register
Services that are accessible from the user's all devices.

A proposal has been raised by a webinos partner in W3C on separating a
Web Intents Agent (WIA) from the User Agent and allowing this WIA be
implemented in another entity than the browser, for example the PZP. The
thread starts here:
<http://lists.w3.org/Archives/Public/public-web-intents/2012Jun/0024.html>.

For webinos there are several possibilities, for example:\
1. Reuse the browsers native Web Intents implementation. Currently only
Google Chrome for desktop provides native support for Web Intents but it
is expected that other browsers will follow. This would mean that users
will experience a UI for webinos Web Intents Services that is consistent
with any other Web Intents Services but will limit the possibilities for
webinos to what is provided by the browser implementation and APIs.

2\. De-couple the Web Intents implementation from the browser or widget
runtime and create a webinos implementation of the "Web Intents Agent"
in the PZP. This would make webinos support for Web Intents independent
of browsers and widget engines used and also easier to provide a
repository of registered Web Intents Services that can be shared among
the different devices in a user's personal zone. This repository could
for example be located in the PZH. However, privacy issues, for example
the feature that Client and Service web applications are anonymous to
each other, must be considered.

3\. Implement support for Web Intents for webinos, or parts of Web
Intents, by using browser extension capabilities. The [Chrome socket API
extension](http://developer.chrome.com/trunk/apps/app_network.html)
could for example be used to implement support the Web Intents addendum
for local network services through the ability to get access to UDP.

### Registration of Webinos Web Intents Services[¶](#Registration-of-Webinos-Web-Intents-Services)

The W3C Web Intents specification defines Service registration markup
with the \<intent\> tag,
<http://www.w3.org/TR/web-intents/#registration-markup>. Web pages can
register themselves as Service handlers or other same-origin pages as
Service handlers. However, this Service registration method is currently
not implemented in Chrome. Instead Chrome Web Intents Services must be
registered in the Chrome manifest file manifest.json,
<http://developer.chrome.com/extensions/manifest.html#intents>.

There is also ongoing discussions on adding a JS API for registration
and unregistration.

In addition dynamic registration of Web Intents Services on locally
discovered UPnP and mDNS devices are specified in [Web Intents
Addendum - Local
Services](http://w3c-test.org/dap/wi-addendum-local-services/). Here a
"Web Intents document" retrieved from the discovered UPnP or mDNS device
contains the registration markup.

For webinos it seems reasonable to declare a Service to be Web Intents
enabled in the manifest file. This file could for example contain a link
to an html page that contains registration markup or JS for
registration. Compare with the "Web Intents document" for UPnP and mDNS
devices as described in the [W3C Web Intents Addendum - Local
Services](http://w3c-test.org/dap/wi-addendum-local-services/), section
4.1.3.

It should be considered if there should be two states in the
registration process:

1.  Discovered but unregistered Services are stated as “suggested
    Services” in the Web Intents Service picker.
2.  When the user explicitly has approved, in the Service picker, when
    configuring the system or in any other situation, to use a suggested
    Service it is moved to the list of “selectable Services”.

The Chrome Web Intents implementation works similar to above.

### Service invocation[¶](#Service-invocation)

When a web application invokes an Intent through startActivity () and
the Web Intents Service picker is visible in the User Agent the
suggested and selectable Services that are able to handle the Action and
Type of the Intent is displayed in the Service picker.

Invoking a webinos Web Intents Service is basically done in the same way
as for any other Web Intents Services the webinos access control
framework will control allow or deny access based on Client web
application origin, Service identity and policy settings.

### Interaction between webinos applications and webinos Web Intents Services[¶](#Interaction-between-webinos-applications-and-webinos-Web-Intents-Services)

The section [Web Intents based
APIs](/t3-4/wiki/Web_Intents_for_Webinos_investigation#Web-Intents-based-APIs)
describes the situation on Web Intents based APIs. So far W3C has only
specified RPC like Web Intents based APIs. However, use cases that
require a long lasting relation between the Client application and
Service are common. For example, running a web application that controls
video playback on a remote TV device or running a web application
continuously using data from sensors on a remote device. So we need:

1\. Specified high level protocols that run on top of an html message
channel running between the Client and Service web applications.

2\. The ability to run a Service application in the background, i.e.
hidden with no UI, as many use cases require that the UA continues to
show the Client Web Application after the Service has been selected.

For 1 one idea could be to facilitate for application developers by
creating JS libraries of simple methods on top of the message channel
protocol used to interact with the Service. This would make it possible
to reuse existing JS APIs and use them to access Services selected
through Web Intents. For example, the user has a Web Intents enabled
UPnP device, providing a remote video view Service, The Client web
application communicates with the Service handler page through a high
level “video view” protocol (“Play”, “Stop”, “Pause”, “Resume”, etc). A
JS library could then be included by the Client web application and this
library could have JS methods for Play”, “Stop”, “Pause”, “Resume”, etc.

For 2 the [W3C Web Intents
specification](http://www.w3.org/TR/web-intents/) does currently not
allow "hidden" Services. Only Service disposition with a new browser
window or disposition inline the Service picker is allowed. Google's
motivation for not allowing disposition "hidden" is that running
Services in the background with no UI would be a security issue.
However, there is an action on Sony to propose how disposition "hidden"
could be provided in a secure manner.

### Security and privacy comparison[¶](#Security-and-privacy-comparison)

The existing webinos discovery API and Web Intents have different
security and privacy models which would need to be aligned more closely.
Web Intents define the following access control points:

-   *Registration* - The decision to register an intent service as
    'selectable'.
-   *User consent* - The user's consent is granted when they make the
    decision to select a particular intent service at runtime.
-   *Authenticating users and services* - The standard web model is
    followed. An intent service may require user authentication and
    services may be offered through HTTPS sessions.

In comparison, the webinos discovery system relies on:

-   *Registration* - Each device offering a service must be explicitly
    connected to a personal zone before it can be accessed. This is
    either through enrolment (when adding a new device belonging to the
    user) or through certificate exchange (when connecting to a device
    outside the personal zone).
-   *User consent* - The policy system is used to authorise application
    installation and api invocation. Policies can be set when an
    application is installed or can be modified subsequently. Policies
    can change based on the user's environment, such as whether they are
    roaming or on a local wifi network. A policy might require user
    consent once, every time or never.
-   *Authenticating users and services* - The personal zone overlay
    network is relied upon to mutually authenticate services to users.

These are similar but with key differences. Firstly, registration in
webinos is a more time-consuming process and is most suited to creating
personal networks rather than registering arbitrary services. This
allows authentication to be mutual and (arguably) stronger, but imposes
a higher overhead. Secondly, the consent model in webinos is more
flexible but also more complicated. Thirdly, In Web Intents, the consent
process is combined with a service selection process, which could be
considered an advantage in usability. However, this fails to satisfy use
cases where the application needs to maintain some control over the
services selected (e.g., specifying that they all belong to the same
device) or where the application wants to save the user's choice of
service provider. Finally, the discovery approach in webinos is
currently vulnerable to *fingerprinting* attacks, allowing users to be
tracked between different web applications. Web Intents, in comparison,
are potentially more privacy-preserving as they explicitly don't allow
the enumeration of potential intent service providers.

To align the two models would require the following changes:

-   webinos would need to have altered policy settings which referred to
    the intent service selection process. E.g., a policy would need to
    answer the question: can application X invoke the 'share' intent? In
    this case, the possible policy settings might be:
    -   "yes, show intent selection prompt each time",
    -   "yes, show intent selection prompt the first time",
    -   "yes, always use intent provider Y"
    -   "no"
-   These settings would not make webinos incompatible with web intents,
    and would *still* support flexible use-cases based on user
    environment information.
-   webinos would either need to stop supporting applications which
    require visibility of all services available in a personal zone, or
    support both web intents *and* the discovery API. These would need
    to be made compatible at the API level.
-   webinos services are generally more trusted than arbitrary intent
    service providers. They are hosted on known devices and are likely
    to store data in well-known places. They use a standard
    authentication process which is arguably more trustworthy.
    Furthermore, the privacy implications of using a service provided by
    a personal zone device are likely to be understood. Online web
    intent services, on the other hand, may authenticate users
    differently (or not at all) and may provide no transport security.
    As such, presenting both webinos services and web intent services to
    the user as equal options during intent service selection might be
    misleading. Work would need to be done to identify the best way of
    presenting personal zone services and web services differently to
    users.

### Web Intents versus webinos AppLauncher API[¶](#Web-Intents-versus-webinos-AppLauncher-API)

A question was raised whether Web Intents could be used as an
application launcher mechanism.

The general answer is yes in the context of one web application
launching another web application of a certain type. However, comparing
with the [webinos AppLauncher
module](http://dev.webinos.org/specifications/draft/launcher.html) there
are signficant differences.

webinos AppLauncher module:

-   Provides two methods:
    -   Launch a webinos application that is installed on the same
        device. The application to launch can be either webinos native
        or an installed webinos application and is identified by a
        unique application identity.
    -   Check if a webinos application, identified by a unique
        application identity, is installed on the device.
-   The operation of the API is guided by application execution
    policies, which can be modified by user.

Web Intents:

-   Allows a web application to launch another "Service" web application
    identified by the action the Service performs and a type. For
    example pick an image (action="Pick", type="image/\*") or view a
    video (action="View", type="video/\*"). The User Agent allows the
    user to choose the Service application to use among a list of
    registered Services that are capable of handling this action and
    type. There is also a possibility for a Client application to point
    out a unique Service web application that should be launched, see
    [Explicit
    Intents](http://dvcs.w3.org/hg/web-intents/raw-file/tip/spec/Overview.html#explicit-intents).
-   The Service executing the Intent does not have to be installed in
    the device, it can reside anywhere.
-   The Client web application requesting the action to be performed and
    the executing Service web application are annonymous to each other
    if not an explicit Service is stated when the Client invokes the
    Intent.
-   The security model is based on user consent when selecting a Service
    to use for the requested Action. Operation is not guided by any
    pre-configured application execution policies. However, a Web
    Intents enabled Service can of course implement any standard web
    security mechanisms as needed, e.g.login with user credentials or
    transport layer security.
-   There is currently no explicit method to check the availability of a
    certain Service application and expose this information to the
    requesting Client web application (and I don't think it should due
    to privacy/fingerprinting reasons). However, the specification opens
    up for applications to provide a user controlled check of registered
    Services. According to the Web Intents specification, section 4, 2nd
    paragrah:

> The User Agent must not allow web pages the ability to discover
> passively which services the user has configured to handle particular
> intents, or any intents, whether by enumeration or exact query. There
> may be mechanisms for the user to actively grant this information to
> web pages, but it must not be made available passively.

So, it should be possible to provide a method, that is governed by
webinos security policies, to check registered Web Intents Services.

The conclusion is that Web Intents is a more general concept than
webinos application launching but it should be possible to use Web
Intents as an application launcher mechanism in the webinos context.

