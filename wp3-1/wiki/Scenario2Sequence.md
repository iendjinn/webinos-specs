Scenario 2 Sequence Diagram[¶](#Scenario-2-Sequence-Diagram)
============================================================

![ title Scenario 2\\nGeorge wants to view his mobile hosted MP4s on his
set-top-box\\nand neither of the devices have access to the internet
actor George participant "George's mobile" as George\_mobile participant
"George's set-top-box" as George\_set\_top\_box autonumber note over
George, George\_set\_top\_box \#FF6666 : this scenario differs from
scenario 1 in note before step 7 == identification == group
identification example George -\> George\_mobile : switch on
George\_mobile -\> George : ask the pin George -\> George\_mobile :
provide the pin end == device discovery == group device discovery
example note over George, George\_mobile : the user may set a policy to
automatically\\nstart device discovery George --\> George\_mobile :
\<font color="gray"\>\<i\>start device discovery\</i\>\</font\>
George\_mobile -\> George\_set\_top\_box : broadcast hello message
George\_set\_top\_box -\> George\_mobile: hello response end == personal
local cloud join == note over George\_mobile, George : the user may set
a policy to automatically\\nselect devices to autenticate and
join.\\ntree possible solutions are:\\n- try to authenticate every
sensed device\\n- maintain a local membership list\\n- maintain a local
copy of a remote\\n membership list George\_mobile --\> George : \<font
color="gray"\>show available clouds and devices\</font\> George --\>
George\_mobile : \<font color="gray"\>select the set-top-box\</font\>
George\_mobile -\> George\_set\_top\_box : George's mobile
authentication George\_set\_top\_box -\> George\_mobile : George's
set-top-box authentication note over George\_mobile,
George\_set\_top\_box : personal cloud devices can use their shared
secret to\\ndistribute session keys and establish secure channels
George\_mobile -\> George\_set\_top\_box : establish a secure channel ==
service provision == George -\> George\_mobile : ask for MP4 list
George\_mobile -\> George\_set\_top\_box : MP4 list retrieval
George\_set\_top\_box -\> George\_mobile : MP4 list transmission
George\_mobile -\> George : MP4 list display George -\> George\_mobile :
MP4 selection George\_mobile -\> George\_set\_top\_box : MP4 retrieval
George\_set\_top\_box -\> George\_mobile : MP4 transmission
George\_mobile -\> George : MP4 consumption
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=64d604da054beae2edfe2b6e314dcdf2ebcd374047fc6126c4368981ec8a6599)

-- "Personal local cloud join" open points --

How to select devices to authenticate?

a\) like in scenario 1

b\) like in scenario 1

c\) maintaining a personal cloud membership remote list (e.g. on WAP)\
 c.1. George's mobile gets the personal cloud membership list from the
local cache\
 c.2. George's mobile tries to authenticate devices of the personal
cloud membership list

d\) *extension of C)*: primary device of the user runs a backup service
which provides all the features of online entities\
 d.1. George's mobile cannot reach the online entity which stores the
cloud membership remote list (e.g. the WAP)\
 d.2. George's mobile starts discovering other devices belonging to
George's cloud which might be reachable on the network (in contrast to
the WAP)\
 d.3a. if any of the reachable devices of George's cloud runs a baackup
service, George's mobile retrieves the list from there\
 d.3b. if none of George's other devices is reachable or if none of them
runs a backup service, George's mobile uses its own cached list of
devices and starts running the backup service for any other device which
may join later\
 Note: d) is more complex than c) but it has two advantages: (1)
behaviour of devices in the online and offline case are almost the same,
(2) cached lists can be synchronised with the other devices in the cloud
more easily

