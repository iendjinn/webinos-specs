Cloud Security and Privacy[¶](#Cloud-Security-and-Privacy)
==========================================================

Introduction[¶](#Introduction)
------------------------------

Cloud computing has emerged as a distributed system of choice for many
use cases. As a utility, cloud platforms enable a pay-per-use basis,
while their dynamic scalability attributes enable automated increase or
decrease of resources for a particular service in response to increasing
or falling demand, respectively. However, security and privacy remains
one of the biggest challenges
([Kandukuri-cloud-sec-09](Kandukuri-cloud-sec-09.html)); as a result
many organisations are reluctant in adopting cloud computing, especially
when it comes to critical or sensitive applications.

Despite these challenges, significant strides have been made in the
adoption of cloud computing as can be seen by an increase in cloud
service offerings in the area of storage ([Dropbox](Dropbox.html)),
communication and social networking. It is therefore impossible for
webinos to completely ignore cloud computing; several applications
running on webinos-enabled devices will use cloud services, others
applications may be hosted on the cloud or indeed some components, such
as the Personal Zone Hub (PZH), may be deployed in the cloud. For
example, see the possible PZH deployment profile in the D3.3 informative
specifications ([Webinos-D33](Webinos-D33.html)). However, in order for
webinos to successfully take advantage of cloud computing or indeed work
with services on the cloud, it is important that security and privacy
implications are understood.

This section aims to meet this goal by investigating how the use of
cloud computing could affect the security and privacy of webinos. More
specifically, the section investigates the possible assets that could
exist in a cloud-based PZH and how these are affected by common threats
and vulnerabilities associated with cloud computing.

The investigations are based on the following scenario. *Alice* is a
technology enthusiast who always wants to take advantage of new
technology to make her life easier. She has been encouraged by cloud
computing's promise of on-demand provision of resources, global
accessibility and pay-per-use model. She recently signed up to Amazon
Web Services and has now started using these services; she has so far
managed to deploy a gaming application and streaming service. *Alice*
has realised that there are some free compute cycles on her account and
she has decided to use those for webinos. Depending on how this goes,
she may decide to offer this as a service to her friends. However,
before she can do that she needs to understand what the impact of this
move on the security of her data and her privacy would be.

To help *Alice* decide on whether or not it would be ok to use cloud
computing, the section begins with some background on general cloud
computing issues including its definition and some of the top threats to
its adoption. Following this, a security and privacy analysis is
performed on a cloud-based Personal Zone Hub. This analysis identifies
the assets that may exist in a cloud environment and then investigates
how these assets are affected by some of the common threats identified
in the background. The section then describes how these threats might be
realised.

Background[¶](#Background)
--------------------------

Cloud computing has emerged as one of the hot topics in distributed
computing. However, there is still confusion on how cloud computing is
defined. Some suggest that it is a new architecture and approach, while
others argue that it is simply a modification of the business models
rather than a new computation paradigm. In order for the analysis to be
useful, this section needs to make clear the view of cloud computing
adopted; with the hope that this view will be shared with *Alice*. For
this reason, the next section covers the definition and taxonomy of
cloud computing before discussing the security challenges of using it.

### Cloud definition, taxonomy and examples[¶](#Cloud-definition-taxonomy-and-examples)

Despite significant attempts at defining cloud computing, there is still
no consensus on its definition. However, one commonly accepted
definition is that from NIST
([NistCloudDefinition2011](NistCloudDefinition2011.html)):

> Cloud computing is a model for enabling ubiquitous, convenient,
> on-demand network access to a shared pool of configurable computing
> resources (e.g., networks, servers, storage, applications, and
> services) that can be rapidly provisioned and released with minimal
> management effort or service provider interaction.

Central to this definition is the idea of on-demand provision of
computational resources ([CloudSecMather2009](CloudSecMather2009.html),
[CloudCompRittinghouse2010](CloudCompRittinghouse2010.html)) so that
users can start with a minimal set of resources, which can be
dynamically increased or decreased depending on demand. This enables a
pay-per use model where users only get to pay for the amount of
resources used rather than for the ownership of those resources. To
support this, cloud computing is designed with a number of
characteristics.

#### Service Models[¶](#Service-Models)

Cloud computing services can be provided using three main models:

-   “Software as a service” (SaaS) - the customer does not purchase
    software, but rather rents it for use on a subscription or
    pay-per-use model
-   “Platform as a service” (PaaS) - the vendor offers a development
    environment to application developers, who develop applications and
    offer those services through the provider’s platform
-   “Infrastructure as a service” (IaaS) - the vendor provides the
    infrastructure to run the applications, but the cloud computing
    approach makes it possible to offer a pay-per- use model and to
    scale the service depending on demand.

Other less common used models include:

-   “Communication as a service” - a subtype of Software-as-a-Service
    model, where providers are responsible for the management of
    hardware and software, e.g. VoIP, instant messaging, and
-   “Security as a service” - a vendor offers security functionalities
    like e-mail and web content filtering, vulnerability management,
    etc.

#### Essential Characteristics[¶](#Essential-Characteristics)

NIST identifies five key characteristics of cloud computing including:

1.  On-demand self-service - users can request more services any time
    and the system used can provide these services automatically without
    requiring human interaction.
2.  Broad network access - the services can be globally accessed using
    standard network mechanisms, enabling users to use different devices
    such as mobile phones, tablets, laptops, and workstations.
3.  Shared resource - a multi-tenant model enables resources to be
    shared among a number of users while giving an illusion that each
    user owns the resource.
4.  Rapid elasticity - the capabilities and/or capacity of resources can
    be increased or decreased automatically without affecting the
    availability of the services.
5.  Measurable services - resources used can be transparently monitored
    and measured for the purpose of billing and monitoring of
    service-levels

### Cloud security models[¶](#Cloud-security-models)

Security concerns about cloud computing include a mix of old and new
threats, targeting software bugs, exploiting social engineering, and
involving network security and access controls. These exist at different
levels including: network, host and application. Sensitive data must be
adequately secured at each level to avoid confidentiality and integrity
breaches. Furthermore, proper access control, accountability identity
and access management must be designed in order to achieve efficient
procedures, mitigate complexity, improve user experience, and reduce
errors and insecure short-cuts.

#### Cloud security - network[¶](#Cloud-security-network)

Like all network-based systems, cloud systems expose significant risk at
network level. Data in transit to and from the cloud infrastructure may
suffer from confidentiality and integrity problems resulting from
activities by malicious agents along the path. Unauthorized access can
also be problematic when cloud providers do not adopt effective IP
address reallocation mechanisms
([DHCPDynamicIPAddressing](DHCPDynamicIPAddressing.html)) that ensure
that an IP address that was originally assigned to a resource that is no
longer needed cannot be used to access that same resource. As a result
of this, customers cannot assume that network access to their resources
is terminated upon release of its IP address, opening the path to
unwanted access.

Cloud system must also guarantee high availability. For example, BGP
hijacking ([BGPAttacks04](BGPAttacks04.html)) can affect the
availability of cloud-based resources, while the use of external DNS
querying exposes clouds to DoS attacks.

The use of cloud systems also introduces new and different security
boundaries. The established model of network zones and domains is
replaced with less precise and firm “security groups”, “security
domains” or “virtual data centers”. Conceptually, this allows separation
between tiers, but these need to be properly understood if security
breaches and improper use is to be avoided.

Network security hardening is necessary to avoid common network attacks.
For example, confidentiality and integrity can be assured by appropriate
encryption and digital signature, network filters (e.g., firewall)
should be shaped and managed by cloud providers. For the sake of
accountability and forensics, provider-managed aggregation of security
event logs is desirable, and to timely address ongoing problems,
network-based intrusion detection system/intrusion prevention system is
useful.

#### Cloud security - host level[¶](#Cloud-security-host-level)

Although there are few new host level security threats and
vulnerabilities, some are inherited from related environments, e.g. some
virtualization security threats carry into the public cloud computing
environment. Even if the threats are not conceptually new, cloud
computing harnesses the power of thousands of compute nodes, combined
with the homogeneity of the operating system employed by hosts. This
means threats can propagate quickly and easily.

Different cloud models imply slightly different security requirements.

In SaaS and PaaS, host security is opaque to customers. The
responsibility of securing the hosts is relegated to the CSP (Cloud
Service Provider), who institutes the necessary security controls. These
include restricting physical and logical access to hypervisor and other
forms of employed virtualization layers.

In the IaaS cloud model, the CSP has to secure the virtualization layer.
A vulnerable hypervisor could expose all user domains to malicious
insiders. The customer guest OS (or virtual server) is also a point of
interest. It has an operating system provisioned on top of the
virtualization layer that customers have full access to. Since the
virtual server may be accessible to anyone on the Internet, access
mitigation steps should be taken to restrict access to virtual
instances. It is therefore necessary to adopt a *secure-by-default*
configuration; this includes tracking the inventory of VM images and OS
versions that are prepared for cloud hosting.

#### Cloud security - application level[¶](#Cloud-security-application-level)

In addition to well known application vulnerabilities, and well known
attack types, cloud-based systems can experience other attacks. For
example, an application-level DoS attack could manifest itself as
high-volume web page reloads, XML web services requests, or
protocol-specific requests supported by a cloud service. These kinds of
attacks can be particularly dangerous because it is difficult to
selectively filter the malicious traffic without impacting the service
as a whole ([AppLayerDDOSXie](AppLayerDDOSXie.html)). This is because
attackers use legitimate HTTP requests to the victim, which are
indistinguishable from requests coming from genuine users
([AppLayerDDOSXie](AppLayerDDOSXie.html),
[AppLayerDDOSMonitor09](AppLayerDDOSMonitor09.html)). DoS attacks on
pay-as-you-go cloud applications could result in an increased cloud
utility bill due to increased use of network bandwidth, CPU, and storage
consumption. Therefore, sufficient protections need to be put in place
to prevent resources used by a hijacked or exploited cloud accounts from
being enrolled into botnets.

End users should be conscious about security and take appropriate steps
to protect their web browsers from attacks. They must install patches
and updates in a timely basis to mitigate threats related to browser
vulnerabilities. However, as cloud-based services become widespread,
relying on users alone will not be sufficient, so providers need to give
some kind of assurance of adequate security. This assurance might be in
the form of legal responsibility; for example, SaaS providers are
largely responsible for securing the applications and components they
offer to customers, while customers are usually responsible for
operational security functions, including user and access management as
supported by the provider.

In a PaaS context, developers need to become familiar with specific APIs
for deploying and managing software modules to enforce security controls
as part of their product life cycle. In theory, developers should expect
CSPs to offer a set of security features, including user authentication,
single sign-on (SSO), authorization, and SSL or TLS support, made
available via the API. In the IaaS model , however, matters are
predominantly left in the hands of end users. Customers should not
expect any application security assistance from CSPs beyond basic
guidance on firewall policies that may affect the application’s
communications with other applications, users, or services within or
outside the cloud. customers are responsible for keeping their
applications and runtime platform patched to protect the system from
malware and hackers scanning for vulnerabilities to gain unauthorized
access to their data in the cloud, and highly recommended to design and
implement applications with a “least-privileged” runtime model.

### Cloud security alliance Top Threats[¶](#Cloud-security-alliance-Top-Threats)

Several organisations and communities have invested significant effort
in identifying and characterising cloud computing security issues. An
example of such an effort is that by the Cloud Security Alliance (CSA)
who have identified top threats to cloud computing
([CSA-TopThreats](CSA-TopThreats.html)), discussed below.

#### Abuse and nefarious use of cloud computing[¶](#Abuse-and-nefarious-use-of-cloud-computing)

The registration process offered by some devices accept anyone with a
valid credit card or even worse offer limited trial periods, which may
allow spammers, worm author and criminals in general to conduct
unauthorized activities with relative anonymity and impunity. This
particularly affects IaaS and PaaS models. This threat can be mitigated
by employing stricter registration and validation processes, e.g.
monitoring of fresh credit card frauds, monitoring of user network
traffic (possibly in aggregate form, to respect privacy issue) and
monitoring procedures.

#### Insecure interfaces and APIs[¶](#Insecure-interfaces-and-APIs)

Providers should be very careful in exposing software interfaces to
interact with cloud services, and design these interfaces adopting
proper encryption, authentication, access controls and monitoring to
avoid policy circumvention, like anonymous access and or reusable
authentication tokens, monitoring and logging capabilities unable to
identify key events, unknown service and API dependencies. This kind of
problem is quite generic and involve Cloud models of IaaS, PaaS and SaaS
types.

To mitigate such a problem, knowledge of dependency chain associated
with the API, as well as mandatory strong authentication in concert with
encrypted transmission is needed.

#### Malicious insiders[¶](#Malicious-insiders)

IaaS, PaaS and SaaS models suffer from the convergence of services and
customers under a single management domain, often combined with lack of
transparency of providers internal processes. In this way, opportunities
for harvesting confidential data or to gain unauthorized control over
the cloud service can be achieved with little risk of detection.

This is remediable by a proper organizational (e.g. a strict supply
chain management with associated supplier assessment) and legal
(specification of resource requirements as part of legal contracts)
framework. Clear, transparent and well-established information security
management, compliance reporting as well as security breach notification
processes also contribute towards mitigation of this issue.

#### Shared technology issues[¶](#Shared-technology-issues)

Shared technology must implement strong isolation properties for a
multi-tenant architecture. Access of resources should be mediated by the
virtualization hypervisor, which manages guest operating systems and
prevents improper resource access or control on the underlying system.
However, even hypervisors can be flawed, and cause unwanted influence of
the underlying platform by the guest operating system.

To prevent this critical issue, which is especially sensitive in IaaS
model, security best practice must be adopted when installing and
configuring the system. Monitoring system must adequately identify
unauthorised changes and suspect activities. Strong authentication and
fine-grained access controls should enforce proper administrative access
and operations. Vulnerability scanning and configuration audit should be
performed periodically, and a proper threat management process should
ensure prompt patching and vulnerability remediation.

#### Data loss or leakage[¶](#Data-loss-or-leakage)

Since data in the cloud can possibly be physically unbound to local
users, cloud-based data management must avoid alteration of records with
no backup, as well as loss of encoding keys (which may result in
effective data destruction) and unauthorized access to sensitive data.
This is a general problem which any of IaaS, PaaS and SaaS model have to
prevent.

This kind of problem can be mitigated by some security best practice,
like detailed API access control, encryption and integrity protection of
data in transit (driven by a careful analysis of data protection scheme
both at design and run time), implementation of secure key generation
and life cycle management (e.g. storage and destruction procedures). An
appropriate legal framework is useful as well (e.g. contractual
obligations for providers to wipe persistent media before releases of
sensitive data, contractual specification of backup and data retention
strategies)

#### Account or service hijacking[¶](#Account-or-service-hijacking)

Being a network based model, clouds are vulnerable to phishing, fraud
and software vulnerability exploitation. Given that credentials and
password are often reused, the impact of such attacks is amplified. This
is because account owners are often unaware that their accounts have
been exploited to form the basis of further malicious actions. All IaaS,
PaaS and SaaS can suffer of these issues.

A mandatory policy on credentials (e.g. prohibit sharing of passwords or
credentials between users and services), and leveraging multi-factor
authentication techniques (whenever possible) as well as proactive
monitoring to promptly identify unauthorized entities can alleviate
impact of this threat.

#### Unknown risk profile[¶](#Unknown-risk-profile)

A detailed knowledge of security posture is important for threat
prevention. Understanding the software, software updates, security
practices, intrusion attempts, and employed security controls are
important factors in understanding current risk level and planning
adequate modifications. The temptation of employing *security by
obscurity* should be avoided as opaque designs make in-depth analysis
difficult. This is a general concern that is valid for all cloud models.

Mitigating practices include providing information about who is sharing
the infrastructure, disclosure of network intrusion logs, redirection
attempts (and success), and partial/full disclosure of infrastructure
details (e.g. patch level, firewalls, etc). Even if not intuitive, these
processes foster a more vulnerability-free and secure system.

webinos in the cloud[¶](#webinos-in-the-cloud)
----------------------------------------------

Although webinos is designed to run on devices such as in-car systems
and mobile devices, it relies on inter-device connectivity for several
aspects of its operation. In particular, keeping a list of preferences
synchronized across a user's devices or sharing media content requires
the devices to connect to each other or to a mediating component. These
devices could be geographically distributed across the globe. As a
result, webinos relies on global scale infrastructure such as the
Internet to provide connectivity. However, such infrastructures are
faced with a multitude of security and privacy problems. webinos' use of
these infrastructures imply that it will also be exposed to these
problems, and its cross device nature would make it an even more
attractive target for attackers. For this reason it is important to
understand the impact of webinos' reliance on these infrastructures on
the security and privacy of both webinos devices and the data they
handle.

### Why in the cloud?[¶](#Why-in-the-cloud)

The webinos architecture proposes to make use of cloud infrastructure to
host personal zone hubs (PZHs). The primary requirement of a PZH is that
it is constantly available via the internet and is at a known address.
High availability is one of the key selling points of a cloud, so this
implementation choice makes sense. Alternative scenarios such as a PZH
being on a home router are also possible, but unlikely to be as
available for users such as our personas Georg and Clara (since these
users are quite mobile and may require global access to their PZH).

A cloud-based PZH would need to be provided by a cloud service provider.
This would be a service which inevitably cost money, perhaps as part of
a mobile contract or with home broadband connection providers. The
service could be charged on a per usage basis or as a one-off fee. Cloud
hosting would allow for many additional bundled services, such as cloud
storage and backup or enhanced security and assurance (see later).

Deploying services on a cloud infrastructure has some widely recognized
barriers, which seems acceptable in the webinos case for the following
reasons:

1.  **Availability of service**: since the use is limited to a single
    person, the assurance level provided by cloud providers is
    acceptable for a personal zone. The synchronisation and data caching
    features provided by personal zones may be seen as a way of
    mitigating availability issues. However, in the case of a personal
    zone hub used by an entire organisation (and 'enterprise zone hub'),
    it is likely this assumption should be discarded. In that case, one
    possible risk mitigation strategy would be to have this enterprise
    hub hosted on multiple cloud providers. In this case, some
    functionality to synchronising between the two personal zone hubs
    (hosted by different cloud providers) would be desirable.
2.  **Data lock-in**: occurs when a cloud provider stores or manages a
    user's data in a way that is only compatible with their system, so
    that it becomes difficult for the user to move away from the
    provider. To avoid this problem, the user can export the PZH data
    and to import it in another cloud. This can be achieved by either
    directing transferring data between providers or exporting it in
    some format and re-importing at the other providers.

One of the main expected use of cloud systems in webinos is the hosting
of PZHs. For this reason, the following sections provide more
comprehensive analysis of the threats and attacks related to running a
PZH in the cloud.

### Cloud-based personal zone hub and hub provider[¶](#Cloud-based-personal-zone-hub-and-hub-provider)

A personal zone hub (PZH) is a key component in webinos. It provides a
consistent means of communication among devices; through its API and
services such as synchronization. In this section, we investigate the
security and privacy impact of running a cloud-based PZH --- where
cloud-based implies that the PZH has been deployed on a cloud
infrastructure.

#### Security Analysis[¶](#Security-Analysis)

Security analysis is based on previous work described in D2.7 and D2.8.
More specifically, the assets, threats and vulnerabilities identified in
the two tasks are used as input into the analysis. These are analysed to
identify how they are affected by the adoption of a cloud environment.

#### Analysis approach[¶](#Analysis-approach)

In order to understand the implications of running a PZH in the cloud, a
three-staged analysis approach was taken.

The first stage identified the threats faced by a cloud-based PZH design
and the assets that may reside on or be transmitted through a PZH. Using
the literature on cloud computing security as it relates to web
applications, common vulnerabilities that may exist on a cloud-based PZH
were identified, together with the possible attacks that might result
from compromising these vulnerabilities. The output of this stage is a
list of threats that webinos could be exposed to as a result of running
a cloud-based PZH.

Stage 2 involved analysing the current design of the PZH to (i) mine
architectural patterns currently in use in the PZH design, and (ii)
identify which or to what extend these patterns addressed the threats
identified in stage 1.

Stage 3 used the catalogue of architectural patterns to identify the
patterns that could be applied to the PZH design. This stage also
included an analysis of how these patterns and the ones identified in
stage 2 impacted security, privacy, performance and scalability. This
analysis produced a matrix specifying the relation of each pattern to
its security, privacy, performance and scalability impact on webinos.
The matrix was used to identify deployment profiles for PZHs. The figure
below illustrates the input and output of each stage as well as the
aspects considered in each stage. However, stages 2 and 3 are outside
the scope of this document, and will instead be documented on an
on-going basis.

![](pzh-analysis-approach.png)

#### Asset Model[¶](#Asset-Model)

D2.7 and D2.8 identified a number of assets and assigned security and
privacy values associated with each assets in a particular environment.
These assets where defined at higher level of granularity, i.e. system
level. This section is focused on understanding the impact of running a
PZH in the cloud. The PZH is a component of webinos and therefore, to
understand the threats associated with it, we would need to firstly map
the assets to a granularity suitable for a component.

The approach adopted for specifying the granularity is *subclassing*,
where each asset is broken down into subtypes that are as specific as
possible. For instance, an asset such as *SynchronisedAppData* could be
broken down to subtypes such as *Media*, *UserProfile* and
*LocationData*. Subclassing allows the association of assets to
components to be as specific as possible, thus enabling better analysis.

There are several assets used, generated or stored on a PZH. For
simplicity, we categorise the assets into two categories, namely:
credentials and functionality-related.

Credentials exist in many forms including certificates, passwords and
cryptographic keys. The diagram below illustrates the assets that fall
into this category.

![](pzh-credentials-assets.png)

The PZH is intended to provide certain key functionality (though the
functionality can be extended). As a result of the services it offers,
the PZH comes into contact with a number of assets. The diagram below
shows the key assets associated with the functionality of the PZH.

![](pzh-functionality-assets.png)

#### Security and privacy requirements for the PZH[¶](#Security-and-privacy-requirements-for-the-PZH)

Before conducing the analysis, however, we need to understand what the
requirements are for the PZH towards the assets identified above. Below,
we discuss some of the crucial ones.

-   Credentials must be held securely, including
    -   Certificate authority keys
    -   Any passwords or tokens used to access other services and
        devices - e.g. OAuth tokens
    -   Lists of trusted certificates
-   Personal data stored on the PZH must be protected. While only the
    minimum has been specified, webinos may store a wide variety of data
    such as:
    -   Contacts
    -   Photos, videos and media
    -   Location data
    -   The context database
    -   Lists of available applications and services
    -   Personal settings and information, such as date of birth, home
        address, identities on other social networks
-   The PZH will provide access control through policies and lists of
    trusted users. These lists are both private and have integrity
    requirements: they must not be modifiable by another party
-   The PZH to some extent represents user identity.
    -   Unauthorised access to this identity would allow impersonation
        and potential identity fraud.
    -   Disclosure of this identity may enable a user to be tracked by
        applications or other devices.

#### Threats to a cloud-based PZH[¶](#Threats-to-a-cloud-based-PZH)

Significant effort by organisations such as Mitre Corporation
([Mitre](Mitre.html)), NIST ([NIST](NIST.html)), cloud security alliance
([CSA](CSA.html)) and other communities, has been directed towards
identifying and classifying common threats that impact computer systems.
Some of the most significant threats that exist in a cloud environment
were discussed earlier. These threats affect different parts of a system
including input, output and in memory. The PZH is not immune to these
attacks. Moreover, some of the design choices for the PZH, such as
running it in the cloud, could make the risks of these threats greater.
For this reason, it is important to understand the threats that affect
the PZH, especially in relation to its cloud adoption.

In this section, we analyse the common threats to identify which of
these affect the PZH and in which instances they do so.

**Insider credential misuse**

In the asset model discussed above, several credentials were identified.
For example, the private key used to sign digital certificates issued to
devices connecting to the PZH was identified to both be highly
confidential and requiring high integrity. These credentials may be
required to be stored in the PZH to enable it to provide its services.
The CSA includes malicious insiders as one of the top threats to cloud
computing. A PZH deployed in the cloud could suffer from this threat and
allow malicious insiders to steal the credentials. Alternative,
non-malicious users, eg. administrators, may unwittingly expose these
credentials, eg. through backups. These leaked credentials can be used
to impersonate the PZH instance (eg. when its private key is
compromised) or issue certificates on behalf of the PZH.

**Unauthorised PZH duplication**

One of the main advantages of cloud computing is the ease of service
provisioning, enabled by mechanisms such as migration and virtual
machine cloning. This feature enables PZHs to be easily instantiated in
response to client requests for PZH instances. Additionally, new PZH
instances can also be created in response to increased demand for
services from a particular PZH. In this case provisioning of a PZH may
be achieved by either cloning an existing PZH or using a standard PZH
template. In the former, data stored within the PZH may be exposed as a
result. Alternatively sensitive PZH configurations may be leaked. In the
latter, PZH may end up sharing configurations, which if if insecure and
not modified, may result in break-once-run-everywhere kind of attacks.

**Loss of data such as synchronisation data**

A PZH once deployed provides a number of services such as
synchronisation and routing. These services handle various data such as
media, personal media preferences or contacts. This data does not have
high availability requirements, but if stored on the PZH alone, could
have significant effects on usability if lost. The issue with cloud
computing, as discussed in the data loss threat from CSA, is that it
provides a number of interfaces through which data may flow and thus
increasing the attack surface.

**Misuse or compromise of interfaces**

Cloud infrastructures are complex in nature. To manage this complexity,
cloud infrastructure provide several abstraction layers which hide the
underlying complexity by limiting accessibility of the services to
specially designed interfaces. These interfaces may, however, be poorly
designed or have vulnerabilities which may lead an attacker to either
misuse them (eg. sending well crafted exploit code) or access services
they are not authorised to access. Deployment of a PZH in the cloud
magnifies this problem. This is because the PZH itself, provides a
number of interfaces through which its services may be accessed. These
interfaces interact with with interfaces provided by the underlying
cloud infrastructure. Therefore any weakness or flaws in either the
interfaces of the cloud infrastructure or the PZH itself could lead to
compromise of the PZH or the assets stored on it.

**PZH integrity compromise resulting from insecure isolation**

A PZH deployed on the cloud would have to share the resources with
possibly other PZHs or other applications. While cloud computing relies
on virtualization to provide isolation, several attacks have
demonstrated that virtualisation may not always provide complete
isolation between services hosted on the same physical resource. CSA
identifies this as a threat resulting from sharing technology.

In the asset model, several PZH components were identified to be assets
as well, due to their relationships with other assets. For example, the
session Manager handles authentication and also comes into contact with
other assets such as private keys. A compromised session manager could
easily expose sensitive data or compromise its integrity. For this
reason, the integrity of some of the PZH components is considered to be
critical for the well functioning of the PZH. The threat of shared
technology could affect the integrity of the PZH components. In other
words PZH instances running in the cloud may not be securely isolated
from other services sharing the same resources, resulting in the
compromise of the PZH integrity.

**Privacy breach as a result of identifiable PZH**

When hosted in the cloud, the PZH will need to be linked to the user for
the purpose of billing. For this same purpose, PZH providers may need to
monitor activities on a PZH instance, e.g. to enable pay-per-use of
particular added-on services. As a result of this, PZH cloud providers
may be able to deduce sensitive information about the activities of the
PZH owner such as the services they accessed, leading to a privacy
breach. Furthermore, as indicated in the account or service hijacking
threat, attackers may perform certain activities which would be traced
back to the owner of the PZH.

**Sensitive residue migration data**

The use of cloud computing for the deployment of a PZH makes it easy to
switch from one provider to another; this is achieved through migration
services provided by most cloud offerings. This means that a PZH
instance can be migrated from one provider to another or from one
platform to another, i.e. as part of load balancing. Migrating a PZH
instance may involve moving the entire execution environment, such as
virtual machine, from one system to another or copying data that is
specific to a particular PZH instance into another environment capable
of running a PZH. In both cases residue data, which could potentially
include sensitive data such as keys, database backs or PZH
configurations, may be left on the original host. This data could be
used to mount attacks on the new PZH instance or leak sensitive
information.

**Data leakage by VM replication**

Similar to the threat of residue migration data, sensitive data could
also be leaked by cloning a PZH instance. Suppose *Alice* requires high
availability for her PZH, then as a solution, a cloud provider could
create several instances of the PZH, each with a copy of all of
*Alice*'s data, so that in an event that the main instance goes down,
eg. for maintenance, any of the cloned instances could be provisioned to
serve any incoming requests. The main threat here is that of an increase
in the attack surface. So that if any of the cloned instances have some
misconfiguration, then an attacker could take advantage of that and
exploit the PZH.

**Compliance and Unauthorised Data Disclosure**

One of the challenges faced in cloud computing is that of data location
([Kandukuri-cloud-sec-09](Kandukuri-cloud-sec-09.html),
[Binning-top-cloud-issues-09](Binning-top-cloud-issues-09.html)).
Whereas traditional dataware mechanisms provide visibility of the
location of data, the use of a cloud environment makes this completely
transparent. This means that data could be stored in a data centre
anywhere in the world. This means that information may cross the border,
raising concerns about forced data disclosure.

In *Alice*'s case, the PZH could be running on a server where the cloud
provider might be forced, under laws such as the Patriot Act
([USPatrioticAct-UnderFire-04](USPatrioticAct-UnderFire-04.html)), to
release the data to government agencies. This has the potential to
disclose all the sensitive information such as *Alice*'s activities and
behavioural patterns and media content.

### Cloud specific vulnerabilities[¶](#Cloud-specific-vulnerabilities)

The previous section presented some possible threats to a PZH running in
the cloud. However, in order for an attacker to realise these into
attacks, there has to be some exploitable vulnerabilities in the system.
One of the challenges in analysing the security and privacy impact of
cloud computing is understanding if at all there are specific
vulnerabilities that exist solely because of the use of a cloud
environment. Grobauer et al.
([Understanding-cloud-vulns](Understanding-cloud-vulns.html)) specifies
the characteristics of cloud specific vulnerabilities to include:

-   is intrinsic to or prevalent in a core cloud computing technology,
-   has its root cause in one of NIST’s essential cloud characteristics,
-   is caused when cloud innovations make tried-and-tested security
    controls difficult or impossible to implement, or
-   is prevalent in established state-of-the-art cloud offerings.

Using this characterisation, they identify some vulnerabilities specific
to cloud environment as well as how some common vulnerabilities equally
apply to cloud. These vulnerabilities are summarised in the table below,
which also indicates relationship to CWE where possible.

category

Vulnerabilities

Description

CWE Equivalency

Intrinsic to technology

Virtual machine escape

a virtual machine is meant to operate without influencing other VMs on
the same host, however, incorrect configuration of the hypervisor could
lead to a VM escaping from its containment and affect other VMs

Session riding/hijacking

sessions maintained by web applications could be exploited by attackers

CWE-613

insecure cryptography

cryptographic algorithms or protocols may be insecurely designed or
implemented and advancements in cryptanalysis may render them insecure

CWE-261

Cloud characteristic

Unauthorized access to management interface

management interfaces provide means of controlling the life-cycle of
resident VMs. Unauthorised access to the management interface could lead
to unexpected behaviour of the VM as their state can be changed

CWE-284, CWE-522

Internet protocol vulnerabilities

vulnerabilities in the underlying Internet protocols could allow
man-in-the-middle attacks

CWE-300

Data recovery vulnerability

resources assigned to a PZH instance might be re-allocated to a
different user at a later time making it possible to recover data
written\
by a previous user

Use of existing controls

Insufficient network virtualization

limited administrative access to IaaS network infrastructure imply that
standard network controls such as IP-based\
network zoning can’t be applied

poor key management procedures

lack of a fixed infrastructure makes it more difficult to apply standard
controls—such as hardware security module

close to CWE-321, CWE-324

Prevalent in state-of-the-art

weak authentication mechanisms or implementations

use of authentication mechanisms such as usernames and passwords have
inherent weaknesses which may allow credential interception and replay

CWE-287, CWE-290, CWE-303

vulnerable VM templates
([Kandukuri-cloud-sec-09](Kandukuri-cloud-sec-09.html))

the VM templates could contain vulnerable programs or data that the
creator did not intende to expose

Insufficient logging and monitoring possibilities

log files may not be linked to a particular tenant or contain sufficient
information making harder to imply security controls that rely on
logging and monitoring

CWE-778

### Extending the PZH functionality[¶](#Extending-the-PZH-functionality)

While the PZH is designed to provide services necessary to support cross
device connectivity, it is not hard to imagine instances where such a
design may be insufficient (i.e. in terms of features). Furthermore, it
is hoped that webinos will inspire some creativity, some of which will
be applied to the PZH functionality. For example, *Alice* may come up
with value-added services and offer her PZH to other people, for a fee.
These services may be implemented as applications which are strongly
tied to a particular PZH instance, PZH farm or PZH session. In order to
understand the security and privacy implications of a cloud-based PZH,
it is necessary to expand the scope of a PZH to include applications
that may be integrated into it. These applications may be vulnerable to
certain kinds of attacks, and thus may expose webinos to even more
attacks.

*Alice* could decide to integrate one of the applications that she uses
to manage her documents with webinos, so that all the preferences and
documents could be synchronized on her devices. This application may
need to know about the nature of *Alice* devices, for example to create
versions of documents compatible with each device. To achieve this, the
application would need to communicate with the PZH, enrol into the
personal zone and discover information about other services in the
personal zone.

webinos supports web applications that are downloadable widget packages
as well as fully web-based hosted applications. Hosted web applications
are often cloud based, relying on cloud storage, databases, or even
hosted on a cloud infrastructure. The design and structure of these
applications is largely out of scope. However, the project will be
considering the security and privacy of the concept applications, as
well as how webinos infrastructure can assist cloud-hosted applications
to make them more trustworthy.

Hosting such an application could be beneficial for *Alice*, as she
could use it on-demand and only pay according to how much she uses.
However, the question of the implication on the security and privacy of
assets still remains. Firstly, the application could be considered a
*virtual PZP*. In this case, the application might have access to all
the data in the personal zone, including contacts, personal preferences,
location data and API usage data. Most likely, such an application will
be designed to store this information in a database. Therefore, even
though the PZH could be secure, flaws in such an application or the
underlying database system might lead to compromise of asserts in the
personal zone.

The application might also incorporate other services from unknown or
untrusted providers. These services may have access to the data handled
by the application and therefore to the asserts. Storage mechanisms used
by the application could also be another source of concern. Furthermore,
the authenticity of the application and the trustworthiness of the
developers deserve some attention. And finally, the level of permissions
given to such *virtual PZPs* could lead to them accessing data they
should otherwise not be expected to access or perform actions that they
should not.

### Mitigations and opportunities[¶](#Mitigations-and-opportunities)

This section has identified a number of threats and vulnerabilities that
could be used to compromise the assets on a PZH. The question that this
raises is, how well placed is webinos to counteract these threats?
webinos already employees some mechanisms to counteract these threats.
However, more needs to be done in order to adequately cater for each of
these issues. Some of the important ones are discussed below:

-   **webinos credential storage** - credentials have been identified as
    one of the main assets in a PZH, which if compromised could have
    significant impact on the security and privacy or other aspects of
    webinos. These credentials could be accessed due to insufficient
    protection mechanisms on them. For example malicious insiders could
    access the credentials and use them to impersonate the PZH. For this
    reason, better protection mechanisms should be put in place to
    prevent these attacks. A common principle that might help with this
    problem is isolating the credentials from the data and or services
    to which they are applied.

<!-- -->

-   **Better credential management** - in addition to secure storage,
    the use of the credentials also needs to be properly controlled. Any
    key that is used must be tied to a well specified usage policy and
    must explicitly be specified with an expiry period after which the
    key should be considered compromised. Any backup procedures used for
    the keys must also be implemented to avoid leakage of these keys.
    Furthermore, when a PZH instance is migrated, the previous keys must
    be carefully destructed and new ones created.

<!-- -->

-   **PZH instance life-cycle management** - a PZH will run on VM
    instances that may be incorrectly configured or have outdated
    software. In order to avoid the attacks resulting from exploiting
    the underlying environment in which a PZH runs, it is important the
    that life-cycle of each VM used to host webinos is properly managed.
    This involves putting in place effective patch and configuration
    management processes as well as transparency in the creation process
    of these VMs.

<!-- -->

-   **Potential for cloud-based attestation of devices** - the devices
    used in a personal zone could also be attested to ensure that they
    have some minimum configurations that ensure protection of personal
    zone asserts. The Attestation API, already implemented in webinos,
    could be used more often to identify devices and their
    configurations. This could also serve as a basis for identifying the
    possible behaviour of *virtual PZPs* before admitting them to the
    personal zone.

<!-- -->

-   **Use of cloud based intrusion detection and traffic analysis** -
    the issue of inadequate logging and monitoring facilities in the
    cloud has significant impact on the security and privacy of the PZH.
    For this reason, it is essential that logging and tracking
    mechanisms are employed to track events on a cloud host and to
    detect and find the cause of breaches. Dedicated log servers and
    intrusion detection systems capable of collecting security relevant
    events must be used all the time.

<!-- -->

-   **Reclaiming cloud-based data** - one advantage that cloud-based web
    applications may gain from webinos is the ability to store data
    reliably on the user's own platform. At present, web applications
    such as Google Docs store data centrally, to provide access from
    anywhere, backup, and synchronisation. As webinos will provide these
    through the PZH and its own infrastructure, private data can be
    reliably stored using browser local storage. This has advantages for
    privacy: while this data is still accessible to the application, if
    the user decided to delete it, the data is no longer available.
    Furthermore, the user can enforce their own policies for passing
    data to a third party. This may be an advantage for application
    providers, as they will be able to avoid data protection
    requirements by not holding personal data themselves.

<!-- -->

-   **Better and verifiable VM provenance** - the VMs used to host the
    PZH might introduce vulnerabilities due to improper configuration or
    use of vulnerable components. For this reason, the provenance of the
    VMs must be securely collected in a manner that enables verification
    of key properties
    ([NamilukoVMProvenance2012](NamilukoVMProvenance2012.html)). This
    provenance should include the origin and integrity of the components
    used, the configurations applied and operations performed to prepare
    the VM in readiness for use in hosting a PZH.

<!-- -->

-   **PZH architecture considerations** - the PZH could be designed
    using several approaches. For example, the current implementation is
    such that the PZH operates similar to a monolithic kernel - storing
    all the data and providing all the services from a single component.
    Other alternative designs should be careful considered and evaluated
    to determine how they fair against cloud related threats. This work
    will be performed as part of stages 2 and 3 in the analysis, as
    discussed above.

Summary and conclusion[¶](#Summary-and-conclusion)
--------------------------------------------------

The promise of unlimited resources, on-demand service and pay-per-use
model of cloud computing is significantly attractive to webinos.
However, the use of cloud computing has the potential to expose webinos
to significant security and privacy risks. While several attempts have
been made to identifying and classifying cloud-related security and
privacy issues, these need to be put into context in order to understand
how the use of a cloud could affect webinos. This understanding enables
users to make informed decisions about the choice of a cloud environment
for webinos. To a user thinking about deploying a PZH in the cloud,
understanding the kinds of assets such as credentials and
synchronisation data that could exist in the cloud and the threats that
these could be exposed to is vital in deciding whether or not the risks
of running a PZH in the cloud are worth taking. To a provider, or indeed
some one thinking about offering PZH services to other users, this
understanding is vital in deciding the level of risk that their
customers would be exposed to as well as in deciding how much of the
responsibility they would be willing to carry. This section provides
information necessary to develop such an understanding. By analysing the
functionality of a PZH, several critical asserts were identified. These
include media content, credentials such as private keys used in
authentication, PZH users list and calendar data such as contacts and
appointment schedules.

### Key Findings[¶](#Key-Findings)

The key findings of the investigations in this section can be summarised
as follows:

-   webinos can take advantage of flexible, on-demand and pay-per-use
    services enabled by the adoption of a cloud-based system,
-   security and privacy issues must, however, be identified,
    characterised and addressed before webinos can take full advantage
    of cloud computing,
-   the analysis demonstrates that significant number of assets may be
    exposed to common security and cloud-specific threats and therefore
    require careful consideration of the risks involved,
-   vulnerabilities in the underlying infrastructure or environment used
    to host a PZH or resulting from inherent characteristics of cloud
    computing or the technology it employs could be exploited to
    compromise the security and privacy of the assets on a PZH,
-   a number of mitigations could be employed to reduce or eliminate
    some of the threats, such as better architecture for the PZH that
    employs principles such as separation of concern and security
    in-depth. However, certain kinds of threats such as compliance and
    jurisdiction may be outside the reach of webinos, instead, webinos
    would have to hope for a quicker maturity in the cloud offerings.

### Recommendations[¶](#Recommendations)

This section has presented the threats and vulnerabilities that a
cloud-based PZH could be exposed and which *Alice* would have to aware
about. But what does this mean to *Alice*, or anyone thinking about
using webinos in the cloud? Based on the analyses performed, the
following recommendations are provided:

-   **Minimal PZH services** - the architecture of the PZH must be
    designed with a minimal set of services following the principle of
    separation of concern. The impact of the architecture of the PZH on
    security and privacy will be investigated as part of stages 2 and 3
-   **Secure design principles** - well known security principles such
    as security in-depth and separation of concern must be employed in
    the design of the PZH, while other principles such as security by
    obscurity must be avoided.
-   **Transparency** - cloud offerings must be more transparent to allow
    the users to see the configurations of their instances, staff hiring
    procedures and management processes involving their data and
    credentials.
-   **More research in personal clouds** - webinos bridges the gap
    between a user's devices, allowing them to share data and services.
    The use of the cloud makes this more interesting, inspires
    creativity and opens up a number of challenges in terms of how this
    personal space, which was initially restricted to physical devices,
    can be securely managed. This calls for further research. Perhaps
    more collaboration with projects such as TClouds could have mutual
    benefits to webinos and other projects.
-   **To *Alice* on hosting a cloud-based PZH** - *Alice* can go ahead
    and set-up a personal zone with minimal devices and keep her VM up
    to date. Furthermore, she must take advantage of current security
    mechanisms such as secure cloud storage and take advantage of the
    latest advancements in cloud security.

### How will this analysis be useful in the future?[¶](#How-will-this-analysis-be-useful-in-the-future)

One of the efforts that have already began is putting the attacks within
the context of the webinos architecture. For example the Architectural
Risk Analysis involved creating attack patterns for various aspects of
webinos and linking them to architectural patterns for the purpose of
understanding how the architecture deals with these threats. The work
presented in this section could be used as a first step towards
understanding webinos architecture's readiness for the cloud.

