Scenario 5 Sequence Diagram[¶](#Scenario-5-Sequence-Diagram)
============================================================

![ title : Scenario 5\\nGeorge has music hosted on a web service,\\nand
wants to listen to them on his own mobile device actor George
participant "George's mobile" as George\_mobile participant WAP
participant UR participant IDP participant SP autonumber ==
identification == group identification example George -\> George\_mobile
: switch on George\_mobile -\> George : ask the pin George -\>
George\_mobile : provide the pin end == authentication == George -\>
George\_mobile : insert address of\\nService Provider (SP)
George\_mobile -\> SP : try to access Service Provider SP -\>
George\_mobile : redirect to Webinos Authentication Provider (WAP)
George\_mobile -\> WAP : ask for authentication WAP -\> UR : ask for
user account list UR -\> WAP : return the user\\nIdentity Provider (IDP)
list WAP -\> George\_mobile : return the IDP list note over
George\_mobile, George : IDP can be automatically selected\\nby the
mobile using a policy or a\\nstored user preference George\_mobile --\>
George : \<font color="gray"\>present an IDP selector\</font\>
George --\> George\_mobile : \<font color="gray"\>select an IDP\</font\>
George\_mobile -\> IDP : autheticate IDP -\> George\_mobile : return the
SAML token George\_mobile -\> WAP : give WAP the SAML token WAP -\>
George\_mobile : issue the WeST George\_mobile -\> SP : transmit the
WeST (with timestamp and user signature) == service provision ==
George -\> George\_mobile : ask for music list George\_mobile -\> SP :
music list retrieval SP -\> George\_mobile : music list transmission
George\_mobile -\> George : music list display George -\> George\_mobile
: music file selection George\_mobile -\> SP : music file retrieval
SP -\> George\_mobile : music file transmission George\_mobile -\>
George : music file consumption
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=18197ce83f2d8ae5d04776be6604b20fb8a1849dcff820cc856458b7734b8922)

REMARKS:

Standard Webinos authentication protocol (SWAP?)

