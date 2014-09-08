Risk Management - Communication and Sequence Diagrams[¶](#Risk-Management-Communication-and-Sequence-Diagrams)
==============================================================================================================

-   [Risk Management - Communication and Sequence
    Diagrams](#Risk-Management-Communication-and-Sequence-Diagrams)
    -   [An application communicating with an API on a local PZP (Virgin
        PZP)](#An-application-communicating-with-an-API-on-a-local-PZP-Virgin-PZP)
    -   [An application communicating with an API on a local
        PZP](#An-application-communicating-with-an-API-on-a-local-PZP)
    -   [An application communicating with an API on a PZP on another
        device in the
        zone](#An-application-communicating-with-an-API-on-a-PZP-on-another-device-in-the-zone)
    -   [An application communicating with an API on a PZP on another
        device in a different
        zone](#An-application-communicating-with-an-API-on-a-PZP-on-another-device-in-a-different-zone)
    -   [Accessing the web interface of the PZH and authenticating the
        user](#Accessing-the-web-interface-of-the-PZH-and-authenticating-the-user)
    -   [Creating a PZH](#Creating-a-PZH)
    -   [Adding a new device to a personal
        zone](#Adding-a-new-device-to-a-personal-zone)
        -   [Through the web interface](#Through-the-web-interface)
    -   [Removing a device from a personal
        zone](#Removing-a-device-from-a-personal-zone)

An application communicating with an API on a local PZP (Virgin PZP)[¶](#An-application-communicating-with-an-API-on-a-local-PZP-Virgin-PZP)
--------------------------------------------------------------------------------------------------------------------------------------------

![](1a_virgin_PZP.png)

An application communicating with an API on a local PZP[¶](#An-application-communicating-with-an-API-on-a-local-PZP)
--------------------------------------------------------------------------------------------------------------------

![](1b_virgin_PZP.png)

An application communicating with an API on a PZP on another device in the zone[¶](#An-application-communicating-with-an-API-on-a-PZP-on-another-device-in-the-zone)
--------------------------------------------------------------------------------------------------------------------------------------------------------------------

![](2_PZP_inside_PZ.png)

An application communicating with an API on a PZP on another device in a different zone[¶](#An-application-communicating-with-an-API-on-a-PZP-on-another-device-in-a-different-zone)
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

![](3_PZP_outside_PZ.png)

Accessing the web interface of the PZH and authenticating the user[¶](#Accessing-the-web-interface-of-the-PZH-and-authenticating-the-user)
------------------------------------------------------------------------------------------------------------------------------------------

![ title Accessing the web interface of the PZH and authenticating the
user actor Alice participant Browser participant PZH participant IdP
autonumber Alice -\> Browser : Visit PZH Login URL Browser -\> PZH :
Request login page PZH -\> Browser : Request user OpenID credentials
Alice -\> Browser : login details Browser -\> IdP : OpenID login
process... IdP -\> Browser : OpenID Credentials Browser -\> PZH : OpenID
Credentials PZH -\> Browser : Success! Redirect to PZH landing page
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=461d87c0e1fa1938693176c03382f09cd8ec4b1ee888e364a45b9a8425a2bdb5)

Creating a PZH[¶](#Creating-a-PZH)
----------------------------------

![ title create PZH actor User as u participant "PZH Farm" as farm box
\#ivory participant "New PZH" as pzh participant "Certificate\\nManager"
as cm end box autonumber u -\> farm : authenticate create pzh farm -\>
pzh : create new PZH create cm pzh -\> cm : generate connection
certificates pzh -\> cm : generate CA certificate pzh -\> cm : generate
signed certificate
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=8c9620bdbb7a53d730733e5165adbb848b0b06ba485b006e1437fc8935290c0c)

Adding a new device to a personal zone[¶](#Adding-a-new-device-to-a-personal-zone)
----------------------------------------------------------------------------------

### Through the web interface[¶](#Through-the-web-interface)

This is a bit rough - need to check the OpenID stuff (it's not right at
the moment)

    Can this be integrated with other diagrams for TLS, OpenID, etc?

![ actor Alice participant Browser participant NewDevice participant
NewPZP participant PZH participant IdP activate Browser autonumber ==
User OpenID login process == Alice -\> Browser : Visit PZH Login URL
activate PZH Browser -\> PZH : Request login page PZH -\> Browser :
Request user OpenID credentials Alice -\> Browser : login details
activate IdP Browser -\> IdP : OpenID login process... IdP -\> Browser :
OpenID Credentials Browser -\> PZH : OpenID Credentials deactivate IdP
PZH -\> Browser : Success! Redirect to PZH landing page == Add new
device == Alice -\> Browser : Click "add new device" Browser -\> PZH :
Call addDevice.html PZH -\> PZH : Generate new device token, QR Code
PZH -\> Browser : token, QR Code image /' Browser -\> Alice : display
token and QR Code image '/ Alice -\> NewDevice : install PZP software
NewDevice -\> NewDevice : install PZP activate NewPZP Alice -\> NewPZP :
open configuration NewPZP -\> Alice : request PZH url and token
Alice -\> Alice : take picture of QR code, or copy token text deactivate
Browser Alice -\> NewPZP : token, PZH URL NewPZP -\> NewPZP : create
private key and self-signed certificate? NewPZP -\> PZH : TLS connection
established using (self-signed?, PZH device cert) NewPZP -\> PZH : token
PZH -\> PZH : check token validity PZH -\> PZH : remove token from valid
list == Issue certificate == PZH -\> PZH : create PZP certificate, add
to list of known devices PZH -\> NewPZP : certificate PZH -\> NewPZP :
terminate connection NewPZP -\> PZH : TLS connection established using
(PZP cert, PZH device cert)
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=63571cde3b7cf094ed2f0763e4ff3b2b1bf3ed7c43e7aea8784550235e68cf11)

Few comments from Andrea:

-   user OpenID credentials, or OpenID credentials might be a little
    misleading, since could mean the OpenID authentication token or the
    credentials to be provided to the IdP, maybe could be made a little
    more explicit.
-   A remark, if after point 11 (Generate new device token, QR code)the
    PZP does not connect, for how much time the token is maintained? is
    it possible to exploit this for a DoS, something like SYN flood
    attack?

Removing a device from a personal zone[¶](#Removing-a-device-from-a-personal-zone)
----------------------------------------------------------------------------------

![ actor Alice participant Browser participant BadDevice participant PZH
participant OtherPZPs activate Browser activate PZH autonumber == Login
process == Alice -\> Browser : Visit PZH Login URL Alice -\> Browser :
"... OpenID process .." == Revocation == Alice -\> Browser : Click "list
devices" Browser -\> PZH : Call listDevices.html PZH -\> Browser :
Display list of personal zone devices Alice -\> Browser : Click on the
"BadDevice" entry and click "Revoke". Browser -\> PZH : Call
revokeDevice( "BadDevice" ) PZH -\> PZH : Policy check (NOT IMPLEMENTED)
PZH -\> PZH : Find BadDevice's certificate PZH -\> PZH : Update CRL to
include BadDevice's certificate serial number PZH -\> PZH : Save CRL to
synchronised storage area PZH -\> PZH : Disconnect BadDevice if
currently connected PZH -\> PZH : Restart TLS stack PZH -\> Browser :
Show "done" deactivate Browser == Synchronisation == activate OtherPZPs
OtherPZPs -\> PZH : Connect to PZH OtherPZPs -\> PZH : Synchronisation
initiated PZH -\> OtherPZPs : Send Updated CRL OtherPZPs -\> OtherPZPs :
Store CRL, restart any TLS connections deactivate OtherPZPs == BadDevice
attempts to connect to PZH == activate BadDevice BadDevice -\> PZH : TLS
connection request PZH -\> BadDevice : Refused - certificate revoked
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=043e2d63ced6557d27f87bf4a85ba29a6fc95d92b4806cd54b8f6540c06b499f)

    This does not cover what happens to devices which rarely connect to the hub.  We need a misuse case or attack, as well as either a mitigation, or an explanation for why we're not doing it.  We could make CRL stapling for devices mandatory if they have not connected in a while... likelihood is that nothing will be fool-proof against a motivated attacker.

Few comments from Polito:

-   Minor: about revocation part, if I'm not wrong in the present
    implementation refers not to device but to PZP. Even if we can
    assume are the same entity in webinos money, I'm wondering if is
    worth to use PZP instead of device in the diagram
-   A request of clarification: what's the purpose in revocation part of
    "restart TLS stack", why is separate from the "restart any TLS
    connection" in synch part?

