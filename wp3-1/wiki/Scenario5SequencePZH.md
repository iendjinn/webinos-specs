Scenario5SequencePZH[¶](#Scenario5SequencePZH)
==============================================

![ title : Scenario 5\\nGeorge has music hosted on a web service,\\nand
wants to listen to them on his own mobile device actor George
participant "George's mobile" as George\_mobile participant
"George's\\npersonal\\nzone proxy" as pzp participant SP autonumber ==
identification == group identification example George -\> George\_mobile
: switch on George\_mobile -\> George : ask the pin George -\>
George\_mobile : provide the pin end == authentication == George -\>
George\_mobile : insert address of\\nService Provider (SP) alt first
step: contact the SP George\_mobile -\> SP : try to access Service
Provider SP -\> George\_mobile : redirect to PZP note over SP,
George\_mobile Doesn't works. How can SP know where to redirect the
connection? end note else first step: contact the PZP autonumber 5
George\_mobile -\> pzp : authenticate pzp -\> George\_mobile : return
the credential George\_mobile -\> SP : transmit the credential end ==
service provision == George -\> George\_mobile : ask for music list
George\_mobile -\> SP : music list retrieval SP -\> George\_mobile :
music list transmission George\_mobile -\> George : music list display
George -\> George\_mobile : music file selection George\_mobile -\> SP :
music file retrieval SP -\> George\_mobile : music file transmission
George\_mobile -\> George : music file consumption
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=e06fe0997e01df8ffa232a4eebbc74cb81123c82aebc93f4ec2f8b857292691c)

