Discovery[¶](#Discovery)
========================

Discovery means different things in different context. The aim of
discovery is to support devices to connect each other to create a
personal zone.

Different kinds of discovery handled in this specification:

-   Device Discovery:
    -   Finding devices which are in near proximity or local devices.
        Devices that can be searched using home networking protocols,
        short range bearers and local bearers are covered in this
        section.
    -   Connecting to pre-known address i.e. PZH URL. There is no
        discovery mechanism involved here, but part of connecting to
        other device in a personal network.
-   Service Discovery: Finding a webinos capable services. They could be
    found either via PZH or via Peer. These services are discoverable
    once device are connected. If not connected service discovery is
    local to a current device.
-   User Discovery: Search users URL to enable connecting them. This can
    be either using WebFinger or by searching OpenId URL.

Device discovery[¶](#Device-discovery)
--------------------------------------

Device discovery involves searching for devices to connect. The
discovery mechanism is applicable in peer to peer connection. The
mechanism to device which are remote is via PZH and does not involve any
discovery.

Webinos does not intend to introduce new device discovery mechanism but
provide a platform to use existing discovery mechanisms.

Different discovery mechanism in Webinos to enable finding local
devices:

### Home Networking Protocols:[¶](#Home-Networking-Protocols)

#### ZeroConf:[¶](#ZeroConf)

ZeroConf provides a mechanism to search local devices in the network. It
involves device that intend to be searchable and advertise about its
available service.

PZP's can look for ZeroConf service and the outcome is finding devices
that matches the service. Finding this service provide the IP address of
the system where this service is located. After this search the
connection is then established towards TLS Server running on peer PZP.
Only devices which has certificate signed from same PZH will be
connected to each other, otherwise connection is dropped if certificate
is not from same PZH.

In Webinos context, ZeroConf advertisement is to enable only when device
is not connected to PZH or if any existing peer to peer connection is
lost. This is intended to not cause power drainage on battery operated
devices.

Please note the service provided by ZeroConf is not similar to Webinos
Service.

TODO: Add ZeroConf discovery sequence diagram

#### UPnP[¶](#UPnP)

### Short Range Communication:[¶](#Short-Range-Communication)

#### Bluetooth[¶](#Bluetooth)

Webinos platform, please note

Bluetooth acts as a

#### WiFi Direct[¶](#WiFi-Direct)

Webinos service discovery[¶](#Webinos-service-discovery)
--------------------------------------------------------

Webinos Service is a functionality which can be discovered and executed
on a PZP. This service supports a set of APIs that allow connecting
devices to access them. The service communication between devices is
done over top of JSON-RPC. The invoking device acts as client and
receiving device acts as a server endpoint for executing RPC calls.

Webinos service model is based on certain device might not be capable of
providing a service, such as camera. It can make use of service on
another device to access its camera. The camera that's accessible is
still running on another device but functionality is invoked from other
device.

Service discovery has its lifecyle and require each service to perform
following steps to be discoverable and accessible:

-   Loading of service
-   Registration of service at PZP
-   Discovering a service
-   Binding service
-   API access

Please note services cannot be performed on devices that are not
connected.

User discovery[¶](#User-discovery)
----------------------------------

A section on T3.5 specifies about using web finger for finding different
users.

