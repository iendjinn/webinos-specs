Scenario 9 Sequence[¶](#Scenario-9-Sequence)
============================================

![ title : Scenario 9\\nGloria is already logged-in to Facebook\\nwhile
accessing a hosted webinos music service actor Gloria participant
"Gloria's mobile" as Gloria\_mobile participant WAP participant UR
participant SP note over Gloria, SP \#FF6666 : this scenario differs
form scenario 5 in the lack\\nof identification phase and IPD contact
phase autonumber == authentication == Gloria -\> Gloria\_mobile : insert
address of\\nService Provider (SP) Gloria\_mobile -\> SP : try to access
Service Provider SP -\> Gloria\_mobile : redirect to Webinos
Authentication Provider (WAP) Gloria\_mobile -\> WAP : ask for
authentication WAP -\> UR : ask for user account list UR -\> WAP :
return the user\\nIdentity Provider (IDP) list WAP -\> Gloria\_mobile :
return the IDP list note over SP, Gloria : here webinos runtime needs to
check if it already holds a\\nSAML token received from an IDP included
in the returned list Gloria\_mobile -\> WAP : give WAP the SAML token
WAP -\> Gloria\_mobile : issue the WeST Gloria\_mobile -\> SP : transmit
the WeST (with timestamp and user signature) == service provision ==
Gloria -\> Gloria\_mobile : ask for music list Gloria\_mobile -\> SP :
music list retrieval SP -\> Gloria\_mobile : music list transmission
Gloria\_mobile -\> Gloria : music list display Gloria -\> Gloria\_mobile
: music file selection Gloria\_mobile -\> SP : music file retrieval
SP -\> Gloria\_mobile : music file transmission Gloria\_mobile -\>
Gloria : music file consumption
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=810332431be9781608e727e23acddafb396f1f09b20287ffa60aa2181dda54db)

