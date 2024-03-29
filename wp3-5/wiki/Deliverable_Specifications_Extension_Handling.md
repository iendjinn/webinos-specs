Security for Extensions[¶](#Security-for-Extensions)
----------------------------------------------------

### Introduction[¶](#Introduction)

Webinos extensions will be based on the NPAPI Standard; this raises
several security risks which have to be reflected in the webinos
security architecture. The architecture has to balance the security of
the whole system on the one side and the flexibility of extensions on
the other. An extension requires access to the underlying operating
systems by definition, but breaks the natural sandbox of the browser
runtime.

### Background[¶](#Background)

#### Requirements[¶](#Requirements)

The requirements for the extensions handling focus on the secure
execution of applications (known behaviour of the application), the user
awarness of the functionality and risks exposed by extentsions and the
possibility of the user to control the access to extensions. These
requirements apply to the some extend to the generic access of device
resources.

This section of the specification aims to satisfy (partially) the
following requirements:

-   [PS-USR-Oxford-17](/wp2-2/wiki/DeliverableVersionAll#PS-USR-Oxford-17)
    : The webinos Runtime Environment shall be capable of setting
    dynamic access control policies for device data when initiating an
    association to another webinos Device.
-   [PS-USR-Oxford-106](/wp2-2/wiki/DeliverableVersionAll#PS-USR-Oxford-106)
    : When installing or using an application for the first time,
    webinos shall make sure that the user trusts the source of the
    application.
-   [PS-USR-Oxford-116](/wp2-2/wiki/DeliverableVersionAll#PS-USR-Oxford-116)
    : The webinos Runtime Environment shall protect applications and
    itself from potentially malicious applications and shall protect the
    device from being made unusable or damaged by applications.
-   [PS-DEV-ambiesense-25](/wp2-2/wiki/DeliverableVersionAll#PS-DEV-ambiesense-25)
    : The webinos runtime shall protect policies from tampering or
    modification by unauthorised applications. The only authorised
    applications shall be from signed, trusted sources, which may be
    defined by the manufacturer, network provider, or end user.
-   [PS-DWP-ISMB-202](/wp2-2/wiki/DeliverableVersionAll#PS-DWP-ISMB-202)
    : The webinos runtime must ensure that an application does not
    access device features, extensions and content other than those
    associated to it.
-   [PS-USR-Oxford-53](/wp2-2/wiki/DeliverableVersionAll#PS-USR-Oxford-53)
    : webinos policies shall be capable of referring to and specifying
    restrictions on device capabilities and features, application data,
    context and personal information held in webinos, and access to
    other devices and applications.
-   [PS-USR\_DEV-Oxford-44](/wp2-2/wiki/DeliverableVersionAll#PS-USR_DEV-Oxford-44)
    : Applications shall specify at install time (or first use) the
    functionality they require access to.
-   [PS-USR\_DEV-Oxford-45](/wp2-2/wiki/DeliverableVersionAll#PS-USR_DEV-Oxford-45)
    : Users shall be able to specify at application install time (or
    first use) which functionality they permit an application to have
    access to.
-   [PS-USR\_DEV-Oxford-46](/wp2-2/wiki/DeliverableVersionAll#PS-USR_DEV-Oxford-46)
    : Applications shall request for access rights to any device feature
    or policy-controlled item prior to accessing it. If an access
    request is denied, applications shall be notified to deal with this
    gracefully.

#### Related technology and research[¶](#Related-technology-and-research)

Browser vendors have integrated mechanisms to secure the usage of NPAPI
plug-ins:

-   Chrome and Firefox are using a built-in generic NPAPI plug-in for
    identifying missing but required plug-ins. As a back-end
    infrastructure for this; Mozilla and Google maintain a repository
    for trusted NPAPI plug-ins
    ([MozillaPluginDirectory](MozillaPluginDirectory.html)). The generic
    plug-in queries the hosted directory for a trusted plug-in
    supporting the unknown MIME-Type, downloads the binary and stores
    the plug-in binary inside the common plug-in folder of the device to
    enable the usage by the browser.

<!-- -->

-   For Chrome extensions embedding NPAPI plug-ins inside extension
    package, Google does not publish the extension on their Chrome app
    store until the extension has been tested against malicious
    behaviour of the NPAPI plug-in.
    ([ChromeNpapiExtensions](ChromeNpapiExtensions.html))

<!-- -->

-   Furthermore, Google introduced the Native Client (NaCl) to enable
    the secure execution of native code inside the browser environment.
    But this concepts reduces the possible functionality of an extension
    significantly ([GoogleNativeClient](GoogleNativeClient.html)). The
    NaCl runtime prohibits all access to OS services (e.g. network or
    file system).

<!-- -->

-   The Firefox add-on "NoScript" illustrates how the user can enable or
    disable specific plug-ins for certain origins (protocol, domain,
    port) depending on his choice. ([NoScript](NoScript.html))

#### Threats[¶](#Threats)

NPAPI's unrestricted access to operating system - which is needed to
enable extensions in webinos - introduces infinite security risks, such
as:

-   Manipulation of the file system
-   Access to sensitive data
-   Uncontrollable network access

### Components[¶](#Components)

#### The application installer[¶](#The-application-installer)

For extensions that are part of the application package the application
installer verifies the signature of the package and allows or disallows
the installation of application including the plug-in accordingly.
Furthermore the application installer informs the user of the potential
security risks and enables the user to prohibit the installation of the
plug-in (defining policy). After the integrity of the application has
been verified and the user has approved the installation of the
application, the installer extracts the platform relevant NPAPI binary
from the application package and stores it inside the common plug-in
folder of the browser.

<div class="uml">title installation handling of a webinos application including extensions 
(*) --> "checking if application manifest contains plugins"
if "" then
	-->[yes] "check application signature"
	if ""  then
		--> [valid] "checking if platform is supported"
		if "" then
			--> [true] "check if policies for plug-in installation exists"
			if "" then
				--> [true] "check if installation is allowed"
				if "" then
					--> [notallowed] "continue with regular installation"
				else
					--> [allowed] "store plugin binary in the rendering engine specific folder"
				else
					--> [ask] "request permissions from user for installation of extensions"
				endif
				
			else 
				--> [false] "request permissions from user for installation of extensions"
				if "" then
					--> [allowed] "create policy for extensions usage of specific application"
					--> "store plugin binary in the rendering engine specific folder"
					--> "continue with regular installation"
				else
					--> [notallowed] "create policy for disabling extensions for the specific application"
					--> "continue with regular installation"
				endif
			endif

		else
			--> [false] "continue with regular installation"
		endif
	else
		--> [invalid] "abort installation of plugins and inform user about invalid signature"
		--> "continue with regular installation"
	endif
  else
	-->[no] "continue with regular installation"
	--> (*)
endif</div>

#### The application launcher[¶](#The-application-launcher)

The application launcher checks the application manifest and the
policies files regarding the usage of the extension and enables the
access to the plug-ins accordingly. The access to extensions is disabled
by default.

#### Secure storage for certificates[¶](#Secure-storage-for-certificates)

The secure storage is used to store the relevant policies and
certificates for the installation and execution of webinos extensions.

#### Application packaging: manifests and resources[¶](#Application-packaging-manifests-and-resources)

Inside the manifest the embedded plug-ins are defined, see
([Webinos-D31](Webinos-D31.html)) for more details.

### Future directions[¶](#Future-directions)

The current security concept focuses on the installation and execution
of verified plug-ins. Once the plug-in is installed it has the unlimited
the access to operating system and runs out of the control from the
incorporated security mechanisms.

Depending on the success of extensions in webinos on NPAPI basis, it
will be necessary to incorporate higher security measurements for
extensions on the client side. Nowadays NPAPI plug-ins is usually
executed in a separate OS process. When the browser spawns the new
process the process rights could be restricted to the OS services (e.g.
file access, network) required for the plug-in to be executed. *A
similar approach is done for NaCl: on Windows all privileges for the
NaCl process are limited.*

