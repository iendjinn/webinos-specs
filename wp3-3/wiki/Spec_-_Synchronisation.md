Spec - Synchronisation[¶](#Spec-Synchronisation)
================================================

*This is work in progress and a complete specification will have to wait
until we have progressed further with implementation work.*

Introduction[¶](#Introduction)
------------------------------

Personal Zones are an abstraction layer encompassing your personal
devices and services. This layer is exposed as a local API in each
device as well as the personal zone hub that runs in the cloud. For this
abstraction layer to function, the shared context needs to be
synchronized across the zone. The context covers authentication data,
user preferences, device capabilities and environmental conditions, and
provides a means for applications to dynamically adapt to changes in the
context. The Personal Zone needs to function even when devices are
offline, or are temporarily unable to access the Internet.

Synchronisation data storage[¶](#Synchronisation-data-storage)
--------------------------------------------------------------

This involves a timestamped history of recent changes held in memory or
persisted as JSON.

Synchronisation Triggers[¶](#Synchronisation-Triggers)
------------------------------------------------------

Synchronization is triggered when a device first registers with the
zone, when it wakes up after being powered down, or it is switched back
to online mode, or when changes are signaled across the zone. Note that
changes may be buffered to improve network efficiency and to prolong
battery life.

Synchronisation algorithm[¶](#Synchronisation-algorithm)
--------------------------------------------------------

Synchronization can take place pairwise between devices, or between a
device and the personal zone hub. If the data model consists of
independent data items, one algorithm is to pick the latest version of a
given item. This involves an assessment of the clock skew between
devices, and assumes each webinos enabled device has a clock. If the
data items are not independent, the merged data needs to satisfy the
data integrity constraints. A transactional model of updates can help,
by providing the time of the latest transaction. This assumes each
device keeps a time stamped history of recent transactions. The
algorithm should further be designed to recover from error conditions
where a given device violates the integrity constraints.

The three way merge algorithm starts with the current state of the two
devices (A and B) and then determines the most recent common ancestor
(C), before identifying what further changes are needed to produce a
merged version (D). This will involve a means to resolve clashes, which
may involve giving precedence to one of the two devices.

![](220px-Three-way-merge-parallelgram.svg.png)\
*Courtesy of David Pattison*

Identification of the base version can be facilitated by a mechanism for
keeping a history of recent changes, and labeling versions of the data
set to be synchronized. This is easiest in a hub and spoke model, but
can be generalized for the peer to peer case when the hub is
unavailable.

Synchronisation protocol[¶](#Synchronisation-protocol)
------------------------------------------------------

This assumes that the data set to be synchronized can be described by a
hierarchy of data items. The protocol involves searching for a common
base version and then exchanging updates since that version. The updates
can be described in terms of add, delete, update, and move operations.
Updates are serialized as JSON, along with the version number and
timestamp. This is work in progress, and we expect to provide further
details as the work proceeds. The general feasibility of the approach
has been demonstrated by distributed revision control systems such as
mercurial, see:

-   Mercurial: The Definitive Guide, Bryan O'Sullivan, 1 January 2007,
    <http://hgbook.red-bean.com/>

