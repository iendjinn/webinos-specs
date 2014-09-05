Scenario 8 Sequence Diagram[¶](#Scenario-8-Sequence-Diagram)
============================================================

![ title : Scenario 8\\nGeorge wants to listen to music stored on his
mobile, through the set-top box\\nbut this time using the set-top box as
the controller actor George participant "George's set-top-box" as
George\_set\_top\_box participant "George's mobile" as George\_mobile
autonumber note over George, George\_mobile \#FF6666 this scenario
differs from scenario 1 in the identification phase and in role exchange
between set-top-box and mobile end note == identification == group
identification example George -\> George\_set\_top\_box : switch on
George\_set\_top\_box -\> George : prompt for identity note over George,
George\_set\_top\_box : e.g. insert George WID George -\>
George\_set\_top\_box : insert identity end == device discovery == group
device discovery example note over George, George\_set\_top\_box : the
user may set a policy to automatically\\nstart device discovery
George --\> George\_set\_top\_box : \<font color="gray"\>\<i\>start
device discovery\</i\>\</font\> George\_set\_top\_box -\> George\_mobile
: broadcast hello message George\_mobile -\> George\_set\_top\_box:
hello response end == personal local cloud join == note over
George\_set\_top\_box, George : the user may set a policy to
automatically\\nselect devices to autenticate and join.\\nthree possible
solutions are:\\n- try to authenticate every sensed device\\n- maintain
a local membership list\\n- maintain a remote membership list
George\_set\_top\_box -\> George : \<font color="gray"\>show available
clouds and devices\</font\> George -\> George\_set\_top\_box : \<font
color="gray"\>select the mobile\</font\> George\_set\_top\_box -\>
George\_mobile : George's set-top-box authentication George\_mobile -\>
George\_set\_top\_box : George's mobile authentication note over
George\_set\_top\_box, George\_mobile : personal cloud devices can use
their shared secret to\\ndistribute session keys and establish secure
channels George\_set\_top\_box -\> George\_mobile : establish a secure
channel == service provision == George -\> George\_set\_top\_box : ask
for MP4 list George\_set\_top\_box -\> George\_mobile : MP4 list
retrieval George\_mobile -\> George\_set\_top\_box : MP4 list
transmission George\_set\_top\_box -\> George : MP4 list display
George -\> George\_set\_top\_box : MP4 selection
George\_set\_top\_box -\> George\_mobile : MP4 retrieval
George\_mobile -\> George\_set\_top\_box : MP4 transmission
George\_set\_top\_box -\> George : MP4 consumption
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=870de63da2761eaedb991864b5a5e4c1bd83a1e932143229e34c77ca7c7fb247)

REMARKS

How to establish the secure channel?

Personal cloud devices can use their shared secret to distribute session
keys and establish secure channels.\
They can use a pairwise session key for every channel and a common
session key (personal-cloud-wise session key?) for broadcast
communications.\
When a device leave the cloud may be necessary to renew the broadcast
key.

