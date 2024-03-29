Secure Elements API[¶](#Secure-Elements-API)
============================================

This is an API for accessing functions on contact or contactless smart
cards or similar devices using the Application Protocol Data Unit (APDU)
command response protocol, as defined by ISO 7816-4. In essence, the
command consists of a 4 byte header followed by up to 255 bytes of data.
The response contains a 2 byte header followed by up to 256 bytes of
data. The headers and data are specified in a suite of standards from
ISO and others. It also possible to develop custom secure elements using
Java cards from companies such as G&D and Gemalto.

The aim is to give system applications written in JavaScript, and
executing on a web run-time, a lightweight means to send commands to
secure elements and handle the responses using byte arrays (similar to
the existing Java API). Applications would have access to the crypto
APIs being developed in the W3C Web Crypto WG.

A brief introduction to APDU can be found at:

-   <http://en.wikipedia.org/wiki/Smart_card_application_protocol_data_unit>

The Java APDU API is described at:

-   <http://docs.oracle.com/javase/6/docs/jre/api/security/smartcardio/spec/>

Implementation[¶](#Implementation)
----------------------------------

There are two main hardware options:

-   USB smart card reader for contact based cards
-   NFC based reader for contactless cards

Java Smart Card development kits are available, and this would involve
interfacing Node with Java. The open source cross platform NFC library
**libnfc** can be used to access smart cards over NFC, but involves a
lot of low level details. For Linux, **PC/SC**, **OpenSC** and **IFD**
provide a convenient open source framework together with **libnfc** and
**Node.js**. A further idea is to use the Java SmartCard API on Android,
see:

-   [Secure Element Evaluation Kit for the Android
    platform](http://code.google.com/p/seek-for-android/wiki/UsingSmartCardAPI)

It appears that the Nexus S should work with that for UICC smart card
development, however, this involves reflashing the phone. Moreover, the
above page states that the minimum required SDK is API15 (Android 4.03)
which is yet to be supported for the webinos Android build. However, it
seems promising as a basis for demo purposes. We would also need some
sample smart cards with some interesting applets on them, although we
could in principle develop our own applets.

Examples[¶](#Examples)
----------------------

***Should code examples aim to be complete, or should they strive to
present the idea simply?***

The first step is to obtain a list of available APDU terminals:

      Webinos.apdu.requestTerminals(listener, success, fail);

      function fail (why)
      {
        console.log("Couldn't get list of APDU terminals: " + why);
      }

      function listen (terminals)
      {
        for (var i = 0; i < terminals.length; ++i)
        {
          var terminal = terminals[i];
          console.log("found APDU terminal: " + terminal.name);
        }
      }

Having picked a terminal and established that a card is present, you can
now connect to the card:

      terminal.connect(success, fail);

      function success ()
      {
        console.log("connected to card");
      }

      // connect operation will fail if card isn't present
      function fail (why)
      {
        console.log("couldn't connect to card: " + why);
      }

Once connected you can format a command, send it to the card, and
process the response:

      var command = terminal.createCommand();

      // initialize header bytes
      command.setHeaders(cla, ins, p1, p2);

      // set payload from byte array
      command.setPayload(payload);

      // and send it to the card
      terminal.transmit(command, success, fail);

      // handle the response
      function success (response)
      {
        console.log("response status: " + to_hex(response.status) +
                    " with " + response.payload.length + " bytes of data");

        // when done, disconnect
        terminal.disconnect();
      }

      // called if transmit failed
      function fail (why)
      {
        console.log("couldn't transmit command to card: " + why);
      }

The terminal status *present* property indicates whether a card is
present, and you can also set handlers for call backs when the card is
inserted or removed.

Secure Elements API - Complete WebIDL[¶](#Secure-Elements-API-Complete-WebIDL)
------------------------------------------------------------------------------

``` {.webidl .prettyprint}
/*
  You first need to find which terminals are available.
  Having found a suitable terminal, you can then test
  if a card is present, and connect to it, and then
  transmit a command and process the response, before
  closing the connection. Call backs are provided to
  signal when cards are inserted and removed.
*/
Webinos implements ApduProperty;

partial interface ApduProperty {
  readonly attribute APDU apdu;
};

interface APDU {
  // request list of APDU terminals
  void requestTerminals(ApduTerminalsCB listener, FailCB fail);
};

// call back for list of available terminals
callback ApduTerminalsCB = void (ApduTerminal[] terminals);

// call back if associated operation has succeeded
callback SuccessCB = void ();

// call back if associated operation has failed
callback FailCB = void (DOMString why);

// the properties and methods for terminals
interface ApduTerminal {
  // each terminal has a name
  readonly attribute DOMString name;

  // whether a card is present in the reader
  readonly attribute boolean present;  

  // call backs for card insertion and removal
  attribute ApduCardInsertedCB inserted;
  attribute ApduCardRemovedCB removed;

  // create an uninitialized APDU command
  ApduCommand createCommand();

  // send command and set listener for response
  void transmit(ApduCommand command,
                ApduResponseCB success, FailCB fail);

  // connect to the current card
  void connect(SuccessCB success, FailCB fail);

  // disconnect from the card
  void disconnect();
};

// call back notifying when card is inserted
// this will be called immediately if when setting
// call back the card is already present
callback ApduCardInsertedCB = void ();

// call back notifying when card is removed
callback ApduCardRemovedCB = void ();

// call back for APDU response
callback ApduResponseCB = void (ApduResponse response);

// initialization of APDU commands
interface ApduCommand {
  void setHeaders(byte cla, byte ins, byte p1, byte p2);
  void setPayload(byte[] payload);
  void setResponseLength(unsigned short length);
};

// the APDU response
interface ApduResponse {
  attribute unsigned short status;  // the 2 status bytes
  attribute byte[] payload;
};
```
