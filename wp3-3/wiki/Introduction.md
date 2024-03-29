Introduction[¶](#Introduction)
==============================

Final update done.

-   [Introduction](#Introduction)
    -   [1 Intended audience](#1-Intended-audience)
    -   [2 What is webinos?](#2-What-is-webinos)
    -   [3 Document structure](#3-Document-structure)
    -   [4 References](#4-References)

This suite of documents, coded D03.3 in the webinos project, provides
detailed technical specifications for the webinos platform. They succeed
the webinos scenario, use cases and requirements specifications [WOS21,
WOS22, WOS24, WOS25]. They are the webinos project Phase II
specifications that supersede the project Phase I deliverable D03.1.
Users should refer to these documents instead of D03.1.

1 Intended audience[¶](#1-Intended-audience)
--------------------------------------------

The primary intended audience are developers of the webinos platform and
developers of webinos applications, as defined in [WOS25, p17, p18].
Other users who may find these documents useful include, but are not
limited to, webinos enabled device manufacturers, webinos application
service providers and network providers [WOS25, p17, p18]. For webinos
platform developers these documents are the complete implementation
guide and the requirements for a conformable webinos implementation. The
developers should refer to these documents during the development
process and any maintenance of and future extensions to the platform.
For developers of webinos applications this document provides an insight
into the platform and will help the developers make the best use of
webinos features to enrich their applications in development.

2 What is webinos?[¶](#2-What-is-webinos)
-----------------------------------------

Increasingly, users are owning more connected devices and expecting
applications to keep preferences and status information synchronised
across devices in different domains. The purpose of the webinos project
is to define and deliver an open source platform, which will enable web
applications and services to be used and shared consistently and
securely over a broad spectrum of connected devices. To achieve this, it
defines and provides an architecture and infrastructure to allow
applications to run not only on a single device, but also across devices
and domains. This applies to device features as well. New APIs are also
provided to allow access to local and remote device resources and
network resources in the Cloud.

Webinos, as defined in [WOS21, p14] and [WOS22, p6], is a cross-domain
platform for secure web application delivery. These domains include
mobile, PCs, home media (TVs), and in-car units devices. It is specified
as middleware installed on a selection of operating systems (OSs) on
current devices to enable the consistent and secure web application user
experience. At the time of writing the supported OSs and device
platforms include:

-   Android 2.3.x\
     tested with devices: Nexus S, Asus Transformer Prime, Samsung
    Galaxy S2, Sonyericsson Xperia Arc, Galaxy Note
-   Microsoft Windows 7 SP, Windows 7, Windows XP\
     tested with laptops: Vaio z11, Dell, Asus EeePC (1215N)
-   Linux: Ubuntu 10.04 LTS, Slackware 13.1, 13.37, Mint, Fedora\
     tested with devices: VMWare Player, Samsung, Asus EeePC (1215N)\
     TV variants of Cocom Churchill 177, Acer Revo etc.\
     vehicle variant of Pandaboard Rev. A3 with Ubuntu 11.10
-   Mac OS X

The webinos platform includes not only a set of newly defined APIs to
enhance current web application runtime environments, but also an
overlay network architecture to enable the webinos specific features.

3 Document structure[¶](#3-Document-structure)
----------------------------------------------

This suite of documents, D03.3, cover the architecture and required
infrastructure and service components. They consist of 6 specifications,
each of them is a self-inclusive specific document. The individual
document structure can be found in each document.

-   High level specification
-   Personal Zone Proxy specification
-   Personal Zone Hub specification
-   Common and core specification
-   Applications specification
-   Informative specification

Webinos APIs and security are only mentioned briefly where appropriate
in these documents to assist specifying the system architecture and
components. They are specified in [WOS34] and [WOS36] in details
respectively.

4 References[¶](#4-References)
------------------------------

[WOS21] webinos project deliverable D02.1, Use Cases and Scenarios.
January 2011.\
[WOS22] webinos project deliverable D02.2, Requirements and Developer
Experience Analysis. February 2011.\
[WOS24] webinos project deliverable D02.4, Updates on Scenarios and Use
Cases. April 2012.\
[WOS25] webinos project deliverable D02.5, Updates on Requirements and
Available Solutions. April 2012.\
[WOS34] webinos project deliverable D03.4, webinos phase II Device,
Network, and Server-side API Specifications. September 2012.\
[WOS36] webinos project deliverable D03.6, webinos phase II Security
Framework. September 2012.

------------------------------------------------------------------------
