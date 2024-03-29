The WAC devicestatus module[¶](#The-WAC-devicestatus-module)
------------------------------------------------------------

### Overview of API[¶](#Overview-of-API)

<http://specs.wacapps.net/devicestatus/index.html>

Provides information about various "aspects" of a device.

### Threats[¶](#Threats)

#### API-Specific threats and misuse cases[¶](#API-Specific-threats-and-misuse-cases)

1.  This API could be used, accessing IMEI code or other device
    properties, to fingerprint the user of a personal device.
2.  Operating System version and Web Runtime version can be used to
    exploit version-specific vulnerabilities.

#### Threats based on remote invocation of this API from another device[¶](#Threats-based-on-remote-invocation-of-this-API-from-another-device)

1.  Remote invocation could be used to access personal information. E.g.
    language (`OperatingSystem` aspect, `language` property), country
    (`CellularNetwork` aspect, `mcc` property), mobile operator
    (`CellularNetwork` aspect, `operatorName` property)
2.  It could be used to fine-tune remote DoS attack (e.g., the bettery
    level is a nice information to shape how much aggressive a DoS have
    to be). \#

#### Implementation threats and possible attacks[¶](#Implementation-threats-and-possible-attacks)

#### Threats to apps and developers using this API (E.g. Jimmy and Jessica)[¶](#Threats-to-apps-and-developers-using-this-API-Eg-Jimmy-and-Jessica)

1.  Wrong result of this API can influence the behavior of an
    application. The result can vary from an odd feeling from the user
    to severe application faults.
2.  If the API can provide unverified results (so, especially in case of
    untrusted browser or widget) the information with the user can be
    partially compromised. E.g., an App which want to display a contract
    and a disclaimer. If the devicestatus does not provide the correct
    size of the screen, the disclaimer could be not showed to the user
    since "visualized" in a zone out of the screen.
3.  If not wisely used, may lead to excessive power consumption (e.g.
    through watchPropertyChange() method)

#### Threats to device manufacturers, operators, other stakeholders[¶](#Threats-to-device-manufacturers-operators-other-stakeholders)

1.  If the API provides wrong results from the sensors/components,
    components manufacturers could have bad reputation due to the
    suspects they components do not work well.

### Mitigations[¶](#Mitigations)

1.  Main problem with this API, seems information leakage. Thus, remote
    access should be provided only to trusted entities, to avoid
    information leakage and attack finetuning
2.  Set adequate limit to watch the properties change

### Recommended default policy rules for applications[¶](#Recommended-default-policy-rules-for-applications)

  Code   Type
  ------ ------------------------------------------------------
  B-A    Browser-based, authenticated via TLS certificates
  W-R    Widget, authenticated using a recognised certificate
  W-U    Widget, unrecognised

Local Invocations:

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

Default allow (install time)

Widgets will need user consent at install time, but users will expect to
allow it (the tick-box will automatically be filled in).

Webpages will prompt for consent (Yes / No / Always) at runtime, this
can be just a warning rather than a prompt

x

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

Remote invocations:

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

x

Default deny (install time)

Widgets will require user consent at install time, but users will expect
NOT to allow it (the tick-box will automatically be empty).

Webpages will display a short notification at first-use saying that
access was denied, with a button to change settings

x

Silently deny

Applications will not be granted access to this API, and users will not
be asked at install time. This can only be modified using a policy
editor.

