Web application packaging handling and Web Runtime specification[¶](#Web-application-packaging-handling-and-Web-Runtime-specification)
======================================================================================================================================

Application handling and packaging covers the description, packaging and
handling of webinos applications as well as the handling and
presentation (start, stop, install, remove, and update) of webinos
applications on the device itself, i.e., how webinos web runtime
environments have to deal with webinos applications.

Link to Turin meeting thematic area introduction at BSCW:
<http://bscw.fokus.fraunhofer.de/bscw/bscw.cgi/d703252/Task%203.1%20Widget%20Handling%20Turin.pdf>

**Up to now specification work in this theme is divided in three
sub-tasks: Webinos Application Specification, Webinos Web Runtime
Environment Specification and Distributed Application Specification**

-   Webinos Application Specification is about how webinos applications
    are technically looking (web site vs. widgets)
-   Webinos Web Runtimie Environment Specification is about requirements
    of the web runtime (supported standards, look and feel / UI, life
    cycle, mandatory runtime features)
-   Distributed Application Specification is about how applications can
    be executed in a distributed manner (some code is running on device
    A and some other code is running on device B etc.)

Partners Involved in this Theme[¶](#Partners-Involved-in-this-Theme)
--------------------------------------------------------------------

According to the [minutes from Turin](minutes%20from%20Turin.html)

-   FOKUS
-   Impleo
-   W3C

*Security and privacy contacts: Impleo, W3C.*

Dedicated Topic Sub-pages[¶](#Dedicated-Topic-Sub-pages)
--------------------------------------------------------

-   [Webinos Core](.html)
-   [Webinos Application Specification Open Questions](.html)

Webinos Application Specification[¶](#Webinos-Application-Specification)
------------------------------------------------------------------------

-   Common web site\
     - Give normal web sites access to webinos JS APIs and how would the
    security/policy integration be realized (e.g.a definition of “some
    kind of config.xml for web sites to express their dependencies on
    features). Should we take care on this in the first phase?

<!-- -->

-   Downloadable, exchangeable, installable application\
     - E.g., packaged as W3C Widget
    <http://www.w3.org/2008/webapps/wiki/WidgetSpecs>\

    `Widget: interactive single purpose application for displaying and/or updating local data or data on the Web, packaged in a way to allow a single download and installation on a user's machine or mobile device`\
     - According to webinos requirements some more meta data tags must
    be introduced. For example, information about the distributor,
    potential destination for analytic data,human readable as well as
    machine processable version name, identification of personal and
    widget related data.\
     - Less effort: use and extend (mostly related to meta data
    definitions) w3c widget\
     - Medium effort: accessing applications using common web page
    approaches and make them offline available via app cache (define a
    manifest that contains more than just needed files for offline mode,
    equal to content of the w3c widget config.xml, how to exchange "app
    chached" applications between devices =\> define exchange format,
    e.g., app cache to widget)\
     - Large effort: investigate new application model that takes care
    on the distributed fashion of webinos applications where different
    parts of applications may run on different devices (how to sign
    applications across devices, how to access and create policy
    statements without the need of a packaged application, distributed
    meta data access...)

Webinos Web Runtime Environment Specification[¶](#Webinos-Web-Runtime-Environment-Specification)
------------------------------------------------------------------------------------------------

-   What have Webinos runtimes at least to provide in order to be
    webinos compliant (from users point of view as well as architectural
    needs)\
     - webinos application Life-cycle definition (install, use, update,
    delete)\
     - allow user to install/delete applications using various
    mechanisms (e.g., via app store/client, via web site, via another
    webinos device, via file system)\
     - UI: e.g., accessing webinos applications must follow the native
    OS approach of accessing applications\
     - multitasking\
     - trigger application execution based on user request or
    internal/external events (e.g., on boot completed, incoming external
    event, requested by another application)\
     - Show user information about applications (icon, author,…)\
     - Secure storage of applications but also transportable by user?\
     - Application Advertisment: discover and present applications
    available to the user which can be installed/used later on (not only
    locally installed applications but also apps provided by other
    devices (e.g. TV remote control or electronic program guide (EPG)
    applications which are provided by the TV set))\
     - How to setup applications which should be available using
    advertisement methods. For example, providing an API which allows
    applications to be discoverable by others (or via native runtime
    functions, or via config.xml/manifest?)\
     - how to handle webinos applications running in background (webinos
    services / no UI applications)\
     - Policy Runtime Environment integration. For example, mandatory
    needs to the runtime like policy editor, remote policy exchange,
    transportable policies (depends on policy management working
    group).\
     - Do we have "No UI" / "No Display" runtimes and if so how will
    they be managed\
     - In addition to application advertisement, should applications be
    able to expose certain functionalities as services?\
     - Possible Reference Specification WAC Waikiki
    <http://www.wacapps.net/web/portal/wac-2.0-spec>

<!-- -->

-   Application code compliance definition (high level: applications
    will be based on web technology programming paradigms)\
     - Which standards have webinos web runtimes to support (HTML x.y,
    CSS x.y, ECMAScript/JavaScript x.y, ...)\
     - For WRTs with user interface WAC 2.0 sufficient for now?\
     - Subset for runtimes with no UI / do we have some?\
     - Possible Reference Specification WAC Waikiki
    <http://www.wacapps.net/web/portal/wac-2.0-spec>

Distributed Application Specification[¶](#Distributed-Application-Specification)
--------------------------------------------------------------------------------

-   Provide possibilities to application developer to “outsource” code
    to other devices in order to be remotely executed. E.g, for
    performance, security, or application rendering reasons.\
     - Transmit code to other device\
     - Trigger execution of desired code fragments\
     - Back channel to “originating” application to allow communication
    between originator and outsourced code
-   Potential outsourcing possibilities (each with pros and cons, which
    one to go for?). Strongly related to the webinos application
    format:\
     - Webinos applications can act as web server by providing
    discoverable web sites\
     - Webinos applications can initiate “cloning” of itself to be
    installed on another device where a specific start-up parameter
    could be provided to go on at a certain code fragment\
     - Webinos application could explicitly transmit only a piece of
    code to other devices. Could be pre-defined code (the developer
    defines which code fragments might be used for code outsourcing,
    "widgets within a widget") or could be dynamic code (e.g.,
    dynamically created by the application or requested from code
    repositories). How to sign dynamic code based on the "parent"
    application signature?

Related Specification Topics[¶](#Related-Specification-Topics)
==============================================================

-   Event handling: some predefined events must be defined (e.g., to
    execute applications based on events)
-   (Application) Discovery: Runtime Environment must be able to detect
    available applications in order to advertise them to the user (e.g.,
    based on ownership or physical distance)
-   Policy Management: WRE must be compliant to policy management
    specification. The user may have the option to import/export/edit
    policies what can be done using the WRE.

Time Plan[¶](#Time-Plan)
========================

  ------------------ ------------------ ------------------ ------------------
  Item               Due                Lead               Status

  Analysis of        March 23                              started
  potential webinos                                        
  application                                              
  definitions                                              

  Analysis of        April 6                               started
  potential                                                
  application                                              
  distribution                                             
  mechanisms                                               

  WRE: Application   March 16                              
  advertisement                                            
  (draft)                                                  

  WRE: Application                                         
  Life Cycle                                               

  WRE: Web Standards                                       
  (referring to                                            
  WAC?)                                                    

  WRE: Security and                                        
  Privacy                                                  
  Integration                                              

  WRE: UI and other                                        
  features                                                 
  ------------------ ------------------ ------------------ ------------------


