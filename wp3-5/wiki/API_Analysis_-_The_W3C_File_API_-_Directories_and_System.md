The W3C File API - Directories and System[¶](#The-W3C-File-API-Directories-and-System)
--------------------------------------------------------------------------------------

### Overview of API[¶](#Overview-of-API)

<http://www.w3.org/TR/2012/WD-file-system-api-20120417/>\
<http://www.w3.org/TR/file-system-api/>

Provides means to navigate file system hierarchies.\
Provides means to expose sandboxed sections of a user's local
filesystem.

### Threats[¶](#Threats)

#### API-Specific threats and misuse cases[¶](#API-Specific-threats-and-misuse-cases)

1.  This API could be used to navigate file system directories and other
    local applications directories.
2.  It can take file system resources inappropriately using storage
    request API.
3.  It can prevent legitimate data access moving local or remote files
4.  it can delete data removing local or remote files

For example, if access to critical file, like credential ones (e.g.
password or private key) is incorrectly allowed, Frankie (the alienated
script kiddie) may be able to delete them, in fact "disconnecting" the
device from the zone (since no longer able to authenticate versus the
other devices), just to make "funny" annoyance to "friends"

#### Threats based on remote invocation of this API from another device[¶](#Threats-based-on-remote-invocation-of-this-API-from-another-device)

#### Implementation threats and possible attacks[¶](#Implementation-threats-and-possible-attacks)

1.  Some operations invalidate the entry/blob used, e.g., remove. The
    implementation does not keep track of the entries/blobs returned,
    creating copies if the same entry/blob is requested multiple times,
    thus not propagating invalidation to all affected objects. The
    validation process is left to the underlying system. This could
    create integrity weaknesses (entries supposed to be deleted but yet
    there), and allow for persistent presence of entries, which could
    lead to information leakage if sensitive information are not
    properly deleted.

#### Threats to apps and developers using this API (E.g. Jimmy and Jessica)[¶](#Threats-to-apps-and-developers-using-this-API-Eg-Jimmy-and-Jessica)

Developers could experience some discrepancies between actual
implementation and expected behavior

1.  Certain UAs, i.e., Browsers. In order to manage origin-private
    filesystems within webinos, additional information is required
2.  Encoding Subtleties: The W3C File API
    specification(<http://www.w3.org/TR/FileAPI/>) requires the IANA:
    Character Sets to be supported
    (<http://www.iana.org/assignments/character-sets>). Internally,
    JavaScript uses UTF-16; the implementation uses UTF-8 and currently
    ignores any given encoding. This direct manipulation have to pay
    attention to not introduce encoding mismatch.
3.  Some operations, e.g., removeRecursively, could continue after the
    occurrence of an error or exception. This implementation works
    differently, aborting any operation that encounters an error or
    exception. Thus, an operation may partially succeed, e.g.,
    removeRecursively may remove some (up to the occurrence of an error
    or exception) but not all children of a directory. The app developer
    have to understand and check the success of those commands to avoid
    damage and leave the system in inconsistent state.\
    Presumably an inconsistent delete operation might result in
    private/valuable data not being deleted, which might cause
    embarrassment due to unexpected data disclosure. E.g., when selling
    an old device, or even affect valuable intellectual property.

#### Threats to device manufacturers, operators, other stakeholders[¶](#Threats-to-device-manufacturers-operators-other-stakeholders)

No obvious threats. Not much significantly, an attacker could navigate
the OS file system and move or delete OS files, causing OS instability
and bad user experience.

### Mitigations[¶](#Mitigations)

1.  For developers threats, provide examples which clarify how the API
    works for each ambiguous case
2.  Each application could have a filesystem section devoted to its own
    files. File system navigation, movement, copy and deletion outside
    this area should be denied, as well as "anonymous" file system
    access

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

X

X

Default allow (install time)

Widgets will need user consent at install time, but users will expect to
allow it (the tick-box will automatically be filled in).

Web pages will prompt for consent (Yes / No / Always) at runtime, this
preference will be saved.

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

Default deny (install time)

Widgets will require user consent at install time, but users will expect
NOT to allow it (the tick-box will automatically be empty).

Web pages will display a short notification at first-use saying that
access was denied, with a button to change settings

Silently deny

Applications will not be granted access to this API, and users will not
be asked at install time. This can only be modified using a policy
editor.

