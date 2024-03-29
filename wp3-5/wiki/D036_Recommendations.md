Recommendations[¶](#Recommendations)
====================================

This section gives advice and recommendations to stakeholders
responsible for certain aspects of the webinos environment in order to
minimize security and privacy concerns. These are in addition to general
best practice guidelines on security and privacy. A list of webinos
stakeholders can be found in the ([Glossary](Glossary.html))
accompanying the main D3.3 specification.

For Identity Providers[¶](#For-Identity-Providers)
--------------------------------------------------

Identity providers are highly trusted with the webinos architecture as
their ability to authenticate users is relied upon to protect the
personal zone. Compromise of an OpenID identity used to manage a
personal zone would result in a potential loss of data, personal privacy
and could be used to perform a number of other attacks.

We therefore recommend that identity providers do the following:

1.  Implement OpenID PAPE extensions. This allows webinos to dictate
    when a user should re-authenticate, rather than relying on the
    OpenID provider to correctly implement authentication caching.
2.  Provide and encourage two-factor authentication. The threat of
    identity theft and compromise of OpenID credentials is significant
    and hard for webinos to mitigate. A solution, however, might involve
    integrating the webinos PKI infrastructure with OpenID in order to
    provide a second factor of user identity.
3.  Provide recovery mechanisms based on secure out-of-band
    communication methods. This will help avoid attacks based on a
    malicious user recovering the credentials of another person, an
    attack we cannot mitigate in webinos.
4.  Follow best-practice guides ([OpenIDBest](OpenIDBest.html)) to avoid
    insecure implementations of OpenID protocols.

For PZH Providers[¶](#For-PZH-Providers)
----------------------------------------

Personal zone hub providers are trusted in the webinos architecture with
the ability to control a user's personal zone. In the T3.3 informative
sections on PZH deployment we describe several potential architectures
which can mitigate some of the trust placed in webinos personal zone
hubs.

For a provider attempting to offer services and preserve user privacy
and security, we suggest the following:

1.  Store all user data on encrypted disks. Do not allow any third
    parties to access this data directly.
2.  Monitor incoming connection traffic to detect potential attacks on
    web interfaces and PZH TLS servers.
3.  Only support OpenID providers who follow the recommendations
    specified above
4.  Support trusted hardware modules in order to secure keys and
    credentials

For Device Manufacturers[¶](#For-Device-Manufacturers)
------------------------------------------------------

1.  Provide user-to-device authentication methods which will mitigate
    threats from devices places in shared environments. For example,
    providing PINs or locks that are easy to use yet provide some real
    resistance from casual attackers. This is important in webinos as
    access to the device is sufficient, in some cases, to access part of
    the entire personal zone.
2.  Provide disk encryption by default. Webinos makes no attempt to
    encrypt application data, recognising that this is something that
    can be provided more effectively by devices. Enable the disk
    encryption facilities of the device before shipping it with webinos.
3.  Use an operating system that provides process isolation. The webinos
    platform assumes that processes are isolated from each other and is
    more secure if each application has its own area of protected
    storage. This can be found in operating systems such as Android and
    iOS, and can be configured in Linux using Linux Security Modules
    such as SELinux and AppArmor. Native malware is a threat that
    webinos cannot protect against, and therefore operating systems must
    provide isolation between processes and data used by each process.
4.  Provide data backup solutions.

For Application Developers[¶](#For-Application-Developers)
----------------------------------------------------------

There are numerous guidelines and recommendations for the secure and
privacy-preserving development of web applications. Secure software
development is a topic covered by hundreds of books and articles which
we do not repeat here. However, we suggest that developers are aware of
the following existing literature:

-   The OWASP development guide ([OWASP-Guide](OWASP-Guide.html))
-   W3C "Web Application Privacy Best Practices" -
    ([W3CAppPriv](W3CAppPriv.html))

We also encourage application developers to request as few webinos
feature permissions as possible, and to register their applications with
well-known app stores.

Finally, for hosted applications we recommend the WebSand project
([WebSand](WebSand.html)) as a source of useful security guidance.

For Users[¶](#For-Users)
------------------------

Users of webinos should be aware that webinos is only as secure as the
various components and entities it relies upon. As such, users should be
careful in choosing:

1.  The devices they use webinos with. If webinos is to be used
    securely, devices should provide disk encryption. Devices should
    also either be used only by the zone owner, or offer user accounts
    which separate users from each other. For shared devices, such as
    TVs, users should be careful to avoid granting them too many
    permissions
2.  The OpenID provider they use. We recommend the use of an OpenID
    provider who offers two-factor authentication
3.  The PZH Host they choose. PZHs are highly trusted within the
    architecture, and users should not choose a provider they do not
    believe to be reliable
4.  The applications they grant privileges to. Applications are a major
    source of threats, and we recommend that applications are not
    granted privileges without reason.

However, most of these responsibilities should not be shouldered by the
user as (in many cases) they are not in a good position to make informed
decisions. As such, these recommendations should primarily be followed
by device manufacturers, service providers and app stores.

