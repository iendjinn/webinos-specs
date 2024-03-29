microPZP Use cases[¶](#microPZP-Use-cases)
==========================================

The following illustrative example use cases for a microPZP.

Portable navigation device[¶](#Portable-navigation-device)
----------------------------------------------------------

A single-purpose device, typically owned and operated by a single user,
capable of supporting a limited set of remote services.\
The APIs exported are:

-   Geolocation;
-   Route database : exposed as a filesystem, a set of files each with a
    set of waypoints;
-   Recorded journey database : exposed as a filesystem, a set of files
    each with a set of waypoints and timestamps.

This is not a full PZP since there is not aspiration to be able to run
user apps; but it is nonetheless a personal device with useful services
that can be exposed in addition to simple geolocation; and the user will
wish to have control over who can access those additional services.

As a mapping device with processor and memory resources commensurate
with processing and displaying map data,, this device would be
TLS-capable, operating over Wi-Fi or BT PAN. It exposes a REST
configuration API in addition to the JSON-RPC API, and has a local admin
web app with limited policy editing capability. A companion phone or PC
application performs setup/enrolment through the admin API.

Multipurpose street furniture[¶](#Multipurpose-street-furniture)
----------------------------------------------------------------

This would be a fixed device embedded in a permanent street fixture such
as a street light. It contains a range of sensors for monitoring the
ambient environment (power, light, temperature, accelerometer/wind, air
quality), and also contains a remotely controllable camera.

The sensors are openly accessible for all webinos peer clients, but
control of, and access to data from the camera is subject to permission
and is only allowed from peer devices in the same Personal Zone.

A large, dynamic population of such installations operates using a mesh
peer-to-peer network. This device is TLS-capable.

It exposes a REST configuration API in addition to the JSON-RPC API, and
has a local admin web app with limited policy editing capability.

This could be architected as a set of sensors and actuators attached to
a separate full PZP, but it is more appropriate for this to be a
microPZP, given that it has multiple sensors that would be enrolled and
configured as a single operation, and the device can communicate
autonomously.

Industrial monitoring and control[¶](#Industrial-monitoring-and-control)
------------------------------------------------------------------------

A range of devices exists in a large industrial facility. These are all
small, low powered and specialized devices – pollutant monitoring,
temperatures, pressures, IR intrusion sensors, door and airlock
controls, etc. Each device may expose a generic sensor API but could
equally implement a specialized API for its specific purpose.

All devices communicate across the facility using a ZigBee mesh network
and are not TLS-capable.

These devices could possibly be architected as individual sensors and
actuators, but this is problematic because it requires the mediating PZP
to have a local implementation of each API for every device. New devices
that implemented new functionality would not be able to be added until
there was a corresponding software update to the PZP to add awareness of
the new API.

Architecting these devices instead as tethered microPZPs puts
device-specific behavior into the device and the client apps, and avoids
any device type-specific functionality in the proxy. As tethered devices
there must be a proxy; the proxy is able to discover new devices on the
mesh autonomously and can enrol those devices automatically as they come
online.

The proxy exposes the admin interface for each device via an integrated
REST service, which allows all devices to be controlled from anywhere
within the facility.

