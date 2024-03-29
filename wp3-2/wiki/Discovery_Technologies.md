Discovery Technologies[¶](#Discovery-Technologies)
==================================================

Each interconnect technology can have its own discovery mechanisms, and
some have several, each with their own terminology. Webinos will need to
provide an overlay that abstracts away from the variations and which
offers simple naming for end users and web developers. The overlay will
need to store the mapping from user friendly names to the underlying
data registered for the device and needed to communicate with it.

Interconnect technologies include:

-   3G, WiFi, WiMAX, Bluetooth, ZigBee, NFC, RJ45, USB, IEEE 1394, ...

Only some of these support IP directly. Webinos should provide a means
for an IP accessible device to proxy for devices that are not IP
addressable.

IP based networks[¶](#IP-based-networks)
----------------------------------------

For IP based networks, three such mechanisms are:

### Multicast DNS[¶](#Multicast-DNS)

Invented by Apple for simplifying the connection of devices in home
networks. The Apple implementation is called "Bonjour". An open source
equivalent is "Avahi". Devices start by randomly picking a link local IP
address in the range (169.254.\*.\*) and making an ARP request to see if
this address is already in use.

Devices assign themselves name in the ".local" domain, and will adjust
this if they detect other devices with the same name. Users can assign
human meaningful names with spaces in them. User agents query for
devices with multicast UDP requests. The devices check for a match and
respond with a multicast UDP packet with the IP address and port number,
the device's domain name, and a list of protocol and/or service names.
The device domain names use human meaningful conventions e.g. "Dave's
laptop.\_workstation.local". A nice feature is the ability for a device
to report on other devices including external services such as the BBC
news on the Web, or a hotel's local Web server giving details of the
hotel's services. Multicast DNS isn't designed to support tens of
thousands of devices, but this can be worked around with discovery hubs.

More information:

-   [Introductory
    talk](http://video.google.com/videoplay?docid=-7398680103951126462)
-   [Stuart Cheshire's website](http://www.multicastdns.org/)
-   [Avahi introduction](http://avahi.org/download/doxygen/)

On Linux, try mdns-scan or avahi-browse -a -v. This only found my Linux
workstation on my WiFi network and not the ADSL Modem, nor the Samsung
laser printer.

### Simple Service Discovery Protocol (SSDP)[¶](#Simple-Service-Discovery-Protocol-SSDP)

Invented by Microsoft and considerably more complicated than Multicast
DNS. SSDP is a UPnP and uses HTTP for notication announcements that give
a service type URI and a unique service name.

On linux try gssdp-device-sniffer. On my WiFi network this found the
ADSL Modem and the Laser printer, but not the Linux workstations.

#### Service Location Protocol (SLP)[¶](#Service-Location-Protocol-SLP)

Defined in RFC 2608 and supported by Hewlett-Packard's network printers,
Novell, and Sun Microsystems, but ignored by some other large vendors.
SLP works over UDP or TCP. On UDP devices listen on port 427 for\
multicast requests. Devices advertise themselves with a URI like

    service:printer:lpr://myprinter/myqueue

This may be supplemented by a list of attributes e.g.

     (printer-name=Hugo),
     (printer-natural-language-configured=en-us),
     (printer-location=In my home office),
     (printer-document-format-supported=application/postscript),
     (printer-color-supported=false),
     (printer-compression-supported=deflate, gzip)

If the data doesn't fit in a single packet, a flag is given that the
user agent can act on to request the SLP info via TCP. SLP also supports
discovery agents and presumably this helps with scaling up to larger
networks with bridged local networks.

### UPnP and DLNA[¶](#UPnP-and-DLNA)

On linux try upnp-inspector. On my network this found the ADSL Modem but
not my Laser printer.

Other interconnect technologies[¶](#Other-interconnect-technologies)
--------------------------------------------------------------------

### WiFi[¶](#WiFi)

For WiFi it is possible to detect access points and what kind of
encryption they are using if any, as well as devices operating in ad hoc
mode. It should be possible to detect device MAC addresses.

### USB[¶](#USB)

For USB see the source code for the Linux lsusb command. This lists the
bus and device number, the device ID and a human readable description
e.g. Logic3 / SpectraVideo plc A4Tech SWOP-3 Mouse, and Microdia Sonix
Integrated Webcam.

### Bluetooth[¶](#Bluetooth)

For Bluetooth, a scan shows the device ID and type, e.g. phone. This id
can be used as a proxy identifier for people, i.e. who is present in the
room or nearby. There is a small set of known device types, e.g. phone,
input device, headset, modem, computer, network, camera, printer or
video device. Users can provide a meaningful name for their device e.g.
"Me" as seen for a phone in a car that drove past my window!

