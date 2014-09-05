PZP[¶](#PZP)
============

In this specification we include information about:

-   PZP TLS client and server connection
-   PZP modes and states
-   Synchronise options
-   Revoked PZP

PZP TLS Client and Server Connection[¶](#PZP-TLS-Client-and-Server-Connection)
------------------------------------------------------------------------------

### TLS Servers on the PZP[¶](#TLS-Servers-on-the-PZP)

Port

Description

Incoming connections from PZPs (zone devices) as well as connections
from external (friend) PZPs.

Parameters

rejectUnauthorized = false

Trusted certificates

PZP certificates & trusted external PZH master certificates

Authentication

Entities with PZP certificates we don't recognise must go through the
peer-to-peer certificate exchange process, documented ...

Entities with PZP certificates from other zones are assumed to belong to
the user connected to the PZH CA certificate in the chain

Entities with PZP certificates from the personal zone are assumed to be
the same user

### Outgoing TLS connections on the PZP[¶](#Outgoing-TLS-connections-on-the-PZP)

Port

Description

Outgoing connections to other PZPs

Parameters

Trusted certificates

Just the certificate of the PZP we are contacting, if they are known. If
not, then just our own CA certificate.

Authentication

The remote party must use the certificate we are expecting, if we are
expecting one.

If the remote party is new (e.g. we have not connected to them before,
no certificate known) follow the peer-to-peer certificate exchange
process, documented ... )

The remote party must be a PZP, not a PZH.

The remote party user identity must be mapped to the identity of its
master CA certificate

PZP Identity[¶](#PZP-Identity)
------------------------------

Personal devices are assigned identity that is bound to their owner's
identity. An identity assigned to PZP is of form user identity followed
by the device name. This allows PZH to identify PZP id. PZP identity is
fetched during its connection to verify if signed PZP is joining in.

PZP Component Interaction[¶](#PZP-Component-Interaction)
--------------------------------------------------------

![](http://dev.webinos.org/redmine/attachments/2349/PZP_components_interaction.png)

PZP Modes - States[¶](#PZP-Modes-States)
----------------------------------------

Various different modes are supported by PZP and depending on modes it
could be in different states.

1.  Virgin Mode: This is a special case before device enrollment. Device
    is not connected to a PZH i.e. it is not certificated
2.  Hub Mode : This is a regular mode where PZP can connect to PZH i.e,
    it has all the certificates
3.  Peer Mode : This is a regular mode where PZP can connect to another
    PZP directly.

Depending on the above modes, device can be in different states:

1.  Not Connected
2.  Connecting
3.  Connected
4.  Disconnected

### Virgin Mode[¶](#Virgin-Mode)

This mode is a special case before device enrollment. This mode
specifies it has not connected to any other device and is not
certificated yet. When devices tries to connect the first time to PZH,
it will be in a Virgin Mode and after retrieving certificates it will go
into the hub mode.

Device in Virgin mode can be in these possible states:

1.  Not connected : Device has tried connecting to PZH but failed to get
    certificates or it has not tried connecting at all. It tries
    resolving DNS address and if successful go to connecting state.
2.  Connecting : Device has started connecting, depending on device this
    state could be longer (Mobile connection) or just a transition
    state. After timeout or in case of fail or socket hangup it should
    go back to not connected state. If successful go to connected state.
3.  Connected : This state will be small transition state from this
    state device stores certificate and if successful goes to hub mode,
    else goes back to not connected state.

If Virgin mode is successful device should be fully certificated with
its PZH.

![ [\*]--\> NotConnected NotConnected --\> Connecting : Successful
(Resolved IP Address) Connecting --\> NotConnected : Error / Timeout/
Hangup Connecting --\> Connected : Successful Connected --\> Hub :
Successful stored certificate
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=61fd0c4703755ee9d5fcb5309265605e5b98a34e36ed58d1024a8a49a0f5c569)

### Hub Mode[¶](#Hub-Mode)

Devices that are certificated are in hub mode. During first time connect
device goes from Virgin Connected to Hub Not connected state
automatically.

1.  Not connected: Devices that are not connected to PZH but has the
    certificate. It is not currently able to establish socket/IP
    connection with PZH. This could be due to PZH non-availability or
    device not having network connection (Example 3G Network Not working
    and device is not connected to WiFi)
2.  Connecting : Devices are triggered manually or automatically for
    connecting with the server. If successful device goes in connected
    state.
3.  Connected : Devices will be in connected state depending on the
    optimization. In case of error or timeout or hangup, it goes to
    disconnected state before going back to not connected state. When in
    connected state it can trigger peer connection to be initialized.
4.  Disconnecting: This is a small transition state where clean up
    operations will take place. After this device will go into not
    connected state

![ [\*]--\> NotConnected NotConnected --\> Connecting : Successful
Connecting --\> NotConnected : Error / Timeout/ Hangup Connecting --\>
Connected : Successful Connected -up-\> Disconnecting: Error/ Timeout/
Hangup Disconnecting-up-\> NotConnected: No valid connection
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=40394115007117a452153bfac8a4def415dbb9e424aaa32bb24d2e8bb7de1a54)

### Peer Mode[¶](#Peer-Mode)

Device can talk to each other if they are in near by proximity. The
advantage of this mode, they do not need to communicate via PZH and can
communicate with each other directly.

Triggers is done by pzpUpdate message sent by PZH when PZP is in
connected mode, which informs two PZP's about available PZP's and . If
two PZP's are available, they can initiate the connection between them.
To initiate this peer mode or not should be a preference setting. Once
peer is initiated it is separated from hub mode and lives in its own
state.

1.  NotConnected : Device is in hub mode but has not initiated
    connecting to other peers.
2.  Connecting : pzpUpdate message has been sent by PZH informing about
    peers under same PZH. If successful it goes to connected state.
3.  Connected : Two PZP's are connected to each other. In case of error
    it goes to disconnecting state
4.  Disconnecting: It is a transition state, after this device goes to
    not connected state.

![ [\*]--\> NotConnected NotConnected --\> Connecting : pzpUpdate
message by PZH Connecting --\> NotConnected : Devices are not available
or not from same PZH Connecting --\> Connected : Successful connected
Connected -up-\> Disconnecting: Error/ Timeout/ Hangup
Disconnecting-up-\> NotConnected : No valid connection
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=db51f72d6df7c5080d71ec69aef2cc4145348f5685a17bdd66054010e6055559)

### The Whole Picture[¶](#The-Whole-Picture)

![ [\*]--\> VirginMode state VirginMode { Virgin\_NotConnected -right-\>
Virgin\_Connecting : Successful (Resolved IP Address)
Virgin\_Connecting -up-\> Virgin\_NotConnected : Error / Timeout/ Hangup
Virgin\_Connecting -down-\> Virgin\_Connected : Successful
Virgin\_Connected -down-\> HubMode : Successful stored certificate }
state HubMode { [\*]--\> Hub\_NotConnected Hub\_NotConnected --\>
Hub\_Connecting : Successful Hub\_Connecting --\> Hub\_NotConnected :
Error / Timeout/ Hangup Hub\_Connecting --\> Hub\_Connected : Successful
Hub\_Connected --\> Hub\_Disconnecting : Error/ Timeout/ Hangup
Hub\_Disconnecting--\> Hub\_NotConnected : No valid connection } state
PeerMode{ Hub\_Connected --\> Peer\_NotConnected : Try connecting other
peers Peer\_NotConnected --\> Peer\_Connecting : pzpUpdate message by
PZH Peer\_Connecting --\> Peer\_NotConnected : Devices not available
Peer\_Connecting --\> Peer\_Connected : Successful connected
Peer\_Connected --\> Peer\_Disconnecting : Error/ Timeout/ Hangup
Peer\_Disconnecting --\> Peer\_NotConnected: No valid connection }
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=3568eb9a2dd16a04ba3dc1e49723350396bd1b818c3baaf146ca322e84a1703d)

Synchronise options[¶](#Synchronise-options)
--------------------------------------------

Users select what should be synchronised between devices and PZH. By
default items to synchronise are included in [Synchronisation](.html)
specification. Compared to PZH, PZP can specify if it also wants to
enable application and media synchronisation.

Revoked PZP[¶](#Revoked-PZP)
----------------------------

PZP that has been revoked and tries connecting with PZH and get error,
"CERT\_REVOKED", should trigger all data that is bind with PZH should be
removed. All synchronisation data should be also stopped with PZH.

