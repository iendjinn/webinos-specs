Remote Notifications and Messaging[¶](#Remote-Notifications-and-Messaging)
==========================================================================

Requirement name

API name

Interface

Method

Application event

API does not specify the predefined events

-

Application launch notification

Applauncher

-

-

Entity event subscription

Event Handling API

Webinos Event Enitity

addWebinosEventListener

Event delivery notification

Event Handling API

WebinosEvent

forwardWebinosEvent

Event delivery time limit

Event Handling API

WebinosEventCallbacks

on Timeout

Event destination

Event Handling API

WebinosEventCallbacks

onSending

Event distribution

Event Handling API

Dispatch webinos event

-

Event instance type

Event Handling API

createWebinosEvent, addWebinosEventListener

Event meta-data

Event Handling API

-

-

Event name conflict

Event Handling API

no webinos predefined events

-

Event payload

Event Handling API

WebinosEventCallbacks

dispatchWebinosEvent and forwardWebinosEvent

Event payload data

Event handling API

WebinosEventCallbacks

dispatchWebinosEvent and forwardWebinosEvent

Event source

Event Handling API

?

-

Event time

Event Handling API

WebinosEventCallbacks

referenceTimeout in dispath and forward

Event type subscription

Event Handling API

Webinos Event Enitity

addWebinosEventListener

Event type unsubscription

Event Handling API

Webinos Event Enitity

addWebinosEventListener

Message caching

Event Handling API

WebinosEventCallbacks

addWebinosEventListener allows multiple client to regiestr and dispatch
and forwards takes care of test

Multiple entity eventing

Event Handling API

?

?

New installation notification

Applauncher AppInstalled

-

-

Subscription

Missing API?

-

-

Unique event instance

Event Handling API

WebinosEventsInterface

createWebinosEvent

webinos event creator

Event handling API

WebinosEventsInterface

create Webinos Event

webinos event

Event handling API

Webinos Events

?

webinos update notification

Event handling API

webinosEvents ?

not present

