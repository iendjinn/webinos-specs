The W3C calendar module[¶](#The-W3C-calendar-module)
----------------------------------------------------

### Overview of API[¶](#Overview-of-API)

<http://www.w3.org/TR/2011/WD-calendar-api-20110419/>

The Calendar API defines a high-level interface to access Calendar
information such as events, reminders, alarms and other calendar
information. The API itself is designed to be agnostic of any underlying
calendaring service sources.

Security and Privacy considerations are already described in [this part
of the
specification](http://www.w3.org/TR/2011/WD-calendar-api-20110419/#security-and-privacy-considerations)
.

### Threats[¶](#Threats)

#### API-Specific threats and misuse cases[¶](#API-Specific-threats-and-misuse-cases)

1.  Distribution of user calendar details - privacy issues abound.
    Sharing with unauthorised parties may result in embarrassment, loss
    of income (meeting information may be valuable to businesses) or
    impact on the safety of the end user.
2.  Targeted advertising based on calendar event information
3.  Stalking possible if the wrong person is given access to calendar
    entries
4.  [Misuse
    case](/wp2-8/wiki/Risks_misusecases#Navigation-Misuse-Case) -
    Calendar details shared over unprotected communication medium and
    accessed by unauthorised parties, allowing them to rob the victim
    when they know he will be at an appointment.
5.  Not all calendars are created equally - some will be used for
    business, others personal, others are common events. Granting access
    to one should not automatically grant access to them all.
6.  The details of contacts who have been added to meetings or
    appointments might be revealed through use of the calendar API in an
    unexpected way.

#### Extended threats based on editing calendars[¶](#Extended-threats-based-on-editing-calendars)

1.  Spam through an unauthorised application adding calendar entries
2.  Missing appointments or loss of information due to an application
    deleting entries or adding too many unwanted entries

#### Threats based on remote invocation of this API from another device[¶](#Threats-based-on-remote-invocation-of-this-API-from-another-device)

1.  Peter might allow his application access to the Calendar on his PC,
    knowing that there is nothing important in it. However, it then has
    access to his mobile phone calendar, which is much more personal and
    sensitive.
2.  There could be an unexpected ripple-effect when deleting a calendar
    entry - deleting it on one calendar could impact all calendars on
    all devices unexpectedly.

#### Implementation threats and possible attacks[¶](#Implementation-threats-and-possible-attacks)

#### Threats to apps and developers using this API (E.g. Jimmy and Jessica)[¶](#Threats-to-apps-and-developers-using-this-API-Eg-Jimmy-and-Jessica)

-   The Calendar API might return enormous amounts of data, causing any
    Web Application to crash or fail.
-   Calendar data from public calendars might be used to perform XSS or
    XSRF attacks.

#### Threats to device manufacturers, operators, other stakeholders[¶](#Threats-to-device-manufacturers-operators-other-stakeholders)

### Mitigations[¶](#Mitigations)

These apply:
<http://www.w3.org/TR/2011/WD-calendar-api-20110419/#security-and-privacy-considerations>

1.  User consent required for accessing each calendar
2.  Separation of calendars is important - access to one calendar should
    not imply access to others
3.  Could the API support "busy/free" invocation methods rather than
    precise information about each event? (this would involve a
    modification to the API)
4.  Granularity is important
    1.  Applications should state how much calendar information they
        will request and why.
    2.  permission might be granted just for an application to see
        whether a particular time is free or busy, but not any details
    3.  permission might be granted to view calendar items but not edit
        (editing is not technically in the specification)

5.  Revocation of consent is necessary.
6.  Suggest a three-phase policy per calendar: "allow all", "allow view
    busy/free", "deny"

### Recommended default policy rules for applications[¶](#Recommended-default-policy-rules-for-applications)

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

X

X

Default ask at runtime (one-shot)

Widgets will require one-off user consent at runtime. This fact will be
visible & modifiable at install time.

Web pages will prompt for consent (Yes / No / Always) at runtime, this
preference will be saved.

Default ask at runtime (every time)

Widgets will require user consent at runtime, every time. This fact will
be visible & modifiable at install time.

Web pages will prompt for consent (Yes / No / Always) at runtime

X

Default deny (install time)

Widgets will require user consent at install time, but users will expect
NOT to allow it (the tick-box will automatically be empty).

Web pages will display a short notification at first-use saying that
access was denied, with a button to change settings

Silently deny

Applications will not be granted access to this API, and users will not
be asked at install time. This can only be modified using a policy
editor.

Rationale: accessing a calendar ought to require explicit consent, and
most pages ought to deny it by default. For those pages and widgets
which are from known sources, it is reasonable to expect that consent is
likely to be granted after one question.

