PZP Components & Deployment[¶](#PZP-Components-38-Deployment)
=============================================================

-   [PZP Components & Deployment](#PZP-Components-38-Deployment)
    -   [Introduction](#Introduction)
    -   [Webinos PZP Components](#Webinos-PZP-Components)
        -   -   [PZP Session Manager](#PZP-Session-Manager)
            -   [Certificate Manager](#Certificate-Manager)
            -   [Key Storage Manager](#Key-Storage-Manager)
            -   [Synchronisation Manager](#Synchronisation-Manager)
            -   [Messaging Manager](#Messaging-Manager)
            -   [Peer PZP Discovery](#Peer-PZP-Discovery)
            -   [Policy Manager](#Policy-Manager)
            -   [Context Manager](#Context-Manager)
            -   [RPC Manager](#RPC-Manager)
            -   [Service Discovery Manager](#Service-Discovery-Manager)

    -   [Platform specific implementation
        details](#Platform-specific-implementation-details)
        -   [Linux](#Linux)
            -   [Key Storage](#Key-Storage)
            -   [Peer PZP Discovery](#Peer-PZP-Discovery)
            -   [Deployment Diagram](#Deployment-Diagram)
        -   [Windows](#Windows)
            -   [Key Storage](#Key-Storage)
            -   [Peer PZP Discovery](#Peer-PZP-Discovery)
            -   [Deployment Diagram](#Deployment-Diagram)
        -   [Mac](#Mac)
            -   [Key Storage](#Key-Storage)
            -   [Peer PZP Discovery](#Peer-PZP-Discovery)
            -   [Deployment Diagram](#Deployment-Diagram)
        -   [Mobile - Android](#Mobile-Android)
            -   [Anode](#Anode)
            -   [Key Storage](#Key-Storage)
            -   [Peer PZP Discovery](#Peer-PZP-Discovery)
            -   [Deployment Diagram](#Deployment-Diagram)
        -   [IVI-system](#IVI-system)
            -   [Vehicle Bus Access](#Vehicle-Bus-Access)
            -   [Input Controler
                Management](#Input-Controler-Management)
            -   [Context manager not
                integrated](#Context-manager-not-integrated)
            -   [Deployment diagram](#Deployment-diagram)

Introduction[¶](#Introduction)
------------------------------

The webinos cross platform functionality is provided through the PZPs. A
PZP could be implemented in different ways, below is a description of
the [current](https://github.com/webinos/Webinos-Platform/tree/v0.6.0)
Webinos Platform implementation. The component diagram provides a
developer working on the webinos specification how different logical
entities of webinos work together and this should be implemented in all
webinos implementations. The deployment section is informative and does
not mandate implementing the PZP as described below. It is just to
provide specific details of the current implementation and give idea of
how different component interact and are deployed across devices.

The current PZP implementations of webinos are developed on top of the
[nodejs](http://nodejs.org/) platform. The main reason for selecting
nodejs was its capability to run in multiple platforms and ease in the
development. Nodejs is an event-driven application framework providing
non-blocking I/O, which is useful for developing large-scale server side
services and applications in JavaScript. Nodejs is build on top of
[v8](http://code.google.com/p/v8/) , Google's open source Javascript
rendering engine, which allows invoking native code calls from
JavaScript. The webinos code is partly implemented in JavaScript and
partly in the native code.

As part of running webinos, nodejs has been ported ~~on~~ to multiple
devices for car (Panda Board) and for home media (Set-top Boxes). The
sections below describe all the webinos components and then show the
specific changes in the platform for running nodejs and webinos code.
All the platforms listed below run on nodejs except for Android which
uses anode (<https://github.com/paddybyers/anode>), modified nodejs for
running on Android platform. Anode uses Java Bridge to allow Java code
instead of native C++ code to be called from JavaScript.The other
platform implementations use C++ to write native code.

Apart from nodejs, webinos uses several node modules. Some node modules
used are pure JavaScript code and some are mix of native code and
JavaScript code. To be able to run webinos, nodejs and the webinos
platform need to be installed. Instructions for installing and running
are described at <https://developer.webinos.org/>.

Webinos PZP Components[¶](#Webinos-PZP-Components)
--------------------------------------------------

The PZP architecture is segmented into smaller components to handle
different functionality. Each components' functionality is considered a
manager, and the dependency between components can be seen in figure 1.

![](pzp_components_interaction.png)\
Figure 1: PZP Components Interaction

These components perform actions in tandem and should be present in all
PZP implementations. The implementation for each component however could
be different and should match the webinos specification.

#### PZP Session Manager[¶](#PZP-Session-Manager)

PZP session manager is a combination of a TLS Client & Server and the
WebSocket Server. TLS server is responsible for creation of a TLS
between PZPs and WebSocket server create https session with WRT (Web
RunTime). Session manager also loads user preferences during reconnect.
In the current webinos implementation, this is implemented via
JavaScript with nodejs functionality.

##### TLS Server & Clients

The PZP uses a TLS Client to connect to the PZH. The PZP enrollment
mechanism joins a device into personal zone; the enrollment mechanism
results in a certificate that allows the PZP to connect to the PZH. Each
personal zone has one PZH and multiple PZPs. The PZP also runs a TLS
Server to allow other PZP's to communicate with the PZP. The PZP joining
a PZH, acts as a TLS server to all other PZP's which are already
connected to the PZH. The previous connected PZPs will only be a TLS
client, all subsequent PZP's can be both a TLS client and server. The
PZP in the personal zone can connect to each other because they are
signed from the same entity, the PZH. PZPs outside the personal zone can
connect to the PZP, if the PZH has exchanged certificates and the policy
permits.

##### WebSocket Server

The PZP provides a WebSocket server to acts as a bridge between the WRT
(Web RunTime) and the PZP. The role of WebSocket Server is to check the
application originator certificate signature and verify that the
application is allowed to communicate with the PZP, if the signature is
valid WebSocket server facilitates the application to communicate with
the PZP. WebSocket server also provides a way of loading the WRT
application that are stored in the PZP. Request originating from the WRT
communicates with the WebSocket Server and then the requests are forward
towards the PZP. For response received from the PZP, WebSocket server
matches the to field and send the response towards the application. In
current Webinos platform it uses the node module
[websocket](https://github.com/Worlize/WebSocket-Node) to establish the
websocket connection between the WRT and the WebSocket server.

In the Android implementation, Android Service is used instead of a
WebSocket server. For Android, WebSocket Server is implemented in Java.

#### Certificate Manager[¶](#Certificate-Manager)

Generates certificates for PZP's before device enrollment. The end
result of this step is a certificate sign request (CSR). This CSR is
then sent to the PZH to get signed. The reason for generating a CSR at
the PZP end is that the CSR needs to be signed with the PZP's private
key. CSR requires signing via private key, this private key remains in
PZP locally. Other functionality the Certificate Manager provides is
verifying certificates at the connection time with peer trusted PZP's.
In webinos platform it is implemented in the native code using the
[OpenSSL library](http://www.openssl.org/).

#### Key Storage Manager[¶](#Key-Storage-Manager)

Key Store stores the PZP private key and uses platform specific way of
handling key. The keys are fetched only during connection time. Keys are
fetched in memory only when required and unloaded when not required.
This is a native code implementation and uses different libraries on
different platforms.

#### Synchronisation Manager[¶](#Synchronisation-Manager)

Synchronises policies, certificate, user details and context object
between PZH and PZP. It is an implementation of the rsync algorithm and
applies a different chunk size depending on the contents of the file. In
the current webinos implementation it is implemented in the JavaScript.

#### Messaging Manager[¶](#Messaging-Manager)

It is responsible for routing packets, handling events and forwarding
packets to the Session Manager. It is a centralized place from where all
other managers invoke their functionality. In the current webinos
platform implementation it is implemented in the JavaScript.

#### Peer PZP Discovery[¶](#Peer-PZP-Discovery)

Peer PZP discovery mechanism is implemented in two ways in Webinos: the
PZH assisted discovery and the PZP local discovery where local PZP's are
searched in the local area network. In the PZH assisted discovery the
PZPs connection information, i.e. IP address and Port information, are
sent from the PZH to the PZP and then the PZP establish communication
with the other PZP. The PZP local discovery uses protocols such as
ZeroConf and UPnP to find other PZPs. The PZP in local area network
respond with the IP address and the connection is established with the
Peer PZP. Two PZPs can connect only if they have proper certificates in
place. If no proper certificate are in place, they could exchange a
temporary certificate exchange between PZPs, this certificate are not to
get the device in personal zone but to facilitate short communication
such as communication between devices in a meeting. Current
implementation is a native code implementation differing on all
platforms.

#### Policy Manager[¶](#Policy-Manager)

Checks and updates user policies for connection and on invocation of
services. The current webinos implementation is in native code, C++.

#### Context Manager[¶](#Context-Manager)

Intercepts and collect context data for webinos services. The current
webinos implementation is in JavaScript with support of the node module
[jsormdb](https://github.com/deitch/jsormdb).

#### RPC Manager[¶](#RPC-Manager)

RPC (Remote Procedure Call) allows Webinos APIs to invoke local or
remote Webinos Services. Webinos Services are implemented on the PZP end
and Webinos APIs are invoked from the WRT. The invocation of request and
execution of request can be on different devices. Using findService API,
a service can be found and then Webinos API are invoked to communicate
with the Webinos Services using RPC. At the invocation end, RPC creates
the payload to communicate with the device, and at receiving device RPC
forwards the payload to the service to execute request. The current
webinos implementation is in JavaScript.

#### Service Discovery Manager[¶](#Service-Discovery-Manager)

This manager provides support for the *findService* API and is basically
just used as a repository holding the current services information. The
current webinos implementation is a JavaScript implementation.

Platform specific implementation details[¶](#Platform-specific-implementation-details)
--------------------------------------------------------------------------------------

In the following sections the platform specific implementation details
an features will be elaborated:

-   Three PC-based implementations (Linux, Windows and Mac),
-   a mobile implementation (Android),
-   A Car implementation (IVI-system)

### Linux[¶](#Linux)

All the components described above are implemented in the Linux
platform. The platform specific implementation for Linux are in Key
Storage and Peer PZP discovery. All the other components are common on
all the platforms.

#### Key Storage[¶](#Key-Storage)

The webinos PZP key storage uses [Gnome
Keyring](https://live.gnome.org/GnomeKeyring/) to securely store private
keys. Gnome keyring unlocks the key when user login and key is
accessible till the user session is login. Once user logout, other users
of the system cannot access the keys. It is tightly coupled with the
user login to the platform.

Gnome keyring does not protect from other applications in the system
that tries to fetch keys when user is logged in, it is more up to user
how he handles session.

#### Peer PZP Discovery[¶](#Peer-PZP-Discovery)

Peer PZP discovery which is assisted by the PZH is same on all
platforms. What differs is how the local area network discovery
mechanism are implemented.

The Linux implementation uses the node module mdns which uses the avahi
library. Through this implementation PZP's can find another PZP when the
PZH is not reachable. [Avahi](http://www.avahi.org/) library is an
implementation of ZeroConf allowing to find devices that support service
"pzp". The device supporting the PZP returns the list of devices and
their IP address. The PZP tries connecting to all the devices, it will
be successful to only those device where it is enrolled.

#### Deployment Diagram[¶](#Deployment-Diagram)

![](pzp_deployment.png)\
Figure 2: PZP Deployment on Linux

### Windows[¶](#Windows)

The Windows implementation differs from Linux in the Key Storage
component and peer PZP discovery implementation.

#### Key Storage[¶](#Key-Storage)

This component has not been implemented yet on Windows, but one option
is to use the built-in [credential management
functions](http://msdn.microsoft.com/en-us/library/aa374731%28v=VS.85%29.aspx#credentials_management_functions)

#### Peer PZP Discovery[¶](#Peer-PZP-Discovery)

Peer to peer PZP discovery that is assisted by PZH follows the same
procedure on all platforms. Windows is not an exception.

In the case that the PZH is unreachable or direct peer to peer discovery
is preferred, mdns local discovery mechanism is adopted.

Windows uses [Apple's Bonjour
library](http://www.apple.com/support/bonjour/) for Windows to have mdns
functionality. Implementations of mdns for windows in Webinos is not
fully supported at Javascript level due to node's libuv does not provide
the necessary abstraction/flexibility to integrate Bonjour.

#### Deployment Diagram[¶](#Deployment-Diagram)

![](windows_pzp_deployment.jpg)\
Figure 3: PZP Deployment on Windows

### Mac[¶](#Mac)

The platform specific implementations for OS X are in the Key Storage
and Peer PZP discovery functionality. All the other components are
common on all the platforms.

#### Key Storage[¶](#Key-Storage)

Webinos PZP key storage uses the OS X Keychain Access to securely store
private keys. When a key is needed from the [Keychain Access OS
X](https://developer.apple.com/library/mac/#documentation/security/conceptual/keychainServConcepts/02concepts/concepts.html)
will prompt the user to ask if webinos is granted access to the
keychain. The user can choose if the access is granted only once or
always or if the access is denied.

#### Peer PZP Discovery[¶](#Peer-PZP-Discovery)

Peer PZP discovery which is assisted by PZH is identical on all
platforms. What differs is how the local area network discovery
mechanism are implemented.

OS X uses the node mdns module just like in Linux. But different from
Linux it does not use the avahi library but Apple's own
[mDNSResponder](http://opensource.apple.com/tarballs/mDNSResponder/)
that is present on Mac OS X systems by default. Through this
implementation PZP's can find other PZPs when the PZH is unreachable.

#### Deployment Diagram[¶](#Deployment-Diagram)

![](pzp_deployment_osx.png)\
Figure 4: PZP Deployment on Mac OS X

### Mobile - Android[¶](#Mobile-Android)

The Android implementation differs from Linux in the following aspects:

#### Anode[¶](#Anode)

[Anode](https://github.com/paddybyers/anode) is a beta framework for
running node.js applications on Android. There are two main parts of
Anode framework:

-   a port of node.js to the Android OS and libraries.
-   a set of Android projects that provide the integration with the
    Android frameworks.

Anode builds to an Android application package (.apk) that encapsulates
the node.js runtime and can run node.js applications through an
intent-based API.

#### Key Storage[¶](#Key-Storage)

This component has not been implemented yet on Android.

#### Peer PZP Discovery[¶](#Peer-PZP-Discovery)

Android follows the same procedure for PZH-assisting peer to peer PZP
discovery.

In the case that the PZH is unreachable or direct peer to peer discovery
is preferred, mdns local discovery mechanism is adopted by Android.

Webinos has developed its own mdns discovery implementations and exposed
as Javascript APIs to web developers. This set of APIs are available for
applications and webinos core components.

#### Deployment Diagram[¶](#Deployment-Diagram)

![](pzp_deployment_android.png)\
Figure 5: PZP Deployment on Android

### IVI-system[¶](#IVI-system)

The IVI-system implementation differs from Linux in the following
aspects:

#### Vehicle Bus Access[¶](#Vehicle-Bus-Access)

In order to provide access to vehicle data the webinos\_pzp includes a
JavaScript wrapper to access the Vehicle Data Provider, which is a
separate module running on the vehicle platform. The Vehicle Data
provider interacts with the Media Oriented Transport System (MOST) bus.

#### Input Controler Management[¶](#Input-Controler-Management)

As the vehicle demonstrator has a standard BMW iDrive ergo commander to
control the webinos applications, the vehicle platform has an additional
executable, which listens on input events from the Ergocommander and
converts the CAN message into keyboard events which are passed to the
browser.

#### Context manager not integrated[¶](#Context-manager-not-integrated)

As the vehicle platform does not integrate the context manager due to
limited resources on the embedded hardware

#### Deployment diagram[¶](#Deployment-diagram)

The following deployment diagram illustrates the highlighted changes on
the vehicle deployment.

![](PZP_automotive.png)\
Figure 6: PZP Deployment on in-car system

