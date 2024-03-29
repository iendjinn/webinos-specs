Analysis - JavaScript, BONDI and Android[¶](#Analysis-JavaScript-BONDI-and-Android)
===================================================================================

Java Script Access Control:[¶](#Java-Script-Access-Control)
===========================================================

-   JavaScript API Access Control layer: Controls access to all
    JavaScript APIs exposed by the Web Runtime. Each Feature is
    identified uniquely by URI, and this security layer mediates access
    to Features on the basis of that ID.
-   Device Capability Access Control layer: Controls access to the
    underlying capabilities of the device when used from JavaScript
    APIs. These Device Capabilities themselves are identified so that it
    is possible to write security policies that control access to
    specific capabilities independently of the JavaScript APIs used to
    access them.

The Javascript Privileges API line of code asking permission to enable a
privilege which allows a script to access a target.

**For example**:

netscape.security.PrivilegeManager.enablePrivilege("UniversalPreferencesRead")\
or\
netscape.security.PrivilegeManager.enablePrivilege("UniversalPreferencesWrite")

**Privileges in Browser**:\
Privilege in Browser represents permissions to access a specific
target.\
• UniversalBrowserRead - Reading of sensitive browser data. This allows
the script to pass the same origin check when reading from any
document.\
• UniversalBrowserWrite - Modification of sensitive browser data. This
allows the script to pass the same origin check when writing to any
document.\
• UniversalXPConnect - Unrestricted access to browser APIs using
XPConnect\
• UniversalPreferencesRead - Read preferences using the
navigator.preference method.\
• UniversalPreferencesWrite - Set preferences using
thenavigator.preference method.\
• UniversalFileRead - Access to file:// URLs.

BONDI Access Control:[¶](#BONDI-Access-Control)
===============================================

-   The BONDI model is defined using concepts, terminology and semantics
    from the eXtensible Access Control Markup Language (XACML)
    framework.
-   BONDI policies are capable of representation in a compact XML format
    (and other formats, including a compact binary representation if
    necessary).
-   It is intended that BONDI policies are also eventually capable of
    representation in XACML, using a specific dictionary of attributes
    and a subset of XACML elements; however this is not currently
    possible without defining a number of extensions to XACML. It is
    hoped that this becomes possible with future revisions of the XACML
    standard.

**Logical Model**:

-   The BONDI access control system, from a logical perspective,
    mediates any attempt by an executing Web Application to access
    Device Capabilities using JavaScript APIs.
-   The access control system, implementing a specific access control
    policy, has the sole effect of making and enforcing an access
    control decision in relation to each attempted access.
-   In order to make that decision the access control system may request
    interactive confirmation from the user, but this is invisible to the
    requesting Web Application.

**Policy Structure**:

-   The policy in effect in any given context is logically expressed as
    a collection of specific access control rules. The rules are
    organised into groups, termed policies, and these in turn are\
     organised into groups termed policy sets.
-   It helps to organise the rules into groups that can be independently
    created and maintained, sometimes under different authority
-   It provides a way of ensuring that the correct precedence is applied
    when processing rules.

**Security Policy**:

-   A collection of access control constraints, abstractly representable
    as a policy-set, as defined in the security policy model in this
    specification, that describes the circumstances under\
     which Web Applications are permitted to access Features and
    underlying Device Capabilities.
-   A security policy configuration must be created and maintained this
    could be the source of usability problems and security
    vulnerabilities BONDI establishes a minimum common baseline for
    security policy management capability to ensure that web runtimes
    are manageable, the associated configuration data are interoperable
    between consuming devices.

**Security Framework**:

Proposes a general security framework that unifies the modeling,
representation and enforcement of security policies. It allows the
expression of different forms of security policy based on widget
resource signatures and blacklists and/or whitelists of widgets, authors
and websites. A compact XML-based interchange format is defined.

A model for the structure and meaning of security policies is defined.
The model identifies:

-   identity types
-   resources
-   attributes
-   conditions

**Widget Signing requirement**:

widgets must be signed according to the W3C Widgets 1.0 digital
signature specification the signature allows the web runtime to verify
the integrity and authenticity of every file widgets must have a valid
author signature and one or more valid distributor signature the web
runtime must support processing of certificates that conform to the
Wireless Application Protocol WAP Certificate and CRL Profiles
Specification.

**Feature access**:

The dependencies of BONDI web applications are indicated in terms of one
or more features a feature corresponds to specific functionality
provided by a web runtime. The web runtime shall only enable a web
application to use a JavaScript API if a dependency has been explicitly
expressed access to the feature has been granted.

The web runtime must resolve all dependencies of features referenced
statically at install time at instantiation time for widget resources
that are instantiated without prior installation for each referenced
feature, the web runtime shall evaluate an access control query.

The web runtime shall only grant access to features that are advertised
as being dependencies of the web application this requires that the
access control system is able to control access based on the ID of a
feature it must be possible to represent security policies portably all
identifiers used in a security policy shall be portably defined (feature
and device capabilities).

**Access Control Policy Structure**:

The policy is expressed as a collection of specific access control
rules. The rules are organized into groups, termed policies and these in
turn are organized into groups termed policy sets each rule is specified
by defining a condition, which is a set of statements which shall be
satisfied in order for that particular rule to apply an effect, which
represents the rule’s outcome.

**Security Policy Management**:

A web runtime shall use a configured security policy as the sole basis
on which access control decisions are made verify that each use of each
feature is permitted by evaluating the feature request against the
configured security policy. Only accept signed security policies from
authorized security policy provisioning authorities support at least one
security policy provisioning authority.

Android:[¶](#Android)
=====================

This section deals in identifying the use of security, permissions,
privileges, application signing, User ID’s, File access, enforcing
permissions in Android manifest.xml, network interface, Package Manager,
manifest permission, access controls related to Android.

**Security and Permissions**:

-   Android is a privilege-separated operating system.In which each
    application runs with a distinct system identity (Linux user ID and
    group ID).
-   Security features are provided through a "permission" mechanism that
    enforces restrictions on the specific operations that a particular
    process can perform, and per-URI permissions for\
     granting ad-hoc access to specific pieces of data.

**Application Signing**:

-   All Android applications (.apk files) must be signed with a
    certificate, private key is held by their developer.
-   This certificate identifies the author of the application.
-   The certificate does not need to be signed by a certificate
    authority: it is perfectly allowable, and typical, for Android
    applications to use self-signed certificates.
-   This allows the system to grant or deny applications access to
    signature-level permissions and to grant or deny an application's
    request to be given the same Linux identity as another application.

**User ID’s, File access and Permissions**:

-   At install time, Android gives each package a distinct Linux user
    ID.
-   The identity remains constant for the duration of the package's life
    on that device.
-   On a different device, the same package may have a different UID;
    what matters is that each package has a distinct UID on a given
    device.
-   By including in Android Manifest.xml one or more \<uses-permission\>
    tags declaring and enforcing the permissions that an application
    needs.

**Enforcing Permissions in AndroidManifest.xml**:

-   High-level permissions restricting access to entire components of
    the system or application can be applied through your
    AndroidManifest.xml
-   Activity permissions (applied to the \<activity\> tag) restrict who
    can start the associated activity. The permission is checked during
    Context.startActivity() and\
     Activity.startActivityForResult()
-   The permissions are checked when you first retrieve a provider (if
    you don't have either permission, a SecurityException will be
    thrown).

**Access Controller privileges**:

-   Java security has a special class called ‘Access Controller’
-   AccessController provides static methods to perform access control
    checks and privileged operations.

It supports some methods such as:

-   checkPermission: Checks the specified permission against the VM's
    current security policy.
-   doPrivileged(PrivilegedExceptionAction\<T\> action) Returns the
    result of executing the specified privileged action.
-   doPrivileged(PrivilegedExceptionAction\<T\> action,
    AccessControlContext context) Returns the result of executing the
    specified privileged action.
-   static AccessControlContext: Returns the AccessControlContext for
    the current Thread including the inherited access control context of
    the thread that spawned the current thread (recursively).

**Network Interface**:

-   getHarrdwareAddress() : Returns the hardware address of the
    interface, if it has one, and the user has the necessary privileges
    to access the address.

**Package Manager**:

-   GET\_PERMISSIONS: return information about permissions in the
    package in permissions.
-   GET\_SIGNATURES: return information about the signatures included in
    the package.
-   PERMISSION\_DENIED: checks if the permission has not been granted to
    the given package.
-   PERMISSION\_GRANTED: checks if the permission has been granted to
    the given package.
-   SIGNATURE\_MATCH: if all signatures on the two packages match

**Manifest Permission**:

-   CALL\_PRIVILEGED: Allows an application to call any phone number,
    including emergency numbers, without going through the Dialer user
    interface for the user to confirm the call being placed.
-   Manifest.permission\_group: Permissions for direct access Account
    Manager, Hardware Control, Location, Messages, Network, Personal
    Info, Storage, System Tools.

Terminology:[¶](#Terminology)
-----------------------------

**Privileged Application**\
A Privileged application is signed with a certificate that is in the
privileged certificate store on the device. Target an application based
on its Digital Certificate.

A Privileged application is an application that can override system
controls and check for specific user IDs (UIDs), group IDs (GIDs),
authorizations, or privileges. The access control elements are assigned
by system administrators.

**Privileges** - A privilege is a discrete right that can be granted to
an application. With a privilege, a process can perform an operation
that would otherwise be prohibited. For example, processes cannot
normally open data files without the proper file permission. Privileges
are enforced at the kernel level.

**Authorizations** - An authorization is a permission for performing a
class of actions that are otherwise prohibited by security policy. An
authorization can be assigned to a role or user. Authorizations are
enforced at the user level.

The difference between authorizations and privileges has to do with the
level at which the policy of who can do what is enforced. Privileges are
enforced at the kernel level. Without the proper privilege, a process
cannot perform specific operations in a privileged application.

**Privilege Monitoring**: Privilege Monitoring will log privileged
application activity that would fail under a standard user account. For
an application to log activity you must enable Privilege Monitoring in
the Application Privileges or Shell Integration sections of the policy,
when you insert an application group.

**Installers**: A Privileged Application provides a policy based
approach to privilege management. All users log on with standard user
accounts and Privilege Application assigns the necessary rights and
privileges to applications, scripts and software installers. Installers
of the Privilege Application run through the console and client.

**Launcher**: The launchers of the Privilege application Policies for
the users will automatically elevate these applications when they are
launched.

**Policy Manager**: A Privilege Application is implemented as an
extension to Group Policy, enabling policies to be managed through the
standard Group Policy Management tools.

**Dashboard**: The Privileged Application can provide information
related to Date, Event ID, Event Description, Username, PID, Parent PID,
Policy, Application Group, Reason, Custom Token, Filename/Codebase,
Type, Instances, Description, Certificate which can be shown in a
Dashboard format for example to view in the form of graphs like area,
bar, line and so on. Auditing and reporting capabilities can also be
viewed by the help of Dashboards.

