The W3C File API[¶](#The-W3C-File-API)
--------------------------------------

### Overview of API[¶](#Overview-of-API)

<http://www.w3.org/TR/2011/WD-FileAPI-20111020/>\
<http://www.w3.org/TR/FileAPI/>

Provides read-only file objects representation.

### Threats[¶](#Threats)

#### API-Specific threats and misuse cases[¶](#API-Specific-threats-and-misuse-cases)

1.  This API could be used to access local files (read only) containing
    sensitive data.

This could be exploited, for example, by Harold, who develops a free and
funny application which can provide the user a nice quote (from an
external DB of quotes) chosen on the information present on the file
system (e.g., retrieve the user name from the file system, and then look
for quotes which contains the same name). To do so, the application
access read the file system with the file API, whose behavior if not
restricted allow access even to sensitive system sections (e.g.
.webinos, where the private key is stored). Those private date can be
sent outside during the exchange with the external quote database.

#### Threats based on remote invocation of this API from another device[¶](#Threats-based-on-remote-invocation-of-this-API-from-another-device)

1.  This API could be used to access remote files (read only) containing
    sensitive data.
2.  It may induce a false feeling in the user, which may assume that
    installing the application on one device limits what it can access
    to just that device, enabling access of sensitive information on
    other devices of the zone.
3.  It is also a case of minimising the surprise to the end user - they
    may assume that installing the application on one device limits what
    it can access to just that device.

#### Implementation threats and possible attacks[¶](#Implementation-threats-and-possible-attacks)

1.  Arguments are not validated, the Jimmy and Jessica have to provide
    by itself the proper validation.

#### Threats to apps and developers using this API (E.g. Jimmy and Jessica)[¶](#Threats-to-apps-and-developers-using-this-API-Eg-Jimmy-and-Jessica)

1.  Certain UAs, i.e., Browsers. In order to manage origin-private
    filesystems within webinos, additional information is required
2.  Encoding Subtleties: The W3C File API
    specification(<http://www.w3.org/TR/FileAPI/>) requires the IANA:
    Character Sets to be supported
    (<http://www.iana.org/assignments/character-sets>). Internally,
    JavaScript uses UTF-16; the implementation uses UTF-8 and currently
    ignores any given encoding. This direct manipulation have to pay
    attention to not introduce encoding mismatch.
3.  unproper data read by applications could contain malicious code,
    exploit bugs and enable bad application behaviour

#### Threats to device manufacturers, operators, other stakeholders[¶](#Threats-to-device-manufacturers-operators-other-stakeholders)

1.  it could be a first step (information leakage, device
    fingerprinting) for another threat which influence device reputation
2.  reading malicious code that enable bugs could provide root access or
    system crash

### Mitigations[¶](#Mitigations)

1.  For developers threats, provide examples which clarify how the API
    works for each ambiguous case
2.  Each application could have a filesystem section devoted to its own
    files. File access outside this area should be denied. (This can be
    done via File API - Directories and System)
3.  Files (or application's file system area) should be encrypted to
    avoid data disclosure to unauthorized readers.
4.  Files' content should be parsed to avoid malicious code execution.

### Recommended default policy rules for applications[¶](#Recommended-default-policy-rules-for-applications)

  Code   Type
  ------ ------------------------------------------------------
  B-A    Browser-based, authenticated via TLS certificates
  W-R    Widget, authenticated using a recognised certificate
  W-U    Widget, unrecognised

Private Application file system

B-A

W-R

W-U

Policy

Explanation (Widgets)

Explanation (Browser apps)

Silently allow

Applications will be granted access to this API without user consent
being required. This can only be modified using a policy editor.

x

x

Default allow (install time)

Widgets will need user consent at install time, but users will expect to
allow it (the tick-box will automatically be filled in).

Webpages will prompt for consent (Yes / No / Always) at runtime, this
can be just a warning rather than a prompt

x

Default ask at runtime (one-shot)

Widgets will require one-off user consent at runtime. This fact will be
visible & modifiable at install time.

Webpages will prompt for consent (Yes / No / Always) at runtime, but the
PZP will remember the setting.

Default ask at runtime (every time)

Widgets will require user consent at runtime, every time. This fact will
be visible & modifiable at install time.

Webpages will prompt for consent (Yes / No / Always) at runtime

Default deny (install time)

Widgets will require user consent at install time, but users will expect
NOT to allow it (the tick-box will automatically be empty).

Webpages will display a short notification at first-use saying that
access was denied, with a button to change settings

Silently deny

Applications will not be granted access to this API, and users will not
be asked at install time. This can only be modified using a policy
editor.

Non private application file system

B-A

W-R

W-U

Policy

Explanation (Widgets)

Explanation (Browser apps)

Silently allow

Applications will be granted access to this API without user consent
being required. This can only be modified using a policy editor.

Default allow (install time)

Widgets will need user consent at install time, but users will expect to
allow it (the tick-box will automatically be filled in).

Webpages will prompt for consent (Yes / No / Always) at runtime, this
can be just a warning rather than a prompt

Default ask at runtime (one-shot)

Widgets will require one-off user consent at runtime. This fact will be
visible & modifiable at install time.

Webpages will prompt for consent (Yes / No / Always) at runtime, but the
PZP will remember the setting.

Default ask at runtime (every time)

Widgets will require user consent at runtime, every time. This fact will
be visible & modifiable at install time.

Webpages will prompt for consent (Yes / No / Always) at runtime

x

Default deny (install time)

Widgets will require user consent at install time, but users will expect
NOT to allow it (the tick-box will automatically be empty).

Webpages will display a short notification at first-use saying that
access was denied, with a button to change settings

x

x

Silently deny

Applications will not be granted access to this API, and users will not
be asked at install time. This can only be modified using a policy
editor.

