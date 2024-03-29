Messaging API[¶](#Messaging-API)
--------------------------------

### Overview of API[¶](#Overview-of-API)

<http://dev.webinos.org/specifications/new/messaging.html>

Provides the capability to read, receive and send sms, mms, email and
instant messages.

### Threats[¶](#Threats)

#### API-Specific threats and misuse cases[¶](#API-Specific-threats-and-misuse-cases)

1.  an application (or remote user) can read user sms/mms/emails/im;
    they may contain sensitive data (for example important information
    about their personal life or work activities).
2.  an application (or remote user) can send sms/mms/emails; this may be
    used, for example, to subscribe the user to a paid service.
3.  an application can modify/replace the message or the recipient list
    before sending it, causing embarassment or other problems to the
    user.

#### Threats based on remote invocation of this API from another device[¶](#Threats-based-on-remote-invocation-of-this-API-from-another-device)

1.  Remote invocation of this API could have unexpected consequences as
    it might break the natural accountability that messaging would be
    expected to have. For example, an application might remotely invoke
    SMS functionality on a smartphone and the user, who is on their PC
    at the time, would only find out when they check their mobile
    device.
2.  Remote invocation could be used to impersonate the user for
    second-factor out-of-band authentication. For example, letting the
    application read an SMS created by a payment provider, or reading an
    email password reset message.

#### Implementation threats and possible attacks[¶](#Implementation-threats-and-possible-attacks)

#### Threats to apps and developers using this API (E.g. Jimmy and Jessica)[¶](#Threats-to-apps-and-developers-using-this-API-Eg-Jimmy-and-Jessica)

#### Threats to device manufacturers, operators, other stakeholders[¶](#Threats-to-device-manufacturers-operators-other-stakeholders)

1.  sending many sms/mms may consume user credit; this may cause
    disappointment with the operator or platform/application developer.

### Mitigations[¶](#Mitigations)

1.  access to send functionalities by default should be prompted every
    time (and denied to untrusted apps);
2.  should the prompt allow the user to check the message to be sure
    it's not modified by the application?

### Recommended default policy rules for applications[¶](#Recommended-default-policy-rules-for-applications)

The following features are defined for this api:

<http://webinos.org/api/messaging> (access to all functionalities)\
<http://webinos.org/api/messaging.send> (access to send message)\
<http://webinos.org/api/messaging.find> (access to find message)\
<http://webinos.org/api/messaging.subscribe> (access to message
subscription)\
<http://webinos.org/api/messaging.attach> (access to message attachment)

The control of message sending should be more restrictive than the
others.

  Code   Type
  ------ ------------------------------------------------------
  B-A    Browser-based, authenticated via TLS certificates
  W-R    Widget, authenticated using a recognised certificate
  W-U    Widget, unrecognised

Message send:

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

x

x

Default ask at runtime (every time)

Widgets will require user consent at runtime, every time. This fact will
be visible & modifiable at install time.

Web pages will prompt for consent (Yes / No / Always) at runtime

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

Other messaging methods:

B-A

W-R

W-U

Policy

Explanation (Widgets)

Explanation (Browser Apps)

Silently allow

Applications will be granted access to this API without user consent
being required. This can only be modified using a policy editor.

x

x

Default allow (install time)

Widgets will need user consent at install time, but users will expect to
allow it (the tick-box will automatically be filled in).

Web pages will prompt for consent (Yes / No / Always) at runtime, this
preference will be saved.

x

Default ask at runtime (one-shot)

Widgets will require one-off user consent at runtime. This fact will be
visible & modifiable at install time.

Web pages will prompt for consent (Yes / No / Always) at runtime, this
preference will be saved.

Default ask at runtime (every time)

Widgets will require user consent at runtime, every time. This fact will
be visible & modifiable at install time.

Web pages will prompt for consent (Yes / No / Always) at runtime

Default deny (install time)

Widgets will require user consent at install time, but users will expect
NOT to allow it (the tick-box will automatically be empty).

Web pages will display a short notification at first-use saying that
access was denied, with a button to change settings

Silently deny

Applications will not be granted access to this API, and users will not
be asked at install time. This can only be modified using a policy
editor.

