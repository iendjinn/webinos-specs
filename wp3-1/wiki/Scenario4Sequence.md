Scenario 4 Sequence Diagram[¶](#Scenario-4-Sequence-Diagram)
============================================================

![ title : Scenario 4\\nGeorge wants to listen to Paul's MP4s on his
mobile\\nmobile to mobile, and neither have access to the internet actor
George participant "George's mobile" as George\_mobile participant
"Paul's mobile" as Paul\_mobile actor Paul autonumber note over George,
Paul \#FF6666 : this scenario differs from scenario 3 in note before
step 15 == identification == group identification example George -\>
George\_mobile : switch on George\_mobile -\> George : ask the pin
George -\> George\_mobile : provide the pin end == device discovery ==
group device discovery example note over George, George\_mobile : the
user may set a policy to automatically\\nstart device discovery
George --\> George\_mobile : \<font color="gray"\>\<i\>start device
discovery\</i\>\</font\> George\_mobile -\> Paul\_mobile : broadcast
hello message note over Paul\_mobile, Paul : For privacy reasons Paul
MAY explicitly\\nturn on visibility of his mobile for the\\ndiscovery
process Paul\_mobile -\> George\_mobile: hello response end == personal
local cloud join == George\_mobile -\> George : show available
clouds\\nand devices George -\> George\_mobile : select Paul's mobile
George\_mobile -\> Paul\_mobile : George's mobile tries to authenticate
note over George\_mobile, Paul\_mobile : authentication fails because
George's mobile\\ndoesn't know Paul's personal cloud secret
Paul\_mobile -\> George\_mobile : authentication failed
George\_mobile -\> Paul\_mobile: ask for join permission
Paul\_mobile -\> Paul : ask for join permission Paul -\> Paul\_mobile:
grant join permission group session key exchange example
Paul\_mobile -\> Paul : generate a session key note over George\_mobile,
Paul\_mobile : How to communicate the session key?\\n- out-of-band\\n-
by a clear, local channel (e.g. by bluetooth)\\n- by an encrypted
channel created without a trusted third party\\n (e.g. a device can send
his public key to the other one) Paul -\> George : communicate the
session key out-of-band George -\> George\_mobile : insert session key
end note over George\_mobile, Paul\_mobile : devices can use the session
key\\nto establish a secure channel George\_mobile -\> Paul\_mobile :
establish a secure channel == service provision == George -\>
George\_mobile : ask for MP4 list George\_mobile -\> Paul\_mobile : MP4
list retrival Paul\_mobile -\> Paul : ask for MP4 list\\nsharing
permission note over Paul, Paul\_mobile : the permission is temporary
because the\\napp user is a personal local cloud guest Paul -\>
Paul\_mobile : grant temporary permission Paul\_mobile -\>
George\_mobile : MP4 list transmission George\_mobile -\> George : MP4
list display George -\> George\_mobile : MP4 selection
George\_mobile -\> Paul\_mobile : MP4 retrieval Paul\_mobile -\> Paul :
ask for MP4 sharing permission note over Paul, Paul\_mobile : the
permission is temporary because the\\napp user is a personal local cloud
guest Paul -\> Paul\_mobile : grant temporary permission
Paul\_mobile -\> George\_mobile : MP4 transmission George\_mobile -\>
George : MP4 consumption George -\> George\_mobile : select another MP4
George\_mobile -\> Paul\_mobile : MP4 retrieval Paul\_mobile -\>
George\_mobile : MP4 transmission George\_mobile -\> George : MP4
consumption
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=f90fd93db23fee3f3fd8da698b5f4566c8a50740a1891ad186f2b862f623188d)

REMARKS:

All Like in scenario 3. Just the fourth case of step 15 it is not
possible without internet access.

