WAC Comparison[¶](#WAC-Comparison)
==================================

This page summarises how webinos uses the WAC security and privacy
specifications and highlights any differences. The following sections
headings are taken from the [WAC 2.0
specifications](http://specs.wacapps.net/2.0/feb2011/core/widget-security-privacy.html)

3. Widget Security and Privacy[¶](#3-Widget-Security-and-Privacy)
-----------------------------------------------------------------

### 3.1. Authentication[¶](#31-Authentication)

#### 3.1.1 AppStore Authentication[¶](#311-AppStore-Authentication)

Notes:

-   Webinos phase 1 does not include details of an AppStore or
    AppStoreClient, and no certification is assumed.
-   Widget downloads may be from non-https sites assuming their
    manifests include signatures from trusted parties.

#### 3.1.2 WRT Authentication[¶](#312-WRT-Authentication)

"WRT authentication ensures that a WAC-certified client is being used,
e.g. to download WAC widgets or use network services provided by WAC
members."

-   There may be several webinos implementations. We have currently not
    considered any certification
-   The webinos runtime will support *attestation* for devices which can
    provide it. This means that apps will be capable of assessing the
    integrity of webinos software instances

"SP-2050 The WRT MUST authenticate itself to network servers as
necessary using a WAC-recognised client certificate unique to the WRT
product and version. A "WAC-recognised client certificate" is one that
has been issued by a WAC-recognised Certificate Authority (CA) and is
considered valid by WAC, i.e. has not been revoked. "

-   Webinos devices will have a certified keypair signed by the personal
    zone hub. This key can be used within the personal zone and to
    identify the device but should *not* be used with untrusted devices
    or for discovery.
-   Webinos will provide access to keys stored on the platform.
-   There is no recognised single webinos authority.

#### 3.1.3 Widget Authentication[¶](#313-Widget-Authentication)

"SP-2060 The WRT MUST consider Widgets that have a self-signed author
signature as "unrecognised"."\
"SP-2061 The WRT MUST consider Widgets that have no author signature as
"unrecognised"."

-   Webinos will do the same in the above cases

"SP-2062 The WRT MUST consider Widgets that have a valid author
signature (i.e. one that has not been revoked) belonging to a
WAC-recognised identity as "recognised"."

-   Webinos *will not* attempt to validate authors against any new list
    of recognised identities.
-   Webinos *will* verify any signatures against a list of certificates
    held within the runtime. This is browser-ssl like behaviour.

"SP-2063 For recognised widgets, the WRT MUST verify that the widget's
Recognised Origin matches the identity of the signer based on the Common
Name attribute of the author certificate."\
"SP-2064 The WRT MUST reject a widget as invalid if the widget's
Recognised Origin does not match the identity of the signing party of
the author signature."

-   Unknown

"SP-2065 The WRT MUST display the following author information to the
user when confirming that the user wishes to install a widget: whether
the widget is recognised or unrecognised, the validated author identity
and author country."

-   Webinos will display some author information. Future webinos
    implementations may attempt to link this to information drawn from
    social networks to establish trustworthiness
-   TODO: How much information?

"SP-2066 The WRT MUST allow installation of widgets with expired author
certificates, if installation is not blocked by other conditions (e.g.
SP-2067, SP-2130)."

-   Webinos will follow this requirement

"SP-2067 The WRT MUST provide a user-configurable 'secure-by-default'
preference to enable installation of widgets that are not
distributor-signed, with the default value set to "No". If the user
selects "Yes", they MUST be shown a warning explaining the potential
dangers of installing unsigned widgets."

-   Webinos will default to disallowing web apps and will allow such a
    dialogue to be implemented

"SP-2068 The WRT MAY further enhance the functionality in SP-2067 by
supporting a latch function to reset the user preference once they have
installed an unsigned widget. The options popup for this
sub-functionality could be as follows: "only for one application", "for
15 minutes", "forever"."

-   Webinos has no requirements to implement a latch policy. Phase two
    could investigate the option for applications to run in a sandbox,
    like the one described in [this paper on the android
    system](http://news.ncsu.edu/releases/wms-jiang-tissa/)

### 3.2. Widget Signatures[¶](#32-Widget-Signatures)

"SP-2080 The WRT MUST support widget signature processing as specified
in Widgets Digital Signature [Widgets-DigSig]. Test: Test Suite for the
"Digital Signatures For Widgets" Specification."

-   Webinos will follow this requirement

"Every widget offered by developers to WAC, and delivered to a WRT
through a WAC channel, MUST have a valid author signature. An author
signature is considered valid if either: it is self-signed - ie the
signature chains to a certificate, which is included in the signature
document itself, which is self-signed; or it is signed by a certificate
belonging to a WAC-recognised identity."

-   Webinos will follow this requirement except "WAC-recognised
    identity" will just be "runtime recognised identity" - an identity
    verifiable by the certificates held in the runtime.
-   Webinos will also follow SP-2090, SP-2100, SP-2110 and SP-2120
    requirements, except the table...

#### Table SP-2120[¶](#Table-SP-2120)

![](http://specs.wacapps.net/2.0/feb2011/core/signatures.png)

The following changes will be made to this table:

-   ...

#### 3.2.1. Signature Revocation[¶](#321-Signature-Revocation)

Webinos will follow all requirements in this section.

### 3.3. Widget Protection[¶](#33-Widget-Protection)

Webinos will follow requirements SP-2180 and SP-2185 in this section.
Widget sharing is not considered to be part of the security framework,
and WAC signed widgets are not relevant. However, Webinos *shall*
support policies which dictate where widgets made be loaded from, which
could implement SP-2196.

### 3.4. Security Framework[¶](#34-Security-Framework)

Webinos will follow SP-2200

#### 3.4.1. Policy Definition[¶](#341-Policy-Definition)

##### 3.4.1.1. Trust Domains

Webinos will follow SP-2240

##### 3.4.1.2. Policy Rules

"SP-2250 The WRT MUST support the following options for policy rule
effects: Blanket prompt, session prompt, one-shot prompt, permit, deny"

Webinos will support this requirement.

##### 3.4.1.3. Policy Structure

Webinos policies will refer to applications as the subject. This is
documented in more detail in the T3.1 page.

##### 3.4.1.4. Sensitive Functions

SP-2280 Webinos policies will be capable of supporting access control to
all APIs and device capabilities in webinos.

SP-2281 Webinos policies will be capable of mediating all network access
and access to particular endpoints. Policies must be able to say
"Application X cannot access my set top box"

##### 3.4.1.5. Security Parameters

"SP-2282 The WRT MUST support the following environment attributes and
device capability request parameters in policy rules: ... "

These environment rules and parameters will be followed by webinos

##### 3.4.1.6. Specific Clarifications

"SP-2300 When access has been granted to a particular filesystem
location, the WRT MUST grant access to all subordinate locations (e.g.
subdirectories) for the duration of the access granted to the
filesystem."

Webinos will follow this rule.

#### 3.4.2. Policy Deployment[¶](#342-Policy-Deployment)

Webinos will follow SP-2320, SP-2330, and SP-2340.

Webinos will follow SP-2351: "The WRT MAY be capable of applying
different policies depending upon device configuration or user
identity/role, e.g. for application of enterprise policies or parental
control policies."

Webinos will follow SP-2352 (new requirement for webinos)

#### 3.4.3. Policy Enforcement[¶](#343-Policy-Enforcement)

Webinos follows SP-2360, SP-2370, SP-2380 and the [BONDI A&S Appendices
Appendix
B](http://bondi.omtp.org/1.1/security/BONDI_Architecture_and_Security_Appendices_v1.1.pdf)
.

#### 3.4.4. User Prompting and Preferences[¶](#344-User-Prompting-and-Preferences)

Webinos specifications do include some GUIs, but these are guidelines
only.

Webinos will follow SP-2390, SP-2400, SP-2420, SP-2421 and SP-2422.

Requirements SP-2405 and SP-2406 will be provided by allowing XACML
combination policies with set priorities.

### 3.5. Security Features of Web Technologies[¶](#35-Security-Features-of-Web-Technologies)

#### 3.5.1. Widget Access Request Policy[¶](#351-Widget-Access-Request-Policy)

Webinos will follow these requirements

### 3.6. Non-WAC APIs[¶](#36-Non-WAC-APIs)

Webinos will not follow SP-2460 but the policy infrastructure should
allow this to be possible.

### 3.7. Description Resources[¶](#37-Description-Resources)

Webinos will have a similar approach to SP-2650 and POWDER policies, but
this is still being confirmed. SP-2691...3 will therefore not
necessarily be followed.

SP-2660 to 2690 will be followed.

### 3.8. Privacy[¶](#38-Privacy)

SP-2480 and SP-2490 should be followed by webinos.

Again, POWDER policies may be used but this is up for consideration.

#### 3.8.1 Privacy Considerations for API Usage[¶](#381-Privacy-Considerations-for-API-Usage)

#### 3.8.2 Privacy Considerations for Device Property Access[¶](#382-Privacy-Considerations-for-Device-Property-Access)

### 3.9. Parental Mode[¶](#39-Parental-Mode)

### 3.10. Default Policy[¶](#310-Default-Policy)

#### 3.10.1 Trust Domains[¶](#3101-Trust-Domains)

#### 3.10.2 Permissions[¶](#3102-Permissions)
