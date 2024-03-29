Minutes-friday[¶](#Minutes-friday)
==================================

**Session Start: Fri Feb 25 08:49:39 2011**\
Minutes for Friday, Feb, 25th, 2011\
**Starting with the WP4 session.**

Formally WP4 does not start until month 11.\
To help some of the discussions on the architecture level, some\
stuff has been prepared.\
First demo: IE mit plug-in to display 'BONDI-style Norton Commander'.\
Application is not locally hostet, but security features still apply as\
if it was an widget.\
Includes full implementation of BONDI security level.\
'Environment' such as roaming/bearer type can be simulated to demo\
effect of policies.\
Just a demo environment, not something to aim for, but helpful as an
info tool and\
teaching aid.\
Based on .NET\
Easy to quickly create and mock-up APIs.\
Will be put on Redmine SVN\
Code will be put up on redmine for people to play with it.

**Question about Linux version:**\
How to put on Linux? This is just a tool to help with specification
work - hold that question\
Nick: This is a tool to aid specification work. Other platforms will be
discussed later.\
Tool developed for creating XACML\
Next demo: Tool for creating policy files.\
Rules/Policy Set/Query\
Rules describe under which cirumstance you allow what level of access.\
E.g. allow, deny, prompt.\
Adding new resources, environment variables possible. Good framework for
exploring this.\
Test page: test environments against queries to see what will happen.\
Also populates test matrix based on environment (roaming, etc.)\
Extensions to XACML defined to PrimeLife to put obligations on Privacy

(Comment by Dave Raggett)\
Code for "webinos policy builder" will be made available as well.\
Stressing again that this is not the "initial code" for webinos, but
more\
an example and 'playground'.\
To help specification work to focus.

One of the big problems with DAP and BONDI apis is the abstraction of
device features/services (e.g. multiple calendars). Assumed to be an
implementation issue, but needs to be handled in specification. Give app
developer the ability to access multiple instantiations of services.\
Almost need a URI as a data source for an API ( e.g. the URI of a google
calendar ) rather than assuming some level of abstraction provides it.\
For webinos to work properly, it should allow the application developer
to open a specific calendar: "Alan's GMail calendar". So need some kind
of description model to define who Alan is, perhaps a SIP address, and a
URI to define which of his calendars it is. This is even true on
personal devices - you may have a calendar on your mobile and somewhere
else.\
Javascript Remoting\
Next step of pre-WP4 work should be demo on how JavaScript remoting
should work.\
Taking basic runtime (for the purpose of this it might just be a plain
browser).\
Intention is to produce a small demo running a node.js server\
Initially messaging over XHTTP\
All exposed through a small javascript proxy service\
Small demo using a remote 'Node.js' proxy service.\
The 'Node.js' may, for example expose the gallery of a rmote device
(such as a set-top box).\
As far as most of the elements are concerned, gallery calls and gallery
exposure\
are local, limited interface needed to actual 'remote'
functionality,might be via WebSocket or Bluetooth/Zigbee.

Question/Comment: You need both devices in this architecture to be on
different, remote devices. May be easier to do on mobile for now.\
Reply: Not too fussed about the devices so far.\
Question: Please explain role of JavaScript Proxy.\
Question: Role of Javascript stubbed proxy?\
In BONDI or W3C a 'get photo from gallery' is a local JavaScript
function.\
For two-device implementation the gallery would be remote - functionally
the API is the same.\
How does the remote entity get resolved?\
Now a programmer would implement SOAP/REST interface to image server.\
Under the hood, we might actually do the same, but we allow 'magically'\
Instantiate a small Javascript object, don't dip down into the device,
instead does an XHR request to the Picasa Server and get the photos
using the JavaScript interface without providing the need to implement
the REST part.\
Question: How does the magic work then?\
Not clear, but probably by wrapping JavaScript call in JSON, transfer,
execute\
From the web developer point of view: how do they target where they get
their photo from?\
locally and return result vie JSON.\
Reply: depends on the identity model. May have pre-configured data
sources\
Webinos needs to expose the interfaces to, e.g., all photo services the
user has access to\
Comment: developer needs a way to specify which photo source to get
access to. May not be the same as the last one that was used...\
Reply: this is a problem 3.1 needs to solve, and this is why demos will
be so important. Need more than one "contacts" API, "calendar" API.\
Does the developer need to know the names involved (e.g. "Nick's
Calendar") or not? Also, who controls which calendar: is the detail
important or not. Is "Alan's Calendar" sufficient or is "Alan's GMail
calendar" important.\
Comment: Data management is important here. Do you simply request data,
or does the data know where the call should go?\
Comment: support the idea of early demos\
Comment: policy starts getting very interesting here.\
This is where policy is starting to get really interesting...\
Longlasting XHTTP will not provide long term sessions... Need to send
"invisible SMS" to wake systems up\
Example contains 'SMS Wakeup' element that is needed due to mobile
sessions\
are not longlasting - an implementation detail that would likely to be\
missed if not working with demos and early implementations.\
Misuse cases will see whether this JavaScript Stubbed Proxy approach is
secure enough\
Question is XHTTP done as an XMLHTTPRequest?\
Probably in first iteration, but not need to be.\
Task 3.1 should not just be Wiki text in documents - it should include
code,\
Hope that the output of WP3 is not just wikis and documents. Hope to
encourage the philosophy of creating proof-of-concept demos\
stubs and proof of concept demos.\
Using XHR and exposing it to the developer is not the most optimal way
of doing remote access to a resource\
Alternative models: access device APIs through a web server.\
However, not the most optimal developer interface as developers will
wrap these calls in Javascript also: back where we started\
Question: What about 3rd party APIs?\
**3.1 service discovery** piece needs to handle this.\
In a simple way, 'just' take the service function, create a JSON wrapper
and\
use it.\
API extensibility through "meta descriptions" of functionality?\
In BONDI/WAC you would probably need some code to inject at JavaScript
interpretation point.\
Security gotchas.\
Gotcha for that approach would be security handling.\
Clearing up misunderstanding - possible C++ code would be an internal
part of the\
runtime, not something exposed to the developer.\
Fix the problem of binding the APIs into the runtime: solve security
issues.\
If we do webinos properly, we have to address exactly this kind of
problem.\
Comment: sometimes web developers want synchronous APIs, but this can't
always be the case.\
Response: Yes - need to do some demos\
What APIs are needed?\
Scope is almost infinite, but we need to prioritize\
Let's see what demos we want to create first to have compelling demos
soon.\
Propose to look at the apps that want to be created in WP5 and use this
to prioritize WP3 and WP4.\
This will help us to prioritize WP3 and WP4 work.\
List of APIs: gallery/file/local device discovery/ social network person
discovery/dumb device connect/native application connect.\
Propose to prioritize: Gallery APIs, File APIs, local device discovery
(one of the hard problems: needs discovery and identity components),
social network augmented discovery, dumb device connect for the "cool
demo" perspective - something not considered a normal computer.\
Comment: local device discovery. There are some interesting problems you
come up against. Samsung - getting outside the firewall can be a very
difficult problem to solve in IPV4 world. Inside own wireless network
this can be fine, between wireless networks is **much** harder

**3.1 device discovery needs** to be working with demos immediately\
Comment: integrate with W3C working groups (P2P)\
Comment: how to unify the identities on social networks and contacts\
Comment: need to do a matching of content\
content = context\
Solutions from literature are quite complex. Worth having a discussion\
Propose that we discuss solutions from literature.\
This part of building the demo is interesting\
Hans: Need to merge vcal, vcf, social networking identity\
Nick: Hans in 5.1 needs to get started ASAP.\
Comment (Stephan): Do partners in 5.1 have the resource?\
18 man years worth of effort\
Interested in getting as much forward planning done as possible. Want to
get people working on the most appropriate areas\
List of resources: WP4 is almost 18 person years, value of 1.5 million
Euro.\
Important questions to partners:\
Tell nick: Domain knowledge, language skills, components you are
interested in...\
What code do you have?\
What languages?\
Component preferences?\
Webkit stack?\
Javascript code ?\
We need to start working out what operating systems and languages and
web stack to use.\
UPnP?\
Question: do we need a bigger list than just "Webkit stacks, javascript
code, upnp" - is there a list of technology anywhere?\
Aim is to be cost effective with resources - no point in re-implementing
UPnP\
or Bluetooth code. If it exists in Open Source, use it. If needed
license\
existing stuff for the purpose of demos, etc.

Action: Nick starts a skeleton of technologies\
AP: Nick will do a skeleton of a list on Wiki.\
What level of the bluetooth API stack are we interested in?\
Don't know yet which parts are hidden and which are exposed.\
For example we might have reasons to expose an Bluetooth API, but it
might\
just be lower level in the communication interface and hidden from the
API programmer.\
Question: if we find something that is open source but owned by a
company - might be able to do this. But not always easy. Samsung are
supposedly keen to do this.\
For Samsung there might be a possibility to OpenSource some sources that
are already there.\
Platform/OS: Technical problem and political.\
Some code will be contributed back to LiMo in the next few months. Might
ve available, but needs to be cleared politically and legally,

**PlatformOS:**\
Starting assumption: must do something on Android.\
We need to do Android - no doubt.\
We need to have a runtime on all three PC operating systems.
**Possibly** lose Linux\
Developers are so tied to Mac, we don't want to lose that.\
We probably need all three PC OS (PC/MAC/Linux) - we might drop Linux,
but\
First issue: How do you hit Mac/Win/Linux from an engineering
perspective?\
developers are strongly attached to Linux, so ignoring that might have a
backlash as\
far as community support is concerned.\
Not a good idea to rub Linux developers in an OpenSource system.\
Comment: for an Open Source project we should not drop Linux\
No good HTML/Webkit experience in J2SE\
J2SE and J2ME are not options - not a good technical experience.\
We can't drop Linux: would hurt potential automotive implementation\
Do we put app on qt? What do we build on?

for Linux\
Once you say Linux you need to decide what WebKit package you use.\
Qt is quickly on its way out.\
Comment: What's wrong with Chrome?\
Chrome works on Linux, Windows, Mac...\
Possible option is the use of Chromium.\
Samsung comment: Android is a linux-based kernel. Meego is Linux-based
system. OSX has some overlap. Windows stuff would be more painful?\
Comment: Porting to Windows may be the biggest pain?\
Something set-top-box is linux based, something mobile is linux based,
some TVs have linux kernels (Samsung), Automotive platform at BMW will
be based on Linux in January\
Additional reason for Linux would be that set-top boxes (such as MythTV
boxes) are\
Nick: As much information on what BMW will use would be useful\
often based on Linux anyway, same for the automotive domain.\
BMW: We can use Debian, Fedora, anything like that.\
We don't have to go with Genivi for the automotive development -
standard distributions will\
Comment: might get some cloud service accessibility out of Ubuntu\
be an option for development/demo - might require some WebKit adaption
for input\
devices and some massaging of the browser to remove browser frame and
such, but\
essentially fairly open choice.\
Big picture question to resolve: with respect to multi-pc
implementation, do we take the hit and do a webkit stack on each? Or do
we use a tool to maintain one codebase?\
Samsung: Integrate as closely with the device APIs - putting in an
abstraction\
Comment: From an integration point of view, we prefer to do a tight
integration with, say, WebKit and OS. Having a layer inbetween is always
difficult to deal with. Particularly when doing non-mainstream stuff.\
layer (such as Qt) creates more problems than it solves.\
Also licence problems with Qt.\
Engineering effort might deviate based on which demos are cool.\
Another constrain (Action for commercial partners?): want to do "cool
demos". If a certain "cool" device is running on a particular platform,
we need to know. Please come forward with specific device constraints\
Rather adapt to a cool device / service than be too attached to a
theoretical\
wider base with fewer actual possibilities.\
Action: Find potential devices and look at constraints, technical
details. We would need access to a few of them, and to be able to demo a
few months down the line.\
AP: Companies provide information about possible
devices/features/capabilites.\
Request to Sony Ericsson and Samsung: can we have something with near
field communication. please?\
Hans: Request to Samsung/SonyEricson - make sure that Android devices
have NFC support,\
meaning 2.3.x version of Android.\
Request: does anyone have particular "dumb devices" which wont have a
runtime on it.\
Same for dumb devices.\
Comment: digital cameras might be a reasonable "dumb device" but have
bluetooth built in.\
Dumb devices (in first approximation) are devices without direct
Internet connection.\
Need to find a commercial partner with an interest in these.\
Problem: authenticating user to device. Need to expose device
capabilities to the device for AuthN.\
Possible uses for authentication - for example smart card readers or
waving a phone\
at the PC to authenticate yourself.\
Invoking external parties for dumb devices also helps in finding
someone\
standing behind a cool demo ten months down the line.\
Trying to chuck in as much code as possible onto the server. If it is
used, fine.\
Comment (John): Request for some useful tools to be put on the SVN for
the rapid prototyping in WP3\
If other want to use their own stuff, fine as well. All are encouraged
to do that as well.\
Is mostly to support WP3 and partly for WP5. WP4 should start from clean
slate\
with commercial quality implementing.

**PMB Meeting**\
Agenda is:\
1. Conclusion from project meeting\
2. Recommendation for next meetings (Sophia...)?\
3. Project review preparation\
4. 3rd party interworking / involvement\
5. Domain experts involvement\
6. Setup Advisory Board\
7. Reporting / Resourcing\
8. Amendment \#3\
9 What else?

3rd party interworking - basic legal procedure will be established by
Nick before review.\
This is different from the source code contributor agreement\
First legal boilerplate will be provided by Nick by next week.\
Consortium agreement should be out today.\
AP: Everyone check document with legal department, changes are marked,
so\
checking should be fast - hope to start signing in two weeks.\
Domain experts mail has been sent out already (yesterday).\
Review meeting:\
April, 1st in Brussels\
Financial data is not needed, resource usage is.\
Collect month 1-6, plan 7-12.\
Also travel (when, where, who) and event participation.\
No other resource spending.\
Agenda for review has already been sent.\
Pre-meeting in Brussels, noon March, 31st, probably IBBT provided room.\
Draft slides by March, 20th.\
IBBT will provide room in Brussels.\
Direct feedback after review, but formal write-up will follow later.\
Attendee list, currently 13 people.\
Correction for earlier list - Ivan instead of John for Oxford\
BMW might be represented by Simon instead of Thomas.\
Probably no active role, but someone from the automotive domain needs to
be there\
in case of questions.

Added Samsung to have mobile/TV manufacturer representative at review.\
WP2 presentation may be reshuffled\
For the WP session concentrate on content, not on resources and
timings,\
since these are partly presented in the initial presentation and also
in\
the reviewer's materials.\
Specific segment on D8.2 Exploitation plan un WP8 presentation\
WP7 also needs to specifically refer to deliverables 7.1, 7.2 and 7.6\
Question: Will this be very interactive?\
There is a specific question and discussion session, so the individual
sessions

should not be too interactive, but we should prepare (and allow time)
for\
interaction during the presentations as well, of course.\
Deliverables:\
We have a certain leeway with delivery dates, but deliverables **have**
to be\
available for the review 14 days before the review **latest**.\
This is a fixed and non-negotiable date. Deliverables delivered after
that

will not be at review.\
Distribution of deliverable will be done by PO. We only submit to PO.\
Question about common slide template.\
Yes, we will have one - using same webinos template, not company
templates.\
Take slide of this PMB presentation from BSCW and use that as template.

Only the deliverables themselves will be needed to be provided to
reviewers,\
no special project summary or overview document.

Sorry, connection problems- not minuted was the overview of slides to
provide per WP.\
Did not deviate from info presented on slides.

Need to provide indication of 3rd party activities.\
Even without CA finished yet, we are using alternative ways to contact\
and stay in contact with 3rd parties. This should be highlighted at
review.\
Regarding deliverables: Should also mention our process of keeping them\
alive and updating them.\
AP: Make sure that public deliverables are available on web site at time
of review.\
Note (George G): In other reviews there was a request not to publish
before read\
by reviewers.\
We will check with the PO, but we should stress that this would create
timing\
issues for some of the WP since, for example, the specification would
not\
be visible outside the project for months.\
AP: Stephan to mail to PO about the publication of deliverable.\
Questions to reviewers:\
Would online deliverables be ok?\
Any workplan changes?\
Publishing of not yet accepted deliverables? (see above - but should
also be asked to the reviewers)\
Review preparation phone conference after slides have been submitted
(after March 20th).\
Hotel suggestion will be sent around next week - we should try to stay
all in the same one.\
Need to have Advisory Board plan and recommendations (name list) in
place for review.\
Would be good to also have non-European experts\
AP: Stephan send mail asking for suggestions.\
AP: Partners send suggestions to Stephan.\
Suggestion: Eric Wilde (formerly ETH, now Berkeley) - even more formerly
FOKUS...\
Suggestion: Someone from Opera\
We will have to decide on how much access advisors will have.\
Alan will also check with a couple of people he knows.\
Possibly worth asking Wendy Hall\
Also need to look for someone in the automotive domain.\
Also good to address future customer of ours - useful to engage them
early.\
Allow flexible commitment - if someone is a specialist in system
architecture,\
the person should not feel like committing for three full years.\
Next topic: Amendmend \#3\
Shift in T2.7 from Samsung to Polito (2.5 PM)\
Any other?\
Peter: Shift from SonyEricsson to Polito and TNO and Fraunhofer\
might not be reflected yet.\
Might be confusion of SonyEricsson and Samsung - will be checked
offline.\
No big issues, so we can probably close amendment \#3 by time of
review.\
Open issues are not only the resources, but also early start of WP5 and
WP6.\
Does not need to be reflected in amendment if we start early - changing
amendment\
might help if we're spending a lot of effort (since it looks better),
but\
not relevant legaly or for resource consumption.\
There is also a small difference in wording between WP7 task description
and part B.\
(Different numbers for promised number of papers and things like this).\
Let's do that after the review, in case there are changes of the
amendment suggested\
by the reviewers, we can do both at the same time.\
Back to agenda.\
Meeting conclusions will not be covered now.\
AP: Stephan will send mail asking PMB for comments and conclusions.\
Guidelines for reporting will be send around by Fraunhofer.\
Level of reporting will stay the same as in WP2 (monthly reporting of PM
on per task level)\
Reporting will be however on some redmine form/wiki instead of mailed
Excel sheets.\
-\
Almost done now. Thanks to Telecom Italia for organizing, see you all
again

in Brussels (review), on May, 2nd (WP3 meeting, no site known yet,
probably at SEMCA)\
or in June at the next full meeting in Sophia Antipolis.\
-\
**End of meeting. Safe trip home!**

