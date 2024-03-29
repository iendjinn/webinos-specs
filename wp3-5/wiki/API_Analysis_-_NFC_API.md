NFC API[¶](#NFC-API)
--------------------

### Overview of API[¶](#Overview-of-API)

</t3-4/wiki/NFC_API>

Allows applications to read and write to NFC tags, to push messages to
other NFC devices, and to establish a temporary bidirectional
asynchronous message channel between the host device and another. NFC
uses short range inductive radio frequency communication. The range is
typically of the order of 4 centimetres. NFC tags lack batteries and are
powered through inductive coupling. The webinos phase 2 API doesn't
(yet) support more advanced techniques such as APDU messages for contact
and contact-less smart cards, as used for electronic payments.

### Threats[¶](#Threats)

#### API-Specific threats and misuse cases[¶](#API-Specific-threats-and-misuse-cases)

1.  Privacy and confidentiality loss - An attacker could place a hidden
    antenna near enough to listen into the communication protocol
    between the NFC devices as NFC communications is typically
    unencrypted. In practice with a hand held NFC device like a mobile
    phone, and a handheld NFC tag (e.g. a smart card), the risk is low.
2.  Loss of an NFC Tag - if data is held on an NFC Tag in an unencrypted
    form, there is a risk of the Tag falling into the wrong hands. This
    is analogous to losing a metro travel payment card (e.g. London's
    Oyster card), a credit card or a security access card used for
    access to restricted premises. A related scenario involves the loss
    of your NFC enabled smart phone.

#### Threats based on remote invocation of this API from another device[¶](#Threats-based-on-remote-invocation-of-this-API-from-another-device)

For this to work, the user would have to be persuaded to cooperate with
physically moving the NFC device close to the other device, e.g. a phone
or tag.

#### Implementation threats and possible attacks[¶](#Implementation-threats-and-possible-attacks)

NFC is sometimes used to exchange credentials for securing other
protocols, e.g. WiFi networks or Bluetooth connections. NFC has also
been suggested as part of the process for inducting new devices into the
user's personal zone. Unencrypted communication between NFC devices
could be used to compromise security, however, see above for the
practical issues in doing so.

#### Threats to apps and developers using this API (E.g. Jimmy and Jessica)[¶](#Threats-to-apps-and-developers-using-this-API-Eg-Jimmy-and-Jessica)

NFC can be used as part of payment solutions, and web developers may
feel unwarranted confidence in the security of NFC devices. We need to
explain the limitations of basic NDEF NFC devices and point people are
more secure solutions where appropriate, e.g. the use of NFC-SEC and
APDU.

#### Threats to device manufacturers, operators, other stakeholders[¶](#Threats-to-device-manufacturers-operators-other-stakeholders)

1.  Availability - NFC is low power and not a big factor in battery
    life.

### Mitigations[¶](#Mitigations)

The wireless connection can be safeguarded through the use of NFC-SEC as
defined by ECMA-385 and ECMA 386, see:

-   [ECMA-385](http://www.ecma-international.org/publications/standards/Ecma-385.htm)
-   [ECMA-386](http://www.ecma-international.org/publications/standards/Ecma-386.htm)
-   [ECMA TC-47 NFC-SEC White
    paper](http://www.ecma-international.org/activities/Communications/tc47-2008-089-Rev1.pdf)

*Note: ECMA 385, 385 have been republished as ISO/IEC 13157-1 and -2,
respectively.*

NFC-SEC provides for a Diffie-Helman secure key exchange, allowing NFC
devices to set up a secure communication path. In principle, this could
be subject to a man-in-the-middle attack, but that would be hard to
achieve in practice due to the nature of the very short range radio
frequency communication paths involved.

Further work is needed to explore how to integrate support for NFC-SEC
in webinos, as this is dependent on the availability of support by the
underlying libraries, e.g. libnfc and the Android SDK.

### Recommended default policy rules for applications[¶](#Recommended-default-policy-rules-for-applications)

The need for users to explicitly bring NFC devices close together acts
as barrier to silent abuse of the NFC APIs, as a result user consent
shouldn't be requested at run-time, except when the system needs to
re-format an existing Tag. It may still be a good idea to ask users for
consent to at install time as a reminder of the capability of the
application in question.

The policy language could be designed to limit the APIs applications can
use according to the need, e.g. if an application only needs to share
personal contact data (an electronic business card) then it could be
restricted to reading and writing such data to NFC devices/tags. The
policy language could further limit the capabilities to applications
that are authenticated by the host platform.

  Code   Type
  ------ ------------------------------------------------------
  B-A    Browser-based, authenticated via TLS certificates
  W-R    Widget, authenticated using a recognised certificate
  W-U    Widget, unrecognised

B-A

W-R

W-U

Policy

Explanation (Widgets)

Explanation (Browser Apps)

Silently allow

Applications will be granted access to this API without user consent
being required. This can only be modified using a policy editor.

Default allow (install time)

Widgets will need user consent at install time, but users will expect to
allow it (the tick-box will automatically be filled in).

Web pages will prompt for consent (Yes / No / Always) at runtime, this
preference will be saved.

Default ask at runtime (one-shot)

Widgets will require one-off user consent at runtime. This fact will be
visible & modifiable at install time.

Web pages will prompt for consent (Yes / No / Always) at runtime, this
preference will be saved.

Default ask at runtime (every time)

Widgets will require user consent at runtime, every time. This fact will
be visible & modifiable at install time.

Web pages will prompt for consent (Yes / No / Always) at runtime

x

x

x

Default deny (install time)

Widgets will require user consent at install time, but users will expect
NOT to allow it (the tick-box will automatically be empty).

Web pages will display a short notification at first-use saying that
access was denied, with a button to change settings

Silently deny

Applications will not be granted access to this API, and users will not
be asked at install time. This can only be modified using a policy
editor.

