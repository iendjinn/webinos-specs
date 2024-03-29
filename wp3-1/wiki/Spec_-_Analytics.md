Spec - Analytics[¶](#Spec-Analytics)
====================================

Authors: Hans Myrhaug, Dr Ayse Goker, AmbieSense Ltd

The objectives of webinos analytics[¶](#The-objectives-of-webinos-analytics)
----------------------------------------------------------------------------

The objective of webinos analytics is to help application developers
provide and learn more about the application and its users. It is
designed for application developers that would like to outsource the
analytics task to gain more focus and time to develop the application.
Webinos analytics is the process of aggregating reports from application
sessions that users have with the applications. Gathering metrics is the
process of gathering and making information about the individual
application sessions available for the analytics. Conducting metrics is
therefore the enabler for providing analytics. Webinos applications must
be equipped with webinos metrics components as means to enable the
aggregation of webinos analytics. Thus, analytics is the process of
aggregating data from the captured metrics data, and performing the
analytics on top of the metrics can be seen as a specialised application
process.

How does the webinos metrics and analytics work for the application
developer and the users? There are many ways one can perform analytics
and subsequently many architectures that could be implemented for
providing metrics and analytics. For webinos applications, the metric
data can either be conducted within the local application on the client
side, or alternatively remotely in conjunction to the web site that the
applications on the devices communicate with. Webinos offers two
different ways to collect the metrics data: within the application on
the user device, or remotely on the web site that the application
communicates with.

Conducting webinos metrics is quite straight forward. The overall user
scenario to keep in mind is:

1.  The user interacts with the application on her device, such as
    requesting for some content on the web
2.  The application uses some webinos metrics software - either
    on-device, or on the web
3.  The webinos metrics software collects metrics data about how the
    application is used
4.  The gathered metrics data is securely sent/uploaded to the analytics
    service
5.  The analytics service gathers and analyses the metrics data for the
    application developer
6.  The application developer logs on to the analytics service to see
    and learn about the application and its users

How to integrate webinos analytics with the application[¶](#How-to-integrate-webinos-analytics-with-the-application)
--------------------------------------------------------------------------------------------------------------------

Webinos applications can run across multiple devices and web servers.
Much of the communication in a web application is via the Hypertext
Transfer Protocol (HTTP). The HTTP-protocol is regarded as stateless,
because there is no notion of state preserved by the protocol itself.
Webinos applications are however not stateless, because the user has to
interact with and go through various stages to interact with the
application. Any notion of state has therefore to be explicitly gathered
and stored somewhere by the web application. This can either happen on
the device or on the web site in a webinos application.

The application on the user device sends HTTP-requests to web sites for
content, and as part of these web request, it has to provide sufficient
context information for the web site to compose and provide the correct
response.

The chosen implementation strategy for the webinos analytics is to
provide a suite of metrics components that together can cater for the
needs of a wide range of web application architectures in need for
outsourcing to webinos analytics. For example, it could be an offline
application running locally on the device, that connects to the web
perhaps once per month, or it could be a web application where several
thousand HTML requests and responses travel between the client and
various web servers. By addressing both of these, we believe we will
able to address most needs for metrics and analytics in web
applications, because one can choose to gather the metrics data in the
application instance running on the users’ device, and one could also
want to perform some analytics work as light weight workers on the web
server side. The work balance for metrics gathering can therefore be
shifted towards the online web servers or more towards the client
application on the device depending on the analytics requirements of the
application.

An important aspect for webinos analytics components is for users and
application developers to be able to trust them. Providing for analytics
across applications therefore means catering for privacy. It is in
general possible to monitor individual interaction with application, but
also to aggregate statistics for a set of users. Most analytics
approaches today provide aggregated statistics for all users using the
web application/ web servers. However, if one places some metrics on the
local device, then one can achieve very accurate and also individual
statistics. This could be used for an application to provide smarter,
and more personalised information experiences. Note however that
individual statistics about a user always is personal and sensitive data
above all. Storing and using such data requires permission/ consent from
the user.

The scope of the webinos metrics components is to be a solution for
application developers to be able to plug in and start using webinos
analytics.

As with web applications, webinos applications can be built in the
following ways:

1.  Client-side application
2.  Client-side and server-side application
3.  Server-side application

The communication between the client and the server will normally be
using the hypertext transfer protocol.

Unlike static websites, webinos applications offer a richer experience
which can be more integrated with mobile devices, tablets, car
infotainment, and laptops. The webinos applications will be able to more
context information than previously possible in web applications. It can
can capture metrics data about access location, motion, camera, local
sensors, networks, near-field communication and so on. The webinos
applications will have different session models and, as mentioned will
also enable offline use. This means that the scope of collecting metrics
in the webinos platform is two-fold:

-   To enable the gathering of metrics data through the use of the
    context API
-   To enable the gathering of metrics data pertinent to HTTP-requests
    and responses; including context information around these

Conceptual Architecture[¶](#Conceptual-Architecture)
----------------------------------------------------

Reading this will help webinos application developers understand the
conceptual level of integrating the application with webinos metrics
components. An application developer integrates in the same way on any
webinos enabled device. This makes it easy to develop and it obtains
efficient development, allowing application developers to focus on what
the application should do instead of what marketing managers would like
to know.

It takes only some minutes to read through this guide to the conceptual
architecture, and afterwards you will be able to spend only a few hours
to plan what you would like to conduct metrics on, and then you
integrate this with your application. It is possible to only read the
metrics API specifications to be able to integrate. However, we
recommend for every application developer to spend some time to read
through this conceptual document in order to know the possibilities
before starting to integrate with webinos metrics.

As mentioned, this documentation is independent of the target device
that your application will be/ or is running on.

Overall system concepts[¶](#Overall-system-concepts)
----------------------------------------------------

Here is some of the core overall system concepts and vocabulary that
application developers will need to be aware of when we discuss webinos
analytics:

### Webinos application sessions[¶](#Webinos-application-sessions)

A webinos application session starts when an application instance
starts, and ends when the application instance stops. Each session is
uniquely identifiable for your application. Throughout the session there
are will be certain points and events that you will be interested in
gathering metrics about and analysing.

### Webinos metrics data and metric points[¶](#Webinos-metrics-data-and-metric-points)

The metrics are chunks of data that you are interested in gathering.
This can be about the user context, the device context, the application
context, specific events that occur, or contextual information about
HTTP-requests and their responses, in your application where you would
like to conduct data and metrics. Thus, metrics is context information
that captures important aspects of the user, application, and the
device. The metric points are the places in your application that you
would like the metrics to be conducted.

### Webinos metrics events[¶](#Webinos-metrics-events)

A metrics event is created by you at the every chosen metrics point in
the application. An interesting event occurs in the application and you
as an application developer decide that it is important to log this
event. A metrics event contains metrics data. Here are some examples of
metrics data that application developers might want to log:

-   The user opens a particular view or page
-   The user changes her profile
-   The user is using different devices
-   The user earns more loyalty points
-   The user checks out and pays for products
-   The user arrives at a new destination
-   The user changes the privacy policy
-   The application presents an advertisement
-   The user sends a new HTTP request
-   The application receives a HTTP response
-   The application crashes
-   The device goes off-line
-   The device goes online
-   The battery status of the device is low
-   The application is upgraded
-   The user has changed to another device
-   The user specifies some interests
-   The user queries for some information to a search facility
-   The application starts
-   The application stops
-   The user chats with another user
-   The application sends data to another application
-   The cookie(s) in the web application are changing

### Webinos metrics workers[¶](#Webinos-metrics-workers)

Metrics can be conducted either locally on the user device or remotely
on web servers. In both cases there are metrics worker threads/
processes that perform the metrics separately in the background. This
enables both heavy- and light-weight metrics tasks to be executed
without affecting the user interface behaviour or any other
communication activities such as web requests and responses. The overall
idea is to conduct webinos metrics as a background task preferably on
the user device, and alternatively on the web server side. In webinos,
we therefore propose two metrics types of metrics workers:

-   **Application metrics workers** - integrated with the local
    application on the device
-   **Server metrics workers** - integrated at the front-tier of remote
    web servers

A web site can be standalone of distributed across several web servers.
In the latter case, information from the metrics events occurring in the
client application will be needed to glue together web logs on the
server side. It is difficult to uniquely identify application sessions
on the website side. Logging the webinos metrics event on the client
side is therefore the recommended route, however, sometimes this will
lead to too much metrics and the marketing manager might instead want
you to monitor what is going on the web server side and not bother too
much about what happens on the client application.

An e-commerce web site might consist of a product offering server, an
advertisement server, and a separate payment service provider. In this
case it will be difficult to know what is going on in the application
session, because the dynamically generated web pages from the domain
name result in a response that is build from subsequent requests to the
other web servers in the background.

Webinos server side deals with this problem by offering webinos metrics
workers for the web server. These components are geared towards web
sites that consist of several web servers, and when there is a need for
metrics on the sever-side to be able to act in the metrics data in the
situation between a web request and its response from the web site.

### Application metrics logs and server metrics logs[¶](#Application-metrics-logs-and-server-metrics-logs)

Webinos metrics workers collects and adds metrics data and add them to
the metrics logs. A webinos metrics log is either stored locally on a
device or remotely on for instance a web server. Metrics logs located on
the user device are called application metrics logs, and server metrics
logs created by a worker thread/ process on a remote web server, are
referred to as server metrics logs. Both types of metrics logs are
created by the webinos metrics workers which are either running locally
on the user device, or remotely hooked up and integrated in the
front-tier of the web site/ web farm.

Technical Use Cases[¶](#Technical-Use-Cases)
--------------------------------------------

### Use case I: Integration with application metrics workers[¶](#Use-case-I-Integration-with-application-metrics-workers)

1.  Register your webinos application client
2.  Create a private webinos analytics key unique for the application
    upon the completion of the registration process
3.  Download and install the application metrics library for client-side
    applications
4.  Use the policy manager to register your intent for using the
    application metrics library
5.  Use the context manager to obtain access to context information
    about the user, the device, or the application context. You can
    create and/ or use context information that is private for your
    application.
6.  Add metric points for startSession(), pauseSession(),
    resumeSession(), uploadSession(), and closeSession().
7.  Create metrics events to record specific metrics data, and add the
    relevant context information to these events as arguments to the
    metrics event.
8.  Test and evaluate the integration by running the application on a
    device
9.  Log in to your webinos analytics page to see how the metrics data is
    being presented.

### Use case II: Integration with server metrics workers[¶](#Use-case-II-Integration-with-server-metrics-workers)

1.  Register your application web site
2.  Create a private webinos analytics key unique for the web site upon
    the completion of the registration process
3.  Download and install the server metrics library from webinos for
    webinos-enabled web sites
4.  Use the policy manager to register your web server's intent for
    using the server metrics library
5.  Use the context manager to obtain access to context information
    about the user, the device, or the application context whenever web
    requests occur.
6.  Create metrics events to record specific web requests and responses,
    and add the relevant context information to these events as
    arguments to the metrics event.
7.  Test and evaluate the integration by running the web site
8.  Log in to your webinos analytics page to see how the metrics data is
    presented.

Formal Specification[¶](#Formal-Specification)
----------------------------------------------

### Reference architecture for application metrics workers[¶](#Reference-architecture-for-application-metrics-workers)

The following diagram shows the reference architecture for when an
application developer chooses to implement Use Case I above. The
advantage of following this approach is that one can very accurately
monitor and capture the application session for each individual
application on the device. It ensures a high quality of the gathered
metrics data, because the application on the user device is in full
control over the interaction states that the user is going through. The
general principle is that each application can monitor the local metrics
data and events as and when these happen on the device. Moving the
webinos metrics intelligence towards the application client can also
significantly reduce the computational resources needed for the webinos
analytics service to effectively aggregate analytics data from the
metrics data of the individual application sessions.

The application registers its intent to use the application metrics
library. It also does the same for the context API. If the webinos
runtime allows this, the application will be writing metrics data to the
local application metrics log when it encounters the metrics points in
the application. The application developer is able to consume the
context information provided by any context provider on the device -
provided that the policy manager permits. Such context information
originating from other context providers in the system is captured and
added to the application metrics log. Examples of such context
information is location, nearby devices, wireless networks, and so on.
Furthermore, context information about the application, such as when it
started, paused, resumed, stopped, and ended can be logged. Finally,
metrics data about web requests can be added to the log by the
application metrics worker - again only if the policy manager permits.
Thus, any context information sourced by a context provider on the
end-user device, including also context information about web requests
and responses, can instantly be logged by the application metrics
workers.

![ digraph G { node [shape=box, fillcolor=lightgray, style="filled,
rounded"] {rank = below; "Application"; "Context API"; } {rank = below;
"Application"; "Application metrics worker"; } {rank = left;
"Application"; "Web site"; } {rank = below; "Webinos analytics";
"Application metrics log"; } "Application" -\> "Context API"
[label="Uses"] "Application" -\> "Application metrics worker"
[label="Uses"] "Application" -\> "Web site" [label="Communicates with",
dir=both] "Application metrics worker" -\> "Application metrics log"
[label="Metrics data"] "Webinos analytics" -\> "Application metrics log"
[label="Aggregates data from"] }
](/redmine/wiki_external_filter/filter?index=0&macro=graphviz&name=c4849065ddabd704e5f742deb783ed70825984ec72346ef99b3fd365d13d48a1)
![ digraph G { node [shape=box, fillcolor=lightgray, style="filled,
rounded"] {rank = below; "Application"; "Context API"; } {rank = below;
"Application"; "Application metrics worker"; } {rank = left;
"Application"; "Web site"; } {rank = below; "Webinos analytics";
"Application metrics log"; } "Application" -\> "Context API"
[label="Uses"] "Application" -\> "Application metrics worker"
[label="Uses"] "Application" -\> "Web site" [label="Communicates with",
dir=both] "Application metrics worker" -\> "Application metrics log"
[label="Metrics data"] "Webinos analytics" -\> "Application metrics log"
[label="Aggregates data from"] }
](/redmine/wiki_external_filter/filter?index=1&macro=graphviz&name=c4849065ddabd704e5f742deb783ed70825984ec72346ef99b3fd365d13d48a1)

The webinos analytics receives the application metrics log from a
background task that is running on the user device. The application
session is easy to maintain locally, because there is only one session.
The application maintains its own state, and the application developer
can choose to gather and add whatever context information believed to be
needed for the analytics. Capturing context information about web
requests is also straight forward. The application developer makes use
of the context API to capture and manage the web context attributes
whenever the application is requesting for information from remote web
servers. The aggregation of analytics from the logged metrics data,
becomes an easy task, because all of the captured metrics data is
uniquely related to the application sessions at hand, and well defined
context providers on the user device - such as for example various
sensors.

Note that webinos-enabled applications using the webinos metrics library
need to flag the intent to use the API. This means that it is possible
for the webinos runtime, and the individual users, to switch off all or
some of the gathered metrics data at any time. We believe that this will
create more trust and transparency for the users compared to the
existing approach of for instance Google analytics, which is: "don't
tell the user about what is being metered, and don't let them switch it
off either".

Thus, both from the local metrics and privacy point of views, webinos
analytics certainly makes progress in favour of users compared to
existing analytics solutions for the web. Moreover, from the application
developer's point of view, it is possible to gather richer metrics data,
because the application metrics worker is working locally within the
context of each application session.

### Reference architecture for server metrics workers[¶](#Reference-architecture-for-server-metrics-workers)

This next diagram exhibits the reference architecture for when an
application developer chooses to implement Use Case II above. The
advantage of this approach is that the metering capability is added to
the front-end of the web site. This is a less intrusive approach,
because the metrics worker is integrated on the web server instead of
within the client application. This approach is also capable of
capturing metrics data about individual application sessions. The
difficulty, however, is in being able to keep track of the application
session and state when interacting with the web site. In general, this
is regarded as more difficult to do this on the web server side, because
the amount of context information that can be captured other than those
directly related to the web requests and responses is reduced due to the
stateless nature of the HTTP protocol, and also because there can be
many sessions from different applications instances to serve at the same
time. However, it ensures that the client application code does not have
to be altered to achieve the metrics data, because the server metrics
worker is responsible for capturing states that the user is going
through. The general principle is that each web site gathers the metrics
data of individual application sessions as and when these events happen.
Moving the metrics intelligence towards the server side however does
increase the computational resources needed for the webinos analytics
service to aggregate quality data the from the metrics. The metrics
points would not always correlate with the points of web requests, and
similarly it sometimes would also be artificial to send web requests to
a web server just because a metrics point in the client application was
reached. Such situations create overhead for the webinos analytics in
terms of aggregating analytics data.

![ digraph G { node [shape=box, fillcolor=lightgray, style="filled,
rounded"] {rank = below; "Application"; "Server metrics worker"; } {rank
= left; "Application"; "Web site"; } {rank = below; "Webinos analytics";
"Server metrics log"; } "Application" -\> "Server metrics worker"
[label="Implicitly uses"] "Application" -\> "Web site"
[label="Communicates with", dir=both] "Server metrics worker" -\> "Web
site" [label="Works at the front end of"] "Server metrics worker" -\>
"Server metrics log" [label="Metrics data"] "Webinos analytics" -\>
"Server metrics log" [label="Aggregates data from"] }
](/redmine/wiki_external_filter/filter?index=0&macro=graphviz&name=67e022107f4b4853d5e61fa93ce72740d71f0dacf48de4164e9f39b266d38a6c)
![ digraph G { node [shape=box, fillcolor=lightgray, style="filled,
rounded"] {rank = below; "Application"; "Server metrics worker"; } {rank
= left; "Application"; "Web site"; } {rank = below; "Webinos analytics";
"Server metrics log"; } "Application" -\> "Server metrics worker"
[label="Implicitly uses"] "Application" -\> "Web site"
[label="Communicates with", dir=both] "Server metrics worker" -\> "Web
site" [label="Works at the front end of"] "Server metrics worker" -\>
"Server metrics log" [label="Metrics data"] "Webinos analytics" -\>
"Server metrics log" [label="Aggregates data from"] }
](/redmine/wiki_external_filter/filter?index=1&macro=graphviz&name=67e022107f4b4853d5e61fa93ce72740d71f0dacf48de4164e9f39b266d38a6c)

The server metrics workers use the context information available on the
web server in conjunction with web requests and responses to capture and
elicit metrics data. A web request starts inside the client application
on the device when the user clicks a web link, or formulates the request
via some other means. The request lasts until the local application has
retrieved, parsed, and rendered the response to the user. During the
response period, the web site performs a variety of subsequent
activities often starting with sending cookies to the local application
at first, before proceeding to respond with subsequent content that in
return can lead to subsequent requests for other content such as more
html text, scripts, multimedia, and images. In a webinos-enabled
application that works by performing many web requests and responses
during the application session, it can be natural to conduct metrics on
the contextual information pertaining to web requests and responses.

Web servers in general have a set of environment variables that together
define the context of the web server for each connection, including web
requests and responses. Some of these variables are web server specific,
whereas the majority of them are web request specific. One can obtain a
list of these variables on the web server. Server metrics workers have
access to these environment variables and uses a cookie framework to
keep track of individual application sessions. Although, it is in
principle possible to extend the set of context information available on
the web server side, we believe this approach to be more limited
compared to gathering metrics data from within the actual application
instance residing on the user device. For more on available environment
variables (i.e. contexts information), see
<http://en.wikipedia.org/wiki/Common_Gateway_Interface#History>

Note that from the end user's point of view, this use case is less
intrusive, gathers less context information, but is more difficult to
control because the server metrics worker is not deployed on the user
device.

### UML components analysis[¶](#UML-components-analysis)

Detail the specifics of the individual components required, using UML
and accompanying prose.

### UML sequence diagrams for application metrics workers[¶](#UML-sequence-diagrams-for-application-metrics-workers)

This section presents sequence diagrams that involve application metrics
workers on the user device. These are:

-   Register the intent to use the application metrics worker
-   Gathering metrics data about the application session lifecycle
-   Register the intent to consume specific context information
-   Using context information from specific context providers as metrics
    data
-   Adding web requests and responses as metrics data
-   Encountering metrics points within the application
-   Uploading the metrics data to webinos analytics

#### Register the intent to use the application metrics worker[¶](#Register-the-intent-to-use-the-application-metrics-worker)

<div class="uml">actor User
autonumber
User -> Application: Starts application
Application -> Application : onRegisterMetrics called
Application -> ApplicationMetricsWorker : Register intent to use application metrics using key
ApplicationMetricsWorker --> Application : A metrics worker instance is returned, if permitted

User -> Application: Interacts with
Application -> Application: onUnregisterMetrics
Application -> ApplicationMetricsWorker: unRegister called
ApplicationMetricsWorker -> WebinosAnalytics: Close web connection
WebinosAnalytics --> ApplicationMetricsWorker: Close web connection
ApplicationMetricsWorker --> Application: Application metrics unregistered</div>

#### Gathering metrics data about the application session lifecycle[¶](#Gathering-metrics-data-about-the-application-session-lifecycle)

<div class="uml">actor User
autonumber

User -> Application: Starts application
Application -> Application: onStart called
Application -> ApplicationMetricsWorker: startSession(MetricsDataEvent) called
ApplicationMetricsWorker -> ApplicationMetricsLog: Add MetricsDataEvent
ApplicationMetricsLog --> ApplicationMetricsWorker: Metrics data event added
ApplicationMetricsWorker --> Application: Application session started

User -> Application: Pauses application
Application -> Application: onPause called
Application -> ApplicationMetricsWorker: pauseSession(MetricsDataEvent) called
ApplicationMetricsWorker -> ApplicationMetricsLog: Add MetricsDataEvent
ApplicationMetricsLog --> ApplicationMetricsWorker: Metrics data event added
ApplicationMetricsWorker --> Application: Application session paused

User -> Application: Resumes application
Application -> Application: onResume called
Application -> ApplicationMetricsWorker: resumeSession(MetricsDataEvent) called
ApplicationMetricsWorker -> ApplicationMetricsLog: Add MetricsDataEvent
ApplicationMetricsLog --> ApplicationMetricsWorker: Metrics data event added
ApplicationMetricsWorker --> Application: Application session resumed

User -> Application: Closes application
Application -> Application: onClose called
Application -> ApplicationMetricsWorker: closeSession(MetricsDataEvent) called
ApplicationMetricsWorker -> ApplicationMetricsLog: Add MetricsDataEvent
ApplicationMetricsLog --> ApplicationMetricsWorker: Metrics data event added
ApplicationMetricsWorker --> Application: Application session closed
Application -> Application: Application closed</div>

#### Register the intent to consume specific context information[¶](#Register-the-intent-to-consume-specific-context-information)

<div class="uml">actor User
autonumber
User -> Application: Starts application
Application -> Application : onRegisterContextMetrics called
Application -> ContextManager : Register intent for metering specific context information
ContextManager -> ContextManager: Authenticate 
ContextManager -> ContextManager: addContextEventListener
ContextManager --> Application : Context permissions object returned, if permitted
ContextManager --> ApplicationMetricsWorker: onContextEvent called
ApplicationMetricsWorker -> ApplicationMetricsLog: Add MetricsDataEvent
ApplicationMetricsLog --> ApplicationMetricsWorker: Metrics data event added
ApplicationMetricsWorker --> Application: Context information added</div>

#### Using context information from specific context providers as metrics data[¶](#Using-context-information-from-specific-context-providers-as-metrics-data)

<div class="uml">actor User
autonumber
User -> Application: Starts application
Application -> Application : onRegisterContextMetrics called
Application -> ContextManager : Register intent for using a specific context provider
ContextManager -> ContextProvider: Request for authentication
ContextProvider -> ContextProvider: addContextEventListener
ContextProvider --> ContextManager: Authentication granted
ContextManager --> Application : Context permissions object returned, if permitted
ContextProvider --> ApplicationMetricsWorker: onContextEvent called
ApplicationMetricsWorker -> ApplicationMetricsLog: Add MetricsDataEvent
ApplicationMetricsLog --> ApplicationMetricsWorker: Metrics data event added
ApplicationMetricsWorker --> Application: Context information added</div>

#### Adding web requests and responses as metrics data[¶](#Adding-web-requests-and-responses-as-metrics-data)

<div class="uml">actor User
autonumber
User -> Application: Starts application
Application -> Application : onRegisterWebMetrics called
Application -> ContextManager : Register intent for metering web requests and responses
ContextManager -> ContextManager: Authenticate 
ContextManager -> ContextManager: addContextEventListener
ContextManager --> Application : Context permissions object returned, if permitted
User -> Application: Makes web request
Application -> WebSite: sends web request
Application -> ContextManager: Aggregate context information
ContextManager --> ApplicationMetricsWorker: onContextEvent called
ApplicationMetricsWorker -> ApplicationMetricsLog: Add MetricsDataEvent
ApplicationMetricsLog --> ApplicationMetricsWorker: Metrics data event added
ApplicationMetricsWorker --> Application: Context information added
WebSite --> Application: Replies with web response
Application --> User: Renders and presents the web response
Application -> ContextManager: Aggregate context information
ContextManager --> ApplicationMetricsWorker: onContextEvent called
ApplicationMetricsWorker -> ApplicationMetricsLog: Add MetricsDataEvent
ApplicationMetricsLog --> ApplicationMetricsWorker: Metrics data event added
ApplicationMetricsWorker --> Application: Context information added</div>

#### Encountering metrics points within the application[¶](#Encountering-metrics-points-within-the-application)

<div class="uml">actor User
autonumber
User -> Application: Starts application
Application -> Application : onRegisterContextMetrics called
Application -> ContextManager : Register intent for providing specific context information
ContextManager -> ContextManager: Authentication granted
ContextManager -> ContextManager: addContextEventListener
ContextManager --> Application : Context permissions object returned, if permitted
User -> Application: Interacts with
Application -> Application: Reaches a metrics point
Application -> ContextManager: Creates a context object
ContextManager --> Application: Context object is returned
Application -> Application: Set the context attributes
Application -> ContextManager: Add the new context
ContextManager --> ApplicationMetricsWorker: onContextEvent called
ApplicationMetricsWorker -> ApplicationMetricsLog: Add MetricsDataEvent
ApplicationMetricsLog --> ApplicationMetricsWorker: Metrics data event added
ApplicationMetricsWorker --> Application: Context information added</div>

#### Uploading the application metrics to webinos analytics[¶](#Uploading-the-application-metrics-to-webinos-analytics)

<div class="uml">actor User
autonumber
User -> Application: Starts application
Application -> Application: onStartUpload called
Application -> ApplicationMetricsWorker: startUpload() called
ApplicationMetricsWorker -> WebinosAnalytics: Request to sign in securely
WebinosAnalytics --> ApplicationMetricsWorker: A secure web connection is returned
ApplicationMetricsWorker -> WebinosAnalytics: Post application metrics data
WebinosAnalytics --> ApplicationMetricsWorker: A response code is returned
ApplicationMetricsWorker -> ApplicationMetricsWorker: Optionally, delete uploaded metrics data locally
ApplicationMetricsWorker -> ApplicationMetricsWorker: Optionally, post new application metrics data at regular intervals

User -> Application: Interacts with
Application -> Application: onStopUpload called
Application -> ApplicationMetricsWorker: stopUpload() called
ApplicationMetricsWorker --> Application: Uploading metrics data stopped
ApplicationMetricsWorker -> WebinosAnalytics: Optionally, close the secure web connection
WebinosAnalytics -> ApplicationMetricsWorker: Optionally, close the secure web connection
ApplicationMetricsWorker --> Application: Connection closed</div>

### Functional and non functional requirements[¶](#Functional-and-non-functional-requirements)

The following table shows the requirements related to the webinos
metrics/ analytics specification. They are from the requirements report
([Webinos-D22](/t3-5/wiki/Deliverable_References#Webinos-D22))
where they were ranked as first priority:

  ----------------------------------------------------------------------------------------------------------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Requirement no.**                                                                                                           **Description**
  [ID-USR-DT-02](/wp2-2/wiki/DeliverableVersionAll#ID-USR-DT-02)                         The webinos system must minimise exposure of personal individual identifiers or canonical identifiers of webinos entities.
  [ID-USR-OXFORD-34](/wp2-2/wiki/DeliverableVersionAll#ID-USR-OXFORD-34)                 It shall be possible to include device identity information in application session data.
  [PS-DEV-ambiesense-08](/wp2-2/wiki/DeliverableVersionAll#PS-DEV-ambiesense-08)         The webinos runtime environment shall support customised encryption of any data stream (independent of its data type or format).
  [PS-DEV-Oxford-89](/wp2-2/wiki/DeliverableVersionAll#PS-DEV-Oxford-89)                 A method must be provided to enable webinos applications to explain how collected sensitive data will be managed (e.g. company name, purpose description).
  [PS-DWP-ISMB-202](/wp2-2/wiki/DeliverableVersionAll#PS-DWP-ISMB-202)                   The webinos runtime must ensure that an application does not access device features, extensions and content other than those associated to it.
  [PS-DWP-VisionMobile-12](/wp2-2/wiki/DeliverableVersionAll#PS-DWP-VisionMobile-12)     webinos shall use user privacy preferences when granting/denying access to user private information.
  [LC-DEV-POLITO-001](/wp2-2/wiki/DeliverableVersionAll#LC-DEV-POLITO-001)               The removal of an application on a device must remove any personal data linked and specific to that application installed on the device.
  [CAP-DEV-ambiesense-052](/wp2-2/wiki/DeliverableVersionAll#CAP-DEV-ambiesense-052)     An application shall be able to run multiple threads within an application, so that the user interface does not temporarily stop/freeze for the user when the application is busy with downloading, uploading, or otherwise processing data.
  [CAP-DEV-FHG-200](/wp2-2/wiki/DeliverableVersionAll#CAP-DEV-FHG-200)                   The webinos runtime shall be able to run applications in the background.
  [CAP-DEV-SEMC-010](/wp2-2/wiki/DeliverableVersionAll#CAP-DEV-SEMC-010)                 webinos shall provide means for applications to access user's profile data.
  [CAP-DEV-SEMC-011](/wp2-2/wiki/DeliverableVersionAll#CAP-DEV-SEMC-011)                 webinos shall provide means for applications to access user's preference data.
  [CAP-DEV-SEMC-014](/wp2-2/wiki/DeliverableVersionAll#CAP-DEV-SEMC-014)                 webinos shall provide means for applications to read and write to local file storage.
  [CAP-DWP-VisionMobile-31](/wp2-2/wiki/DeliverableVersionAll#CAP-DWP-VisionMobile-31)   webinos runtime shall support a standardised way of collecting application analytics.
  [CAP-DWP-VisionMobile-32](/wp2-2/wiki/DeliverableVersionAll#CAP-DWP-VisionMobile-32)   webinos runtime shall support a standardised way of collecting application performance statistics and failures.
  [CAP-DWP-VisionMobile-33](/wp2-2/wiki/DeliverableVersionAll#CAP-DWP-VisionMobile-33)   webinos shall expose application analytics data to the application developer.
  [CAP-DWP-VisionMobile-34](/wp2-2/wiki/DeliverableVersionAll#CAP-DWP-VisionMobile-34)   webinos shall be able to expose the application performance data to the application developer.
  [TMS-DWP-NTUA-001](/wp2-2/wiki/DeliverableVersionAll#TMS-DWP-NTUA-001)                 The system must be capable to identify, store, retrieve, and communicate contextual information for an application executing on user's devices.
  [TMS-DWP-NTUA-003](/wp2-2/wiki/DeliverableVersionAll#TMS-DWP-NTUA-003)                 A webinos runtime must be able to identify and store contextual information for the present situation within which an application is executed.
  ----------------------------------------------------------------------------------------------------------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Protocol definitions[¶](#Protocol-definitions)

The protocols between the application, the webinos metrics workers, and
webinos analytics are inspired by the emerging [W3C standard for Web
Workers](http://dev.w3.org/html5/workers/) (See Editor's Draft 7 July
2011). Web workers enable web applications to launch scripts that runs
in the background while the user interacts with the user interface. In
this way, time consuming tasks can be executed without interrupting any
ongoing user interface, storage, or communication activities. With such
background scripts in mind, the W3C standard for web workers was
proposed as a JavaScript API, where it is up to the application
developer to implement what the web worker actually does.

The difference between the metrics workers in webinos and the W3C
standard for web workers, is that our workers are specialised to perform
application and web metrics. This means that our notion of a metrics
worker is more specific than the web worker definition. Thus, we have
made some more choices on what the webinos metrics workers do. This is
also why the webinos metrics can only seek inspration from the W3C web
worker standard. If webinos fully adopted the web worker standard as is,
it would simply make the application code grow unecessarily large for
the application developer.

### JavaScript APIs[¶](#JavaScript-APIs)

This specification defines an JavaScript API for application metrics
that allows application developers to start a background application
metrics worker that run in parallel to their application. The desired
metrics data can be gathered throughout the application session at both
predefined and custom metrics points. The metrics data is passed on as
messages to the metrics worker in a thread-like, asynchronous fashion.
The metrics worker can upload the metrics to the analytics service in
the background.

This library enables the application developer to run metrics scripts in
the background independently of the main application. This means the
application metrics worker will not be interrupted by the user's
interaction with the application, and therefore can be performed without
worries about how long it may take to gather and upload the metrics for
analytics.

Each application is provided with only one instance of the application
metrics worker each, so that the runtime is not overloaded with metrics
workers. In principle, it is anticipated that the application developer
will register its intent to use the metrics worker at the beginning of
the application session, soon after the application has been launched,
and the metrics worker thread will normally continue until the
application ends - unless the application developer wants to end it
earlier.

#### The MetricsProvider interface[¶](#The-MetricsProvider-interface)

     1 interface MetricsProvider {
     2 /* The metrics provider interface must be implemented by 
     3 any application that would like to use webinos analytics.
     4 */
     5 
     6 void onRegisterMetrics(Session session, MetricsPermissions permissions);
     7 /* The method is called back by the metrics worker 
     8 if the registration has been successful by the application. 
     9 An application session object is provided as parameter for the 
    10 application to refer to when providing metrics. Also a list of 
    11 the permitted data and events is communicated to 
    12 the metrics provider.
    13 */
    14 
    15 void onUnregisterMetrics(Session session);
    16 /* The application metrics worker calls back this method 
    17 when the application has been successful in calling 
    18 the unregister method of the application metrics worker. 
    19 The application session object is provided as input parameter.
    20 */
    21 
    22 void onStopUpload(Session session);
    23 /* The application metrics worker calls back this method after 
    24 the application has called the stopUpload() method of the 
    25 application metrics worker to initiate the stop.
    26 */
    27 
    28 void onStartUpload(Session session);
    29 /* The application metrics worker will call back this method 
    30 when the application called the startUpload() method of 
    31 the application metrics worker to start the upload of 
    32 the metrics data to the analytics service.
    33 */
    34 
    35 void onMetricsLogged(Session session, Event event);
    36 
    37 /*This method is called by the metrics worker whenever
    38  metrics data has been added to the application metrics log. 
    39 (Rename to onMetricsEvent?)
    40 */
    41 
    42 void onMetricsUploaded(Session session, Event event);
    43 /*
    44 This method is called by the metrics worker whenever 
    45 a batch of metrics data has been uploaded to the analytics service.
    46 */
    47 
    48 };

#### The MetricsWorker interface[¶](#The-MetricsWorker-interface)

     1 interface MetricsWorker {
     2 
     3 void register(Intent intent, MetricsProvider provider, Key key);
     4 /* The application must to register its intent to use the 
     5 application metrics worker. It needs to use the key provided to 
     6 the application developer when registering online as 
     7 a user of analytics. It also must refer to the provider itself. 
     8 A metrics permissions object is returned that contains a list of 
     9 metrics permissions.
    10 */
    11 
    12 void unregister(MetricsProvider provider, Session session); 
    13 /* The application can unregister itself from application metrics. 
    14 This will stop the metrics worker and close any web connection that 
    15 maybe busy uploading metric data to the online analytics. 
    16 The call will result in a call back to the onUnregisterMetrics method 
    17 with the session object. The input parameters must be correct for 
    18 the un-registration to succeed.
    19 */
    20 
    21 void startSession(MetricsDataEvent); 
    22 /* This method indicates when the application session is started. 
    23 It should normally be called by the application just after 
    24 the application has been created/ initialised. 
    25 ?Returns that the application session started via a call back method?
    26 */
    27 
    28 void pauseSession(MetricsDataEvent); 
    29 /* This method tells the metrics worker that the application session 
    30 has temporarily paused. The normal place to call this method, 
    31 would be when the user or the runtime is pausing the application 
    32 in some way or another. This would typically be in conjunction with 
    33 the onPause method of the application. 
    34 ?A call to the method will result in a call back from 
    35 the metrics worker to the ... method of the application with parameters 
    36 indicating that the session has been paused.?
    37 */
    38 
    39 void resumeSession(MetricsDataEvent); 
    40 /* This method tells the metrics worker that the application session 
    41 has been resumed/ become active again after it was paused. 
    42 The usual place to for the application to call this method, 
    43 is in conjunction with the onResume method of the application. 
    44 ?Returns that the application session resumed. A call to this method 
    45 will result in a call back from the metrics worker to the ... method 
    46 of the application with parameters indicating that the session 
    47 has been resumed.?
    48 */
    49 
    50 void closeSession(MetricsDataEvent); 
    51 /* Calling this method will log that the session has been closed. 
    52 It will log this and stop any eventual upload activity to the 
    53 analytics service. 
    54 ?This returns that the application session has been closed. ?
    55 */
    56 
    57 void startUpload(Session session); 
    58 /* Calling this method will start a separate background activity 
    59 dedicated to uploading the gathered metrics data to the webinos 
    60 analytics service. The metrics data will be posted at regular intervals. 
    61 One can optionally also delete the metrics data locally, 
    62 once metrics data has been uploaded. 
    63 It will use secure web connection to webinos analytics to upload the metrics data. 
    64 ?After starting the upload, a message will returned via a call back to the 
    65 ... method as means to inform the application about the start of the upload.?
    66 */
    67 
    68 void stopUpload(); 
    69 /* A call to this method will stop any uploading activity to 
    70 the webinos analytics service. It will also close the secure 
    71 web connection to webinos analytics. ?After stopping the upload activity, 
    72 a message will returned via a call back to the ... method as means 
    73 to inform the application about the uploading has been stopped.?
    74 */
    75 
    76 //void onContextEvent called. Returns the Context information added.
    77 //void post new application metrics data at regular intervals
    78 
    79 };

#### The MetricsError interface[¶](#The-MetricsError-interface)

A metrics error describes an event that is considered to be an error
compared to normal system behaviour. Please note that this interface is
only intended for application developers to use when integrating with
the metrics worker. These errors should not be presented to the user.

    1 [NoInterfaceObject]
    2   interface MetricsError{
    3     const unsigned short PERMISSION_DENIED      = 1;
    4     const unsigned short METRICS_NOT_ADDED      = 2;
    5     const unsigned short UPLOAD_CONNECTION_LOST = 3;
    6     readonly attribute unsigned short code;
    7     readonly attribute DOMString message;
    8   };

The code attribute must return the appropriate code from the following
list:

-   PERMISSION\_DENIED - The authentication process failed because the
    application does not have the permission to gather the metrics data
    that it intends to use.
-   METRICS\_NOT\_ADDED - The metrics data that was supposed to be added
    to the log, was not added to the log for some reason. For instance,
    a provider of context information does not work, the log is not
    possible to write to, and so on.
-   UPLOAD\_CONNECTION\_LOST - The secure connection to the analytics
    service was unexpectedly lost. For instance, if the device is out of
    range from the wireless network etc.

The message attribute must contain an error message that describes the
details error details. Please note that this attribute is primarily
intended for application debugging. Application developers should not
use for instance to present it to the user.

#### A metrics worker needs the following interface to be included in the foundations[¶](#A-metrics-worker-needs-the-following-interface-to-be-included-in-the-foundations)

An application affords tasks and information to the end user. Tasks are
focussed activities that the end user can perform to accomplish their
goals, desires, and interests related to the information. An application
enables a finite set of user tasks, and some applications can also to
some extent perform automatic tasks on behalf of the user. An
application provides a user interface for the application developer to
render user interface components, text, video, graphics, sound,
vibration and so on. Thus, it provides a canvas/view where the
application developer can present the user interface components and the
information to the user. Applications would normally be presented in
full screen mode on most mobile devices; however, applications can also
be presented in other ways depending on the look and feel of the device.

Applications must be started by the runtime via the startApplication
method. This might have been triggered by the end user for instance
clicking the application icon to launch the application. The
ApplicationLifecycle interface reflects the various states that the
application can undergo during its lifecycle - from whenever after it
has been installed/ made available for the runtime to launch.

Webinos metrics workers assume a tight integration with the application
lifecycle states and method calls, because an application session
endures throughout the application lifecycle. An application session
should normally start when the application is launched, and normally
should be closed when the application is being shut down.

     1 
     2 interface ApplicationLifecycle{
     3 /* The ApplicationLifecycle interface must be implemented by all applications.
     4 If the application developer see no need in implementing and using
     5 some of the methods, the application developer can leave the methods 
     6 unimplemented. 
     7 */
     8 
     9 void onCreate();
    10 /* onCreate is called by the runtime when the application is starting. 
    11 The application should initialise its starting state when 
    12 implementing this method. A user interface is instantiated and
    13 provided in conjunction with this call.
    14 */
    15 
    16 void onStart();
    17 /*Called by the runtime when the application is (re)started. 
    18 The application should call the startSession method of the 
    19 application metrics worker when this method is called, 
    20 as means to log when the application session (re)started.
    21 Thus, this is either called after the onCreate() or onRestart() 
    22 methods have been called. The application user interface will be 
    23 redrawn again in conjunction with this method call.
    24 */
    25 
    26 void onResume();
    27 /* Called when the application is resumed/ put in the foreground. 
    28 The application should call the resumeSession() method of the 
    29 metrics worker when this method is called, 
    30 as means to log when the application session resumes.
    31 */
    32 
    33 void onPause();
    34 /* Called when the application is paused/ put in the background. 
    35 The application should call the pauseSession() method of the 
    36 metrics worker when this method is called, 
    37 as means to log when the application session pauses.
    38 */
    39 
    40 void onStop();
    41 /* Called after onPause when the application is no longer 
    42 visible for the end user. One of three things can happen 
    43 after this method call: The application can either 
    44 be restarted, destroyed, or just do nothing of the device 
    45 for example is switched off by the end user. Thus, what
    46 happens next depends completely on the interaction with 
    47 the end user. The methods onRestart() or onDestroy()
    48 can be called, but this is not guaranteed unless that was the 
    49 intention of the end user.
    50 */
    51 
    52 void onRestart();
    53 /* Called after the onStop method if the user interacts
    54 in a way on the device that indicated that the user
    55 wants the application to restart again. It is called when the 
    56 application is presented/ made visible to the end user again.
    57 A call to this method also implies that both the onStart and onResume
    58 methods will be subsequently called afterwards as a result.
    59 */
    60 
    61 void onDestroy();
    62 /* The application will use this method to shut down the 
    63 application metrics worker before the application exits. 
    64 The application should call the closeSession method of the 
    65 application metrics worker when this method is called, 
    66 as means to log when the application session is closed. 
    67 The metrics worker will try to upload the metrics in the background,
    68 after the application has been destroyed.
    69 */
    70 
    71 };

Please note that the webinos application lifecycle interface is heavily
inspired by the activity lifecycle in Android. See the Android
[Activity](http://developer.android.com/reference/android/app/Activity.html)
class. This is a tested foundation that works very well. The activity
lifecycle of Android is inspired by other state of the art mobile
platforms too, such as J2ME, Symbian, and iOS.

### Dependencies on other components[¶](#Dependencies-on-other-components)

Application metrics workers are dependent on the following:

-   Context API
-   Secure storage
-   Secure Socket Layer communication

Server metrics workers are dependent on the following:

-   The web server platform of choice
-   The Common Gateway Interface of the web server
-   Secure storage

### Implementation Architecture[¶](#Implementation-Architecture)

Start to look at actual **implementation** issues for code - this does
not presume interoperability and will consider platform specific issues

