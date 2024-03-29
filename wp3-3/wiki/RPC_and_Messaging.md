RPC and Messaging[¶](#RPC-and-Messaging)
========================================

RPC[¶](#RPC)
------------

The functionality implemented for RPC is build on the top of the
services discovered. So once services are discovered, they can use
JSONRPC to invoke service. Services invoked could any other user device
or other user device for which we have connected before.

RPC implemented is based on following specification:
<http://www.jsonrpc.org/specification>.

Nothing specific to Webinos platform is done. All changes are specific
to aid Webinos Service Discovery

Messaging[¶](#Messaging)
------------------------

RPC to communicate to PZH or PZP or browser uses messaging. The
messaging functionality is to look for routing. It involves looking for
registered PZH or PZP. Based on the session information it tries to find
about connected PZH and PZP's. Various different addressing combination
are used to find different paths for connected device. By default
messages are forwarded to PZH if no route to PZP are found.

The other functionality of messaging preparing message that will be
addressable. The message identifier, from, to, resp\_to are added on top
of the message. This allows message to be routed on different system.

Implementation specific: PZP or PZH or browser side gets registered with
messaging. They register the sessionId, which is then used by messaging
to find route. Once message appears in PZP or PZH and is not specific to
PZH or PZP, it forwards it to messaging. Once messaging receives the
message and it has added all fields it forwards message to PZP/PZH which
holds socket information and routes the message.

TODO : Messaging, RPC and PZP sequence diagram\
TODO : Routing algorithm

Another messaging used in Webinos is PROP, these messages are used
internally for communication between PZP and PZP.

