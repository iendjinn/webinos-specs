Component and communication diagrams[¶](#Component-and-communication-diagrams)
==============================================================================

An application communicating with an API on a local PZP (Virgin PZP)[¶](#An-application-communicating-with-an-API-on-a-local-PZP-Virgin-PZP)
--------------------------------------------------------------------------------------------------------------------------------------------

![ title An application communicating with an API on a virgin PZP
component Application as app component PZP as p interface findServices
as find interface API as api p -up- find p - api app -up-\> find app -\>
api
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=b8e03fc33c076edc0f19ce44ccc1dd64afeb9f3b4b70dfc0143806c88391a54a)

An application communicating with an API on a local PZP[¶](#An-application-communicating-with-an-API-on-a-local-PZP)
--------------------------------------------------------------------------------------------------------------------

![ title An application communicating with an API on a local PZP
component Application as app component PZP as p component PZH as h
interface PZP\_findServices as p\_find interface API as api interface
PZH\_findServices as h\_find interface registerServices as reg h -up-
reg h -left- h\_find p -up- p\_find p -left- api p -up-\> reg
p -right-\> h\_find app -up-\> p\_find app -\> api
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=550aaf1b61dc70b4a8d7419dce253b5c01e54454641f56e13aedaf0ff23cb19b)

An application communicating with an API on a PZP on another device in the zone[¶](#An-application-communicating-with-an-API-on-a-PZP-on-another-device-in-the-zone)
--------------------------------------------------------------------------------------------------------------------------------------------------------------------

![ title An application communicating with an API on a PZP on another
device in the zone component Application as app component "local PZP" as
p component "other PZP" as o component PZH as h interface
PZP\_findServices as p\_find interface API as api interface
PZH\_findServices as h\_find interface registerServices as reg h -up-
reg h -left- h\_find p -left- p\_find p -up-\> reg p -right-\> h\_find
o -left- api o -right-\> reg app -right-\> p\_find app -up-\> api
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=72b1045a88286407f9744cf41d47fa74a3de956929f3b88d8e5b0d1bc63675d0)

An application communicating with an API on a PZP on another device in a different zone[¶](#An-application-communicating-with-an-API-on-a-PZP-on-another-device-in-a-different-zone)
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

![ title An application communicating with an API on a PZP on another
device in a different zone component Application as app component "local
PZP" as p component "other PZP" as op component "my PZH" as h component
"other PZH" as oh interface PZP\_findServices as p\_find interface API
as api interface PZH\_findServices as h\_find interface
my\_PZH\_registerServices as reg\_h interface
other\_PZH\_registerServices as reg\_o h -up- reg\_h h -left- h\_find
p -left- p\_find oh -left- reg\_o op -left- api note top of h it is not
necessary to register my\_PZH's APIs to other\_PZH\_registerServices end
note p -up-\> reg\_h p -right-\> h\_find oh -down-\> reg\_h op -right-\>
reg\_o app -right-\> p\_find app -up-\> api
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=27bcd9f15b3f90effaf3a32890f9b2c3adbf693ebe03d002697c096ec3b3664d)

![ title An application communicating with an API on a PZP on another
device in a different zone (alternative) component Application as app
component "local PZP" as p component "other PZP" as op component "my
PZH" as h component "other PZH" as oh interface PZP\_findServices as
p\_find interface API as api interface my\_PZH\_findServices as h\_find
interface my\_PZH\_registerServices as reg\_h interface
other\_PZH\_findServices as o\_find interface
other\_PZH\_registerServices as reg\_o h -up- reg\_h h -left- h\_find
p -left- p\_find oh -left- reg\_o oh -down- o\_find op -left- api
h -up-\> o\_find p -up-\> reg\_h p -right-\> h\_find op -right-\> reg\_o
app -down-\> p\_find app -up-\> api
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=05b0941243352731b328c124bc865540a030643e8f6dbdb034081577089cbf82)

Accessing the web interface of the PZH and authenticating the user[¶](#Accessing-the-web-interface-of-the-PZH-and-authenticating-the-user)
------------------------------------------------------------------------------------------------------------------------------------------

![ title Accessing the web interface of the PZH and authenticating the
user component Browser as b component PZH as h component IdP as p
interface "start OpenID\\nauthentication" as login interface "access
OpenID\\ncredentials" as credentials interface "authenticate
using\\nOpenID credentials" as auth h -up- login h - auth p -left-
credentials b -left-\> login : use b -right-\> credentials : use b --\>
auth : use
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=11616f90cb6c773eb8421824e23f5ca01198f212bd7fca399a39a14e671b3aa0)

Creating a PZH[¶](#Creating-a-PZH)
----------------------------------

![ component "PZH Farm" as farm component "New PZH" as pzh component
"Certificate Manager" as cm interface addPzh as ah interface selfSigned
as ss interface signRequest as sr pzh -left- ah cm -left- ss cm -down-
sr farm -right-\> ah pzh -right-\> ss pzh -down-\> sr
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=a06ad25f64ae50c5af161c26031414ac801c798598e2e8023d09d16f85532fe2)

