Web Intents for Webinos[¶](#Web-Intents-for-Webinos)
====================================================

-   [Web Intents for Webinos](#Web-Intents-for-Webinos)
    -   [Minutes of meetings](#Minutes-of-meetings)
    -   [Web Intents introduction](#Web-Intents-introduction)
    -   [Why take Web Intents into
        Webinos?](#Why-take-Web-Intents-into-Webinos)
    -   [Why not take Web Intents into
        Webinos?](#Why-not-take-Web-Intents-into-Webinos)
    -   [Options](#Options)
    -   [Issues](#Issues)
        -   [Web Intents versus Webinos Security
            model](#Web-Intents-versus-Webinos-Security-model)
        -   [De-coupling Service registration from the browser - Service
            registration in
            PZP/PZH](#De-coupling-Service-registration-from-the-browser-Service-registration-in-PZPPZH)
        -   [Web Intents based APIs](#Web-Intents-based-APIs)
        -   [Web Intents versus Webinos AppLauncher
            API](#Web-Intents-versus-Webinos-AppLauncher-API)

Notes:

-   The result of this investigation in the task 3.4 delivery is here.
    [Task 3.4 delivery Web Intents investigation
    result](/t3-4/wiki/Web_Intents_for_Webinos_investigation)

<!-- -->

-   Most recent information on standardization status of Web Intents is
    at teh task 8.1 wiki. See [Web Intents
    standardization](/wp8-1/wiki/Web_Intents)

Minutes of meetings[¶](#Minutes-of-meetings)
--------------------------------------------

[online meeting 2012-06-08](.html)\
[online meeting 2012-05-31](.html)

Web Intents introduction[¶](#Web-Intents-introduction)
------------------------------------------------------

Basic introduction to Web Intents is here:

-   Task 8.1 wiki page [Web
    Intents](/wp8-1/wiki/Web_Intents)
-   Web Intents presentation
    [Webinos-\_Introduction\_to\_Web\_Intents.pdf](http://dev.webinos.org/redmine/attachments/2118/Webinos-_Introduction_to_Web_Intents.pdf)

Why take Web Intents into Webinos?[¶](#Why-take-Web-Intents-into-Webinos)
-------------------------------------------------------------------------

-   Web Intents has strong momentum in W3C and the web community and is
    driven by Google.
-   Adapt to a standardized service discovery/application launcher
    mechanism for the web.
-   Will help Webinos to get more attention.
-   Will help Webinos to integrate with web applications run in the
    browser context (Web Intents may not be suited for installed web
    applications/widgets)

> > All, please review and provide more input and corrections

Why not take Web Intents into Webinos?[¶](#Why-not-take-Web-Intents-into-Webinos)
---------------------------------------------------------------------------------

-   Current browser centric model does not fit Webinos
-   Web Intents based APIs not yet available
-   Web Intents too much under Google control
-   Too much effort to switch to a Web Intents model

> > All, please review and provide more input and corrections

Options[¶](#Options)
--------------------

-   Don't care about Web Intents.
-   Keep the current Webinos service discovery API for installed Webinos
    applications but base Webinos in browser context on Web Intents.
-   Switch to a Web Intents model both for Webinos installed
    applications and for Webinos browser based aplications

> > All, please review and provide more input and corrections

Issues[¶](#Issues)
------------------

### Web Intents versus Webinos Security model[¶](#Web-Intents-versus-Webinos-Security-model)

See wiki by John Lyle: [Web Intents Security
Points](/t3-4/wiki/WebIntentsSecurityPoints)

### De-coupling Service registration from the browser - Service registration in PZP/PZH[¶](#De-coupling-Service-registration-from-the-browser-Service-registration-in-PZPPZH)

Jean-Claude has started a thread at the W3C Web Intents mailing list on
separating a Web Intents Agent (WIA) from the User Agent. This is
important for webinos use of Web Intents. The thread starts here:
<http://lists.w3.org/Archives/Public/public-web-intents/2012Jun/0024.html>.

The problem with the currently specified model is that it centered
around the browser that the user currently is using. Please see the
e-mail thread for more details.

If Webinos project decides to use Web Intents we can address this issue
in two steps:

1.  De-couple Service registration from the specific user agent, i.e.
    provide a repository of registered Web Intents Services that can be
    shared among the different devices in a user's personal zone. This
    repository could for example be located in the PZH.
2.  Full replacement of "Web Intents enabled User Agent" with "Web
    Intents Agent de-coupled from the User Agent".

### Web Intents based APIs[¶](#Web-Intents-based-APIs)

Some Web Intents use cases are 'fire and forget' and some use cases
require a longer lasting relation between the Client application and the
Service application.

-   "Fire ad Forget": Client sends payload data to the Service with
    intents attributes and Service returns data with the intents
    invocation method callback function.

<!-- -->

-   "Message channel": Web Intents allows a longer lasting relation
    between the Client and the Service by an HTML message channel. On
    top of this message channel a high level protocols can run.

Both the 'fire and forget' and the "Message channel" cases requires
standardized APIs.

One advantage with the Webinos Service Discovery API is that standard or
Webinos APIs are used to interact with the discovered and selected
Service.

For Web Intents there is much to be done in defining the interaction
patterns/APIs/protocols to use between Clients and Services. So far we
have (to a great extend inconsistent with each other) descriptions at:

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

<!-- -->

-   [Pick Media
    Intent](http://w3c-test.org/dap/gallery/ "Web Intents based Gallery API")

<!-- -->

-   [Pick Contacts
    Intent](http://w3c-test.org/dap/contacts/ "Web Intents based Contacts API")

For an example of the case when a message channel between the Client and
Service pages is used to run a high level protocol see slide 18 in the
presentation [W3C Web Intents - Local Network Service
Discovery](http://www.w3.org/wiki/images/2/2e/V4_W3C_Web_Intents_-_Local_UPnP_Service_Discovery.pdf).
Here a high level "TV Control Protocol", independent of low level
communication (for example UPnP) method and details, is used by the
Client web application.

### Web Intents versus Webinos AppLauncher API[¶](#Web-Intents-versus-Webinos-AppLauncher-API)

A question was raised whether Web Intents could be used as an
application launcher mechanism.

The general answer is yes in the context of one web application
launching another web application of a certain type. However, comparing
with the [Webinos AppLauncher
module](http://dev.webinos.org/specifications/draft/launcher.html) there
are signficant differences.

Webinos AppLauncher module:

-   Provides two methods:
    -   Launch a Webinos application that is installed on the same
        device. The application to launch can be either Webinos native
        or an installed Webinos application and is identified by a
        unique application identity.
    -   Check if a Webinos application, identified by a unique
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
Webinos security policies, to check registered Web Intents Services.

The conclusion is that Web Intents is a more general concept than
Webinos application launching but it should be possible to use Web
Intents as an application launcher mechanism in the webinos context.

