Discovery Dependencies[¶](#Discovery-Dependencies)
==================================================

This sections describes interfaces between Discovery and following work
areas:

-   Event Handling

<!-- -->

-   ID Management

<!-- -->

-   Context Management

<!-- -->

-   Security & Policy

Event Handling[¶](#Event-Handling)
----------------------------------

Interfacing with event handling is mainly happening when [i]there are
changes in status of service or device, or in contextual aspects of a
service or device being used;[ii]a new service becomes available. The
new service could be a brand new one or could also possibly be a better
replacement for the existing service. Discovery requests event handling
to provide the following interfaces:

-   Device or service requester to register as event listener
    subscription to a certain event type
-   Device or service publisher to send event
-   Device or service requester to remove event listener

To be able to receive a certain class of notifications on the changes of
status or context information of the service or device being used or to
be informed about new services, the service or device requester needs to
act as an event listener. To do this, the requester can subscribe to the
event source with associated queries. Event source varies on different
use cases. For example, in the case that George would like to be
notified of the update on Paul's MP4s, an possible implementation is to
use pubsub as follows:

<div class="uml">actor George
George -> Public_Website:register/subscribe as event listener to receive "new MP4" notification

actor Paul
Paul -> Public_Website: Publish "new MP4" service

Public_Website -> George: Send "new MP4" notification

George -> Public_Website: remove event listener on "new MP4" notification</div>

In this case, the notification is pushed to George's personal Zone
Hub(PZH). George's PZH will work out whether George prefers this
notification being forwarded to the device he is using or to all his
devices. Alternatively, in the case that George’s media player on mobile
would like to know the updates of on the MP4 files on her PC, a zone API
shall be applied.

Some lower level discovery mechanisms have their own event handling
mechanisms. For example, in UpnP, a control point can be registered at a
service to be informed about device or service status changes. The
service sends event messages to all registered control points after
changing the value of a state variable. Event messages are transmitted
via the Generic Event Notification Protocol (GENA) [1]. In WebinOS,
service advertisement and service status update function shall be
exposed as JavaScript APIs or JavaScript Object. This needs to be
supported by a lower level mechanism. A wrapper on the top of lower
level event handling mechanism might be required in this case, for
example, exposing an HTTP or web sockets or similar server as part of a
plugin.

[1] J. Cohen, S. Aggarwal, Y. Y. Goland General Event Notification
Architecture Internet Draft, 2000.

ID Management[¶](#ID-Management)
--------------------------------

To discovery another person’s zone, in another word, to acquire proxy
object of another person’s personal zone, a user ID or information from
which a userID can be acquired should be provided. The user ID
information could be [i] email address; [ii] phone number; [iii] or just
a text file etc. In whichever way, when user ID is available, user
should be able to locate a query service to determine their zone hub,
further address devices based on their user information.

Due to the variation of interconnect mechanisms, device identity could
be represented in different forms such as IP address in UPnP, MAC
address in Bluetooth, some of them also presents friendly description,
e.g. Mark’s PC, at the same time. The developer, however, doesn't want
to know mechanism specific names or identities. This requires a genuine
Identity representation. Some discovery mechanisms, e.g. mDNS, allow
user assign meaningful names to devices to replace the default names. A
common naming scheme sitting on the top of different bearer schemes,
will allows us to hide the under layer implementation details.

Device names should only be unique to the user they are associated. A
good example on presenting userID and device ID is a full Jabber ID:

<alice@gmail.com>/mobile

