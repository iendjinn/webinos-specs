Summary[¶](#Summary)
--------------------

We have analysed the webinos architecture based on 14 attack patterns
motivated by the findings of Deliverable 2.7 and 2.8, as well as ongoing
development and emerging security and privacy issues. This provides a
substantial range of attacks and obstacles to consider in the
architecture. Indeed, all of the leaf obstacles obtained during this
process have been included in the analysis and shown to either be
satisfied by a goal supported by the architecture or shown to be lacking
a solution at present. Our process is sufficiently rigorous that we are
now able to draw several conclusions about the design of the
architecture. However, more attack patterns and architectural patterns
should be developed in the coming months in order to provide a more
complete analysis and to prioritise future development of security
functionality. It is also important to note that this analysis refers
primarily to the *specification* of the system rather than the
implementation. We have not analysed the level in which the
specifications are implemented, nor have we considered the strength of
the implementation against known code-level vulnerabilities.

Based on the findings of the attack-resistance, weakness and ambiguity
analysis, we have made the following conclusions.

### Application rendering[¶](#Application-rendering)

At present, our architecture does not fully address attacks on content
rendered by widget renderers and browsers. This leaves webinos and
webinos applications vulnerable to attacks such as content injection
(cross site scripting, for example). This is primarily due to the re-use
of existing web browsers as opposed to customising a browser with a
webinos-specific extension. Customisation would allow additional rules
and restrictions to prevent some of the more prevalent and likely
attacks.

### Comparative exposure of personal zone hubs and proxies[¶](#Comparative-exposure-of-personal-zone-hubs-and-proxies)

Based on the quantitative analysis of the attack surface in the
ambiguity analysis, the webinos attack surface associated with setting
up personal zone hubs is greater than the surface exposed when enrolling
devices to personal zones; this is largely due to the attack surfaces of
the assets associated with each architectural pattern rather than the
damage potential associated with component interfaces or connectors.
While a lot of emphasis has been placed on the device-side webinos
architecture, the webinos hub-side architecture is less well understood
with undefined surface types for the administration console and the
potential for rendering engine weaknesses compromising traffic to/from a
personal zone hub.

#### Reliance on OpenID authentication[¶](#Reliance-on-OpenID-authentication)

The webinos platform is novel in its approach to authentication: we
introduce no new passwords or usernames into the system and delegate
most authentication tasks either to the underlying operating system or
to an OpenID provider. However, this puts many mitigations out of scope,
and the system is at risk when a weak or insecure OpenID provider is
used. We believe this to be a reasonable approach, but it also means
that webinos personal zone hub providers ought to limit the number of
OpenID providers they support for security reasons, despite the negative
impact on interoperability.

#### Policy management remains crucial[¶](#Policy-management-remains-crucial)

The policy-based access control system remains an important aspect of
webinos and is responsible for satisfying at least 15 goals from the
ambiguity analysis. This means that additional effort should be spent
making sure that policy features are implemented in the platform, and
that appropriate tools and user interfaces are provided. It is also true
that default policy settings will be important to mitigate several
obstacles, and these may need to be improved based on experience and the
findings from Deliverable 2.8.

#### Privacy and service discovery[¶](#Privacy-and-service-discovery)

A privacy issue that has been discovered throughout the analysis is the
use of the `findService` call, which returns persistent device
identifiers and could potentially be used to re-identify the user,
breaking unlinkability requirements. This problem has been reported to
the rest of the project, and motivates further improvements and
investigations of the Web Intents alternatives, as discussed in
Deliverable D3.3.

#### Protecting webinos source code[¶](#Protecting-webinos-source-code)

The current webinos development process must protect users against the
potential for a malicious contributor from adding back-door
vulnerabilities to the platform. While this is solved (to some extent)
through the gate-keeping implemented as part of the GitHub development
process, further improvements are needed. In particular, creating a
larger distinction between tests and platform code and making it easy to
remove testing code from deployments of the platform.

A related issue is that of code quality and input sanitisation. Any
communication with the PZP should be thoroughly checked and validated
against a provided schema to prevent malicious code injection exploiting
the runtime. This should be part of the requirements for accepting new
code into the webinos source code repository.

#### Denial of service issues[¶](#Denial-of-service-issues)

Several of the attack patterns we considered in this analysis relate to
denial of service issues. We believe that the architecture mitigates
denial of service attacks in the following way:

1.  Because the PZP does not rely on having a PZH available for local
    functionality, loss of the PZH doesn't prevent use of the PZPs. The
    PZH being made unavailable is, therefore, less important in many
    situations than a PZP being made unavailable. Indeed, the PZH is not
    required for local, peer-to-peer interaction between devices.
2.  Support for downloadable widgets means that application can be used
    offline, and can be designed to be resistant to loss of network
    connectivity. Installing applications does not require an internet
    connection.
3.  Process isolation between the web browser or widget renderer and the
    PZP should make the PZP harder to attack directly.
4.  Restrictions on widget content should make content-injection DoS
    attacks harder to perform.
5.  The use of long-term certificates means that credential expiration
    is not an availability issue.

However, we remain aware of the following issues with respect to
availability:

1.  The policy system is vulnerable to misconfiguration, which could
    make PZPs unable to communicate.
2.  The availability of the OpenID provider is important, but is out of
    the control of webinos.
3.  Attacks on platform integrity from malware is not something we can
    mitigate.
4.  API-specific resource exhaustion attacks may be a problem. These are
    discussed in the API Security and Privacy Analysis section.

#### Data storage[¶](#Data-storage)

The security of data used within webinos is largely dependent on the
devices running webinos, and therefore is largely outside of the scope
of the webinos architecture. The webinos implementation has avoided
providing additional data encryption tools on grounds that most
platforms already provide these options. In most cases, users have the
tools available to protect themselves. The outstanding threats include:

-   Protecting valuable IPR stored within downloaded widgets. A solution
    to this problem would require Digital Rights Management. This is
    hard to implement across multiple platforms and is no longer within
    the scope of webinos.
-   Isolated data storage on windows and Linux. Native malware may be
    able to access webinos data as it is not protected on these systems
    by default.
-   PZH implementations may have varying levels of security from online
    attacks. We refer to the cloud security section to provide more
    details on potential solutions.

