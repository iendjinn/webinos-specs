WP31 Event Handling[¶](#WP31-Event-Handling)
============================================

Events are essentially structured messages and could be delivered
reliably over TCP, or unreliably as unicast or multicast messages over
UDP. To cope with devices that are switched off or currently
inaccessible we also need to allow for store and forward distribution of
events. Events may be passed across Firewalls and NAT boundaries, and
via communication hubs. Events from different sources/services may be
multiplexed on the same stream for better utilization of network
resources.

Security Considerations[¶](#Security-Considerations)
----------------------------------------------------

Some things to think about:

### Authentication of events[¶](#Authentication-of-events)

Are events to be trusted and acted upon? This requires some form of
authentication. On local area networks, it may be reasonable to trust
all the devices present that can send events, and this speaks to the
point of "good enough security".

### Event integrity[¶](#Event-integrity)

Detecting when an event has been tampered with on route.

### Confidentiality of events[¶](#Confidentiality-of-events)

Ensuring that events are only read by the intended parties.

### Event orchestration[¶](#Event-orchestration)

Recognizing when an event has been sent out of sequence, and if acted
upon could result in harmful or wasteful behaviour.

### Denial of service attacks (event floods)[¶](#Denial-of-service-attacks-event-floods)

When a rogue device/service generates sufficiently large numbers of
events to have a harmful effect on the performance of other devices.

