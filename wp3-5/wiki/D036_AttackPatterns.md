Contextualised Attack Patterns[¶](#Contextualised-Attack-Patterns)
==================================================================

This section was automatically generated based on the contents of the
webinos WP 2 git repository at <http://dev.webinos.org/git/wp2.git>.

Obstacle probability: colour codes[¶](#Obstacle-probability-colour-codes)
-------------------------------------------------------------------------

![](ObsColour.jpg)

Application DoS[¶](#Application-DoS)
------------------------------------

### Intent[¶](#Intent)

Harold has developed a webinos application he is very proud of.
Unfortunately it is not receiving much attention because another app
(which he believes to be inferior) is extremely popular. Harold decides
to get rid of the competition, which he feels will be best for everyone:
he gets the recognition he deserves and users get a better experience.

### Motivation[¶](#Motivation)

  Security Goal   Value   Description
  --------------- ------- ---------------------------------------------------
  Availability    High    Users become unable to reliably use a certain app

### Structure[¶](#Structure)

  ----------------------------------------------------------- --------------- ----------------------------------------------------------
  Attack: Malicious Automated Software Update                 Origin: CAPEC   Obstacle: The Application is auto-updated by an attacker
  Exploit: Improper Verification of Cryptographic Signature   Origin: CWE     Obstacle: Application signing key not checked
  ----------------------------------------------------------- --------------- ----------------------------------------------------------

### Participants[¶](#Participants)

  Attacker   Motives   Capabilities (Value)
  ---------- --------- -------------------------------------------
  Harold     Money     Knowledge/Methods(High), Software(Medium)

### Collaboration[¶](#Collaboration)

  --------- --------------------
  Target    Application Module
  Exploit   Widget Processor
  --------- --------------------

### Implementation[¶](#Implementation)

![](Application_DoSObstacleModel.jpg)

Harold performs a denial of service attack on an application, rendering
it unusable by end users.

### Obstacles[¶](#Obstacles)

  Obstacle                                                   Category        Definition
  ---------------------------------------------------------- --------------- -----------------------------------------------------------------------------------------------------------------------------------------------------
  Application blacklisted after negative reviews             Vulnerability   The application is given several negative reviews and warnings on app stores and social networks, putting it on a blacklist
  Application developer signing key compromised              Vulnerability   The application developer's signing key is leaked to the attacker, perhaps due to it being embedded in a source file or another means.
  Application impossible to use                              Vulnerability   A webinos application is no longer usable
  Application signing key not checked                        Vulnerability   Update procedure does not check that the update signing key matches the original signing key
  Bad default policy                                         Vulnerability   The default webinos policy settings are too restrictive
  Bad user-selected policy                                   Vulnerability   The user has selected bad policy settings
  Badly configured policy                                    Vulnerability   The webinos policy settings are poorly chosen and the application is denied access to too many APIs
  Hosted application is attacked through content injection   Vulnerability   The application's hosted components are attacked via a content injection attack, possibly XSS.
  JavaScript injection overwrites webinos.js                 Vulnerability   Injected javascript prevents the application from accessing PZP functionality by overwriting webinos.js
  JavaScript injection triggers security violation           Vulnerability   Injected javascript causes the application to trigger security warnings and get disconnected by the PZP or webinos runtime
  The Application is auto-updated by an attacker             Vulnerability   The application downloads an update automatically and installs it. However, the update was issued by an attacker rather than the application author
  Webinos backdoor                                           Vulnerability   The webinos platform is updated to specifically target this application and render it unusable

Capture Hidden Analytics[¶](#Capture-Hidden-Analytics)
------------------------------------------------------

### Intent[¶](#Intent)

Subversely capture analytics about application usage.

### Motivation[¶](#Motivation)

  Security Goal   Value   Description
  --------------- ------- -------------------------------------------------------------------------------
  Anonymity       High    Jimmy relies on anonymity to capture context data without users realising it.

### Structure[¶](#Structure)

  ---------------------------------- --------------- ---------------------------------
  Attack: Spyware                    Origin: OWASP   Obstacle: None
  Exploit: Lack of data provenance   Origin: D2.8    Obstacle: Apps share usage data
  ---------------------------------- --------------- ---------------------------------

### Participants[¶](#Participants)

  Attacker   Motives   Capabilities (Value)
  ---------- --------- ---------------------------------------------
  Jimmy      Money     Knowledge/Methods(Medium), Software(Medium)

### Collaboration[¶](#Collaboration)

  --------- ----------------
  Target    Analytics Data
  Exploit   Analytics Data
  --------- ----------------

### Implementation[¶](#Implementation)

![](Capture_Hidden_AnalyticsObstacleModel.jpg)

Peter is about to head to Berlin for a long weekend and decides to
download the Berlin Gallery Guide from the Android app store. This
application gives Peter a quick overview of art galleries in Berlin and
allows him to take snaps and submit reviews about places visited. Before
downloading the app, Peter checks what the application has access to.
Additionally, before running the app for the first time, he also scans
the application's terms and conditions, briefly noting that the
application captures information about time. Several days later, Peter
is walking out of the Neue Nationalgalerie and submits some of his
thoughts about the gallery as a review.

One month earlier, Jimmy was in the midst of a dilemma. His Berlin cafe
guide was more successful than he thought, but he really wished that he
had captured more analytics information; his new Berlin Gallery Guide
might be just the opportunity he needs to get this data. While Peter
really wants to capture information about location rather than time of
review, this would mean re-drafting the privacy policy associated with
the app to better reflect his intentions; this is both time consuming
and, to his mind, unnecessary. "I mean" Jimmy thought, "I'm the only
person using the data, and I'm not going to abuse it so who really cares
if I capture location data rather than time in my app. The PDP
associated with the running application won't notice the difference and,
perhaps, maybe that means capturing this data is ok." Eventually, Jimmy
convinces himself to reuse his previous privacy policy and configuration
file entries related to permission, but change the Javascript code to
store location data as context data rather than time.\
Several weeks later, Jimmy feels vindicated by this decision as useful,
fine-grained location data starts to arrive via his gallery guide app,
including unauthorised location data arising about Peter's visit to Neue
Nationalgalerie.

### Obstacles[¶](#Obstacles)

  Obstacle                                             Category        Definition
  ---------------------------------------------------- --------------- ------------------------------------------------------------------------------------------------------------------------------------------------------
  Application has user identifier without permission   Vulnerability   One application is installed and is able to obtain a user identifier without requesting access to an API for this.
  Apps share usage data                                Vulnerability   The two application share usage data, either directly or through an intermediary analytics service
  findService API reveals permanent user identifier    Vulnerability   The output of the findServices API is an effective user identifier.
  Independent apps have common identifier for user     Vulnerability   Two or more independent applications have been installed in the personal zone and have the same user identifier.
  User identity tracked between applications           Vulnerability   An application is able to successfully re-identify a user of a different application despite them restricting access to personally-identifying APIs.

Device availability loss[¶](#Device-availability-loss)
------------------------------------------------------

### Intent[¶](#Intent)

Part of a larger attack, Ethan tries to drum-up interest in his own
"battery life extender" application by rendering his victim's devices
unusuable due to battery life problems that he has caused.

### Motivation[¶](#Motivation)

  Security Goal   Value    Description
  --------------- -------- -----------------------------------------------------------------------------
  Availability    Medium   The device rapidly becomes unavailable as battery life is spent too quickly

### Structure[¶](#Structure)

  -------------------------------------------------------------------- --------------- ------------------------------------------
  Attack: Denial of Service through Resource Depletion                 Origin: CAPEC   Obstacle: Device effectively unavailable
  Exploit: Uncontrolled Resource Consumption ('Resource Exhaustion')   Origin: CWE     Obstacle: Processor always busy
  -------------------------------------------------------------------- --------------- ------------------------------------------

### Participants[¶](#Participants)

  Attacker   Motives                 Capabilities (Value)
  ---------- ----------------------- -----------------------------------------------------------------
  Ethan      System resource theft   Knowledge/Methods(Medium), Software(Medium), Technology(Medium)

### Collaboration[¶](#Collaboration)

  --------- ------------------
  Target    Widget Processor
  Exploit   Widget Processor
  --------- ------------------

### Implementation[¶](#Implementation)

![](Device_availability_lossObstacleModel.jpg)

Ethan exploits commonly used web applications to drain the battery life
of users and encourage them to use his software.

### Obstacles[¶](#Obstacles)

  Obstacle                                     Category        Definition
  -------------------------------------------- --------------- ----------------------------------------------------------------------------------------------------------
  Battery exhausted                            Vulnerability   The device's battery is out of capacity
  Data storage limit reached                   Vulnerability   The local storage is full, preventing normal operation
  Device effectively unavailable               Vulnerability   The mobile device becomes effectively unusable for any function
  Installed app exploited                      Vulnerability   An installed application has been compromised and is now under the control of an attacker
  Installed app misbehaving                    Vulnerability   An installed and trusted application is behaving in unexpected ways with bad consequences
  Malicious background application installed   Vulnerability   A malicious webinos application has been installed
  Malicious background application running     Vulnerability   A background application is running and is behaving maliciously
  Native malware running                       Vulnerability   There is native malware installed on the device
  Processor always busy                        Vulnerability   The device's processor is constantly active, perhaps due to infinite loops or too many processes running
  Unnecessary use of APIs                      Vulnerability   APIs are being called repeatedly, just for the purpose of exhausting the device
  Webinos widget processor bug                 Vulnerability   The webinos platform contains a bug resulting in it acting unpredictably or looping infinitely
  XSS attack on hosted app                     Vulnerability   An installed app has been attacked through a XSS vulnerability, allowing code injection

Loss of personal zone administration access[¶](#Loss-of-personal-zone-administration-access)
--------------------------------------------------------------------------------------------

### Intent[¶](#Intent)

Part of a larger attack to misuse user credentials or perform identity
theft, an attacker deletes or changes the password on the user's OpenID
account.

### Motivation[¶](#Motivation)

  Security Goal     Value    Description
  ----------------- -------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Availability      Medium   The attacker makes the personal zone administration interface unavailable to the user, resulting in an inability to control policy or authentication in the zone
  Confidentiality   High     The attacker can view and misuse user personal zone data

### Structure[¶](#Structure)

  ------------------------------------- --------------- ----------------------------------------------
  Attack: Denial of Service             Origin: OWASP   Obstacle: PZH offline
  Exploit: Unverified Password Change   Origin: CWE     Obstacle: Password recovery process attacked
  ------------------------------------- --------------- ----------------------------------------------

### Participants[¶](#Participants)

  Attacker   Motives          Capabilities (Value)
  ---------- ---------------- ---------------------------------------------
  Frankie    Thrill-seeking   Knowledge/Methods(Medium), Software(Medium)

### Collaboration[¶](#Collaboration)

  --------- --------------------------------------
  Target    Personal Zone Administration Console
  Exploit   Identity Provider
  --------- --------------------------------------

### Implementation[¶](#Implementation)

![](Loss_of_personal_zone_administration_accessObstacleModel.jpg)

Frankie is attempting to gain access to personal accounts on a range of
popular websites, including email services and social networks. He
intends to deface public records of some people (those he knows and has
taken offense to) and maybe to expose a few people who he thinks are
arrogant and deserve to be knocked down a peg or two. To do this, he is
exploiting password recovery features and guessing commonly used "secret
phrases" for openid accounts based on user names he knows, as well as
some he has found on public forums. This resets user passwords and, as a
consequence, means that the real users can't authenticate against the
OpenID providers. Unfortunately for the victims, this also means that
they have lost access to their webinos personal zone administration
interface. Later on, Frankie realises that some of his victims are
running webinos, and he makes use of his access to their accounts to (in
some cases) delete files and settings, and in other cases secretly add
his own device to their personal zones.

### Obstacles[¶](#Obstacles)

  Obstacle                             Category        Definition
  ------------------------------------ --------------- -----------------------------------------------------------------------------------------
  Account deleted                      Vulnerability   The OpenID account was deleted by an attacker impersonating the user
  Account lock-out                     Vulnerability   The OpenID account has been "locked out" due to too many failed authentication attempts
  Authentication failure               Vulnerability   The OpenID authentication process refuses to authenticate the user
  Credentials changed                  Vulnerability   The OpenID account credentials have been changed by an attacker
  Forgotten credentials                Vulnerability   The webinos user has forgotten their credentials
  Loss of PZH admin access             Vulnerability   The PZH administration interface cannot be reached
  OpenID account inaccessible          Vulnerability   The OpenID process does not successfully authenticate the correct user to the hub
  OpenID provider offline              Vulnerability   The OpenID provider is unavailable
  Password guessed and reset           Vulnerability   The OpenID account password was guessed by an attacker and then reset
  Password recovery process attacked   Vulnerability   The OpenID account recovery procedure has been exploited to reset the password
  PZH offline                          Vulnerability   The PZH is not accessible over the internet

Exploit network bandwidth[¶](#Exploit-network-bandwidth)
--------------------------------------------------------

### Intent[¶](#Intent)

Exploit webinos to gain access to network provider resources.

### Motivation[¶](#Motivation)

  Security Goal   Value    Description
  --------------- -------- ---------------------------------------------------------------------------------------------------------------------------
  Integrity       Medium   Ethan's ability to manipulate media preferences and other personal or log data should be considered a significant attack.

### Structure[¶](#Structure)

  --------------------------------------------- --------------- ------------------------------------------
  Attack: Repudiation Attack                    Origin: OWASP   Obstacle: None
  Exploit: Permissive convergence preferences   Origin: D2.8    Obstacle: Spoof network settings message
  --------------------------------------------- --------------- ------------------------------------------

### Participants[¶](#Participants)

  Attacker   Motives                 Capabilities (Value)
  ---------- ----------------------- -----------------------------------------------------------------
  Ethan      System resource theft   Knowledge/Methods(Medium), Software(Medium), Technology(Medium)

### Collaboration[¶](#Collaboration)

  --------- ----------------------------
  Target    Personal Media Preferences
  Exploit   Personal Media Preferences
  --------- ----------------------------

### Implementation[¶](#Implementation)

![](Exploit_network_bandwidthObstacleModel.jpg)

Ethan has discovered that, invariably, webinos users have
over-permissive convergence settings between devices used in the home
and, with by altering the right settings, it is possible to change
network service settings. This is especially useful given that some
network providers, as part of their business model, allow users to
change their bandwidth settings online via webinos. This is a boon for
Ethan's botnet business the convergence affordances allow him to easily
increase the bandwidth available to his botnet clients.

A number of botnet client machines were running webinos, so he tried
connecting to one of them and running a customised webinos web service
client to discover any available webinos services. Sure enough, he
discovered a text input service running on a mobile phone. Ethan was
able to easily connect to this and manipulate the machine owner's "use
maximum bandwidth" setting. If he was lucky, the machine owner's network
provider would automatically increase this home's bandwidth without the
owner ever finding out.

### Obstacles[¶](#Obstacles)

  Obstacle                                Category                Definition
  --------------------------------------- ----------------------- ----------------------------------------------------------
  Post spoofed message                    Accountability Threat   Post spoofed message
  Spoof network settings message          Accountability Threat   Spoof network settings message sent to network provider.
  Spoof network settings message origin   Integrity Threat        Spoof network settings message origin.

Man In The webinos Browser[¶](#Man-In-The-webinos-Browser)
----------------------------------------------------------

### Intent[¶](#Intent)

Ethan wants to steal application data, either to find credit card
details, account details or to sell-on to advertisers or spammers

### Motivation[¶](#Motivation)

  Security Goal     Value   Description
  ----------------- ------- ------------------------------------------------
  Confidentiality   High    Ethan intercepts confidential application data

### Structure[¶](#Structure)

  ------------------------------------------------------------------- --------------- -----------------------------------------------
  Attack: Man-in-the-browser attack                                   Origin: OWASP   Obstacle: Application data intercepted
  Exploit: Inclusion of Functionality from Untrusted Control Sphere   Origin: CWE     Obstacle: Widget renderer supports extensions
  ------------------------------------------------------------------- --------------- -----------------------------------------------

### Participants[¶](#Participants)

  Attacker   Motives                 Capabilities (Value)
  ---------- ----------------------- -----------------------------------------------------------------
  Ethan      System resource theft   Knowledge/Methods(Medium), Software(Medium), Technology(Medium)

### Collaboration[¶](#Collaboration)

  --------- ------------------
  Target    Application Data
  Exploit   Rendering Engine
  --------- ------------------

### Implementation[¶](#Implementation)

![](Man_In_The_webinos_BrowserObstacleModel.jpg)

Ethan develops a browser plugin which allows him to intercept all
messages between the webinos widget renderer and the PZP, giving him
access to application data.

### Obstacles[¶](#Obstacles)

  Obstacle                              Category        Definition
  ------------------------------------- --------------- ----------------------------------------------------------------------------------
  Application data intercepted          Vulnerability   Application data from webinos widgets is intercepted in the widget renderer
  Application data readable             Vulnerability   Application data from webinos widgets is readable outside of the widget renderer
  Malicious plugin installed            Vulnerability   The user installs (or suffers from a driveby download) a malicious plugin
  Malicious plugin is running           Vulnerability   Malware in the form of a malicious widget renderer plugin is running
  Malicious plugin not detected         Vulnerability   Malware plugin not detected.
  Widget renderer supports extensions   Vulnerability   The widget renderer supports plugins or extensions

Overlay network facilitated relay attack[¶](#Overlay-network-facilitated-relay-attack)
--------------------------------------------------------------------------------------

### Intent[¶](#Intent)

Exploit webinos overlay network to commit fraud.

### Motivation[¶](#Motivation)

  Security Goal     Value    Description
  ----------------- -------- ---------------------------------------------------------------------------------------------
  Accountability    High     David relies on seamless convergence and a lack of traceability to carry out his attack.
  Confidentiality   Medium   David is interested in obtaining confidential information available to the webinos runtime.

### Structure[¶](#Structure)

  ---------------------------- -------------- ---------------------------------------------
  Attack: NFC replay attack    Origin: D2.8   Obstacle: Malicious personal zone enrolment
  Exploit: System data trust   Origin: D2.8   Obstacle: Spoof message origin
  ---------------------------- -------------- ---------------------------------------------

### Participants[¶](#Participants)

  Attacker   Motives      Capabilities (Value)
  ---------- ------------ --------------------------------------
  David      Data theft   Resources/Personnel and Time(Medium)

### Collaboration[¶](#Collaboration)

  --------- ---------------------------------
  Target    Device API, Privacy Preferences
  Exploit   Analytics Data, Device API
  --------- ---------------------------------

### Implementation[¶](#Implementation)

![](Overlay_network_facilitated_relay_attackObstacleModel.jpg)

As Alice was walking away from the bar with her drinks, she narrowly
avoided dropping one of her glasses as man brushed past her. "Sorry", he
mumbled as he walked briskly towards the toilets.

David devised a new scam which took advantage of the recent take-off of
NFC based mobile payment, and the new webinos platform that could link
different apps and devices together. The scam involved dropping a leech
mobile phone into someone's bag which contained a webinos enabled NFC
phone. The leech would attempt to get the victim's phone to join his
personal zone which, David estimated, would not be too difficult. Once
in place, David could then purchase things via NFC, while webinos routed
the request to the victim's NFC reader via the personal zone overlay
network. David tinkered around with different devices, settings, and
applications, and was quite surprised at how easy this scam appeared to
be. Consequently, he would need to make the most use of this exploit
quickly before other people got in on the act.

David's plan was to find somewhere where there would be lots of young
but unsuspecting people who might not notice something being put into
their bags. David decided a nightclub on a Friday night would be a good
bet. As David entered the club at shortly after midnight, he noticed a
large group of people mingling near the bar. As he approached, he
noticed a large women trying to carry multiple drinks with a hand-bag
slung around her shoulder. Confidently, with his leech device in hand,
David walked towards this woman.

### Obstacles[¶](#Obstacles)

  Obstacle                                 Category                Definition
  ---------------------------------------- ----------------------- --------------------------------------------------------------------------------------------------------
  Automate personal zone enrolment         Accountability Threat   A device is enroled into a personal zone without the use of an out-of-band channel.
  Disable valid personal zone proxy        Accountability Threat   A valid device personal zone proxy is disabled
  Malicious code evaluated                 Vulnerability           Event handler evaluates malicious JSON content.
  Malicious NDEF tag                       Integrity Threat        An NFC tag contains NDEF message encapsulating malicious code.
  Malicious personal zone enrolment        Accountability Threat   A device is enroled into a personal zone without the knowledge of the device owner.
  Overwrite valid authentication data      Integrity Threat        Overwrite valid authentication data.
  Overwrite valid PZP Configuration        Integrity Threat        Overwrite valid PZP Configuration file.
  Revoke device from valid personal zone   Accountability Threat   Revoke device from valid personal zone
  Run multiple personal zone proxies       Accountability Threat   Valid and malicious personal zone proxies run on a single device.
  Spoof message origin                     Integrity Threat        Messages sent from a source leech device to a destination device have the leeched device as an origin.
  Unauthorised NFC payment request         Accountability Threat   A request is received for an NFC payment from an unauthorised device.

Policy evasion through Browser APIs[¶](#Policy-evasion-through-Browser-APIs)
----------------------------------------------------------------------------

### Intent[¶](#Intent)

Jimmy creates a webinos application which collects location data for a
social application. Jimmy believes the app is much better if location
tracking is enabled and so uses every source of location data available.

### Motivation[¶](#Motivation)

  Security Goal     Value   Description
  ----------------- ------- ---------------------------------
  Unobservability   Low     Jimmy can observe user location

### Structure[¶](#Structure)

  ------------------------------------------------------------------ --------------- ----------------------------------
  Attack: Accessing Functionality Not Properly Constrained by ACLs   Origin: CAPEC   Obstacle: Browser API authorised
  Exploit: Missing Authorization                                     Origin: CWE     Obstacle: None
  ------------------------------------------------------------------ --------------- ----------------------------------

### Participants[¶](#Participants)

  Attacker   Motives   Capabilities (Value)
  ---------- --------- ---------------------------------------------
  Jimmy      Money     Knowledge/Methods(Medium), Software(Medium)

### Collaboration[¶](#Collaboration)

  --------- ---------------
  Target    Personal Data
  Exploit   Browser
  --------- ---------------

### Implementation[¶](#Implementation)

![](Policy_evasion_through_Browser_APIsObstacleModel.jpg)

Jimmy creates a legitimate and generally non-malicious web application
which the end user installs. However, Jimmy designs it so that it
accesses both webinos APIs and browser APIs, depending on what is
available at the time. When the user turns off access to geolocation
using webinos, Jimmy's app automatically invokes the browser API instead
which has already been authorised.

### Obstacles[¶](#Obstacles)

  -----------------------------------------------------------------------
  Obstacle                Category                Definition
  ----------------------- ----------------------- -----------------------
  App running in browser  Vulnerability           The application is
                                                  running in a browser

  Browser API authorised  Vulnerability           

  Browser Geolocation API Vulnerability           The application can
  accessed                                        access the
                                                  browser-supplied
                                                  geolocation API

  Geolocation accessed    Vulnerability           An application is able
  despite policy setting                          to access user
                                                  Geolocation details
                                                  despite policy settings
                                                  explicitly specifying
                                                  that this shouldn't be
                                                  possible.

  Policy misconfigured    Vulnerability           The user believes they
                                                  have disabled
                                                  geolocation when, in
                                                  fact, they haven't
  -----------------------------------------------------------------------

PZH Pharming[¶](#PZH-Pharming)
------------------------------

### Intent[¶](#Intent)

Ethan wants to steal user account details for personal zones in order to
create a botnet of webinos devices

### Motivation[¶](#Motivation)

  Security Goal     Value   Description
  ----------------- ------- ------------------------------------------------
  Confidentiality   High    Ethan intercepts confidential user credentials

### Structure[¶](#Structure)

  ------------------------------------------------------- --------------- ----------------------------------------------
  Attack: Pharming                                        Origin: CAPEC   Obstacle: PZH Admin page spoofed by attacker
  Exploit: UI Misrepresentation of Critical Information   Origin: CWE     Obstacle: User does not check PZH admin URL
  ------------------------------------------------------- --------------- ----------------------------------------------

### Participants[¶](#Participants)

  Attacker   Motives                 Capabilities (Value)
  ---------- ----------------------- -----------------------------------------------------------------
  Ethan      System resource theft   Knowledge/Methods(Medium), Software(Medium), Technology(Medium)

### Collaboration[¶](#Collaboration)

  --------- --------------------------------------
  Target    Identity Provider
  Exploit   Personal Zone Administration Console
  --------- --------------------------------------

### Implementation[¶](#Implementation)

![](PZH_PharmingObstacleModel.jpg)

Ethan creates a web application which offers a link to the user's PZH
administration console. This link actually directs them to a spoofed
version of their page, featuring a MITM attack on the credentials they
would enter into their identity provider's webpage.

### Obstacles[¶](#Obstacles)

  Obstacle                                     Category        Definition
  -------------------------------------------- --------------- ----------------------------------------------------------------------------------------------------------------------------------------------
  PZH Admin page spoofed by attacker           Vulnerability   The user's PZH admin page is impersonated by another webpage
  PZH Admin URL displayed without prominence   Vulnerability   The PZH admin URL bar is not visible or easy to miss
  PZH Admin URL not well known                 Vulnerability   The user does not know the correct URL
  PZH Admin URL too complicated                Vulnerability   The PZH admin URL is complicated and easy to misread
  PZH Credentials stolen                       Vulnerability   The user types their PZH administration page credentials into an attacker's webpage
  User clicks on link within application       Vulnerability   A malicious application offers a link to the user's PZH admin page, which is in fact directed to a malicious webpage hosted by the attacker.
  User does not check PZH admin URL            Vulnerability   The user does not check that the PZH admin page URL is what it should be

Steal In-Car Data[¶](#Steal-In-Car-Data)
----------------------------------------

### Intent[¶](#Intent)

Use an open webinos session for unauthorised transfer of data between
devices in different personal zones.

### Motivation[¶](#Motivation)

  Security Goal     Value    Description
  ----------------- -------- -----------------------------------------------------------------------------------------------------------------------------
  Accountability    High     The attacker can access user active session of the service. If it is a service with a fee, the attack can spend user money.
  Confidentiality   Medium   The attacker can access user session data.

### Structure[¶](#Structure)

  --------------------------- -------------- ---------------------------------------------
  Attack: Session hijacking   Origin: D2.8   Obstacle: None
  Exploit: Automatic login    Origin: D2.8   Obstacle: Malicious personal zone enrolment
  --------------------------- -------------- ---------------------------------------------

### Participants[¶](#Participants)

  Attacker   Motives      Capabilities (Value)
  ---------- ------------ --------------------------------------
  David      Data theft   Resources/Personnel and Time(Medium)

### Collaboration[¶](#Collaboration)

  --------- ---------------
  Target    Personal Data
  Exploit   Browser
  --------- ---------------

### Implementation[¶](#Implementation)

![](Steal_In-Car_DataObstacleModel.jpg)

Justin gives David, the mechanic, his car keys so David can carry out
his scheduled MOT.\
David at the moment has not other customers, so he decides to fiddle
with the in-car system.\
The computer requires no authentication so he can enter and nose about
navigation history. He realizes that the web browser is logged in a
music service with fee. He listens to the music waiting for the next
motorist coming.\
After listening few songs, he uses his own webinos enabled smartphone to
get the Justin's personal zone device list via Justin's PZH. From the
list he selects the in-car system. When on the in-car system touch
screen appears the confirmation dialog box, he taps on OK and the
devices are now connected. David can exit from the car and access
Justin's music service form his own smartphone.\
When Justin comes back to the parking, David disconnects the smartphone
form the music service and from Justin's personal zone and returns the
car to its owner.

### Obstacles[¶](#Obstacles)

  Obstacle                                 Category                Definition
  ---------------------------------------- ----------------------- --------------------------------------------------------------------------------------------------------
  Automate personal zone enrolment         Accountability Threat   A device is enroled into a personal zone without the use of an out-of-band channel.
  Disable valid personal zone proxy        Accountability Threat   A valid device personal zone proxy is disabled
  Malicious code evaluated                 Vulnerability           Event handler evaluates malicious JSON content.
  Malicious NDEF tag                       Integrity Threat        An NFC tag contains NDEF message encapsulating malicious code.
  Malicious personal zone enrolment        Accountability Threat   A device is enroled into a personal zone without the knowledge of the device owner.
  Overwrite valid authentication data      Integrity Threat        Overwrite valid authentication data.
  Overwrite valid PZP Configuration        Integrity Threat        Overwrite valid PZP Configuration file.
  Revoke device from valid personal zone   Accountability Threat   Revoke device from valid personal zone
  Run multiple personal zone proxies       Accountability Threat   Valid and malicious personal zone proxies run on a single device.
  Spoof message origin                     Integrity Threat        Messages sent from a source leech device to a destination device have the leeched device as an origin.
  Unauthorised NFC payment request         Accountability Threat   A request is received for an NFC payment from an unauthorised device.

Steal webinos Session[¶](#Steal-webinos-Session)
------------------------------------------------

### Intent[¶](#Intent)

Exploit open sessions to steal personal data for financial gain

### Motivation[¶](#Motivation)

  Security Goal     Value    Description
  ----------------- -------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Anonymity         Low      The malicious request associated with the CSRF may involve harvesting small amounts of data which, collectively, could lead to the disclosure of a subject's identity.
  Confidentiality   Medium   The attack allows the malicious code access to session data, some of which may be long-lived.

### Structure[¶](#Structure)

  ------------------------------------ --------------- ------------------------------------
  Attack: Cross-Site Request Forgery   Origin: OWASP   Obstacle: None
  Exploit: Session Fixation            Origin: OWASP   Obstacle: Malicious code evaluated
  ------------------------------------ --------------- ------------------------------------

### Participants[¶](#Participants)

  Attacker   Motives                 Capabilities (Value)
  ---------- ----------------------- -----------------------------------------------------------------
  Ethan      System resource theft   Knowledge/Methods(Medium), Software(Medium), Technology(Medium)

### Collaboration[¶](#Collaboration)

  --------- ---------------
  Target    Personal Data
  Exploit   Session
  --------- ---------------

### Implementation[¶](#Implementation)

![](Steal_webinos_SessionObstacleModel.jpg)

As a new source of income, Ethan has opened an account with an affiliate
stock photo service. Ethan carries out some rudimentary google hacking
to identify forums that might be open to stored XSS vulnerabilities.
Eventually, Ethan finds a forum that is used by a Webinos enabled camera
app that synchronises images with a cloud based photo sharing service.

Ethan develops an XSS/CSRF exploit by loading malicious code into the
application's blog page. On viewing the blog, the script obtains the
Webinos session data and, via some local and external javascript and
php, sends the session data to another site which uses the Webinos APIs,
close a device's session, re-opens the session to the device, obtains
the images, and submits these to the affiliate stock photo service using
the service providers web services API. Ethan realises the exploit might
only work on certain devices, but he thinks that something is better
than nothing...

Several days later, Justin is taking some snaps of some his friends at a
bar using a recently downloaded camera application that syncs his images
to the cloud based provider. On his way home, Justin browses the
community developed help data in the application. Justin doesn't realise
that, by checking this help data, his photos are about to net Ethan some
additional income.

### Obstacles[¶](#Obstacles)

  Obstacle                                 Category                Definition
  ---------------------------------------- ----------------------- --------------------------------------------------------------------------------------------------------
  Automate personal zone enrolment         Accountability Threat   A device is enroled into a personal zone without the use of an out-of-band channel.
  Disable valid personal zone proxy        Accountability Threat   A valid device personal zone proxy is disabled
  Malicious code evaluated                 Vulnerability           Event handler evaluates malicious JSON content.
  Malicious NDEF tag                       Integrity Threat        An NFC tag contains NDEF message encapsulating malicious code.
  Malicious personal zone enrolment        Accountability Threat   A device is enroled into a personal zone without the knowledge of the device owner.
  Overwrite valid authentication data      Integrity Threat        Overwrite valid authentication data.
  Overwrite valid PZP Configuration        Integrity Threat        Overwrite valid PZP Configuration file.
  Revoke device from valid personal zone   Accountability Threat   Revoke device from valid personal zone
  Run multiple personal zone proxies       Accountability Threat   Valid and malicious personal zone proxies run on a single device.
  Spoof message origin                     Integrity Threat        Messages sent from a source leech device to a destination device have the leeched device as an origin.
  Unauthorised NFC payment request         Accountability Threat   A request is received for an NFC payment from an unauthorised device.

Test footprinting[¶](#Test-footprinting)
----------------------------------------

### Intent[¶](#Intent)

### Motivation[¶](#Motivation)

  Security Goal    Value   Description
  ---------------- ------- -----------------------------------------------------------------------
  Accountability   High    Ethan looks for test code which provides unauthorised resource access

### Structure[¶](#Structure)

  --------------------------------------------------------------- --------------- ----------------------------------------------
  Attack: Locate and Exploit Test APIs                            Origin: CAPEC   Obstacle: Test API enabled
  Exploit: Allocation of Resources without Limits or Throttling   Origin: CWE     Obstacle: Unrestricted request specification
  --------------------------------------------------------------- --------------- ----------------------------------------------

### Participants[¶](#Participants)

  Attacker   Motives                 Capabilities (Value)
  ---------- ----------------------- -----------------------------------------------------------------
  Ethan      System resource theft   Knowledge/Methods(Medium), Software(Medium), Technology(Medium)

### Collaboration[¶](#Collaboration)

  --------- ------------------
  Target    Application Data
  Exploit   Access Request
  --------- ------------------

### Implementation[¶](#Implementation)

![](Test_footprintingObstacleModel.jpg)

Ethan finds apps with superflous test code which allows him to exploit
test data in runtime.

### Obstacles[¶](#Obstacles)

  Obstacle                             Category        Definition
  ------------------------------------ --------------- -----------------------------------------------------------------------------
  Ambiguous request specification      Vulnerability   Request specification is ambiguous.
  Ambiguous resource spec              Vulnerability   Resource specification is ambiguous
  Anonymous data usage                 Vulnerability   Users do not specify how they will use data they are requesting.
  Misspecified resource                Vulnerability   Resource is misspecified.
  Misspecified usage request           Vulnerability   Usage request is misspecified.
  Non-mandated request                 Vulnerability   Request is non-mandated.
  Overrestricted resource              Vulnerability   Resource is overly restricted compared to its specification.
  Superfluous installation data        Vulnerability   webinos application installation contains superfluous data and code.
  Test API enabled                     Vulnerability   Test API is enabled in operating environment.
  Test configuration enabled           Vulnerability   Test and sample configuration data is enabled in the operating environment.
  Unrestricted request specification   Vulnerability   User agent grants access to all network resources.
  Unrestricted resource                Vulnerability   Resource contains no restrictions.
  Unspecified resource                 Vulnerability   Resource is unspecified.

Exploiting transitive permissions[¶](#Exploiting-transitive-permissions)
------------------------------------------------------------------------

### Intent[¶](#Intent)

Frankie wants to spy on people through a web application, as he thinks
it might be fun and might be able to catch people in embarassing
situations

### Motivation[¶](#Motivation)

  Security Goal     Value    Description
  ----------------- -------- -------------------------------------------------------------------------
  Confidentiality   Medium   Frankie can access personal data normally protected by webinos policies

### Structure[¶](#Structure)

  ----------------------------------------------- --------------- ---------------------------------------------------------
  Attack: Data Interception Attacks               Origin: CAPEC   Obstacle: Installed App exposes communication interface
  Exploit: Improper Preservation of Permissions   Origin: CWE     Obstacle: Installed App given API permissions
  ----------------------------------------------- --------------- ---------------------------------------------------------

### Participants[¶](#Participants)

  Attacker   Motives          Capabilities (Value)
  ---------- ---------------- ---------------------------------------------
  Frankie    Thrill-seeking   Knowledge/Methods(Medium), Software(Medium)

### Collaboration[¶](#Collaboration)

  --------- ---------------
  Target    Personal Data
  Exploit   Device API
  --------- ---------------

### Implementation[¶](#Implementation)

![](Exploiting_transitive_permissionsObstacleModel.jpg)

Frankie creates an application which appears to be legitimate and only
requests minimal permissions. Even if untrusted, many users are likely
to install it and trust the webinos security framework to protect it
once it has been uploaded to an app store. However, the application
makes use of an unprotected communication interface with another
application (which has access to many APIs) to read user data. Frankie
makes sure that his app uploads this data to is servers...

### Obstacles[¶](#Obstacles)

  Obstacle                                                    Category        Definition
  ----------------------------------------------------------- --------------- --------------------------------------------------------------------------------------------------------------------------------------------------
  Installed App allows unrestricted postMessage               Vulnerability   The trusted application is part hosted and allows arbitrary postMessages from other origins
  Installed App allows unrestricted XHR                       Vulnerability   The trusted application is part hosted and allows arbitrary XHR from other origins
  Installed App exposes communication interface               Vulnerability   A trusted app exposes communication interface to other applications
  Installed App given API permissions                         Vulnerability   A trusted app is installed and given permission to access several APIs with access to personal data
  Installed App uses unauthenticated webinos event messages   Vulnerability   The trusted application will receive and process event messages from other apps without verifying the authenticity of the other applications
  Installed App vulnerable to content injection               Vulnerability   The trusted application is part hosted and vulnerable to a content injection attack, allowing another site to abuse the permissions of that site
  Malicious App misuses communication interface               Vulnerability   A malicious application is able to communicate arbitrarily with a trusted application
  Unauthorised API access by application                      Vulnerability   A webinos application is able to access an API despite restrictions imposed by the policy system through calling another, trusted application

Linkability through findServices[¶](#Linkability-through-findServices)
----------------------------------------------------------------------

### Intent[¶](#Intent)

Jimmy wants to be able to re-identify users of different applications in
order to sell data to analytics and marketing companies who run
advertising networks. If he can collect data about users on applications
this can be used to better target adverts.

### Motivation[¶](#Motivation)

  Security Goal   Value   Description
  --------------- ------- --------------------------------------------------------------
  Unlinkability   Low     Jimmy can connect actions of users of different applications

### Structure[¶](#Structure)

  ---------------------------------------------------------- --------------- ---------------------------------
  Attack: Cross Site Identification                          Origin: CAPEC   Obstacle: None
  Exploit: Information Exposure Through Persistent Cookies   Origin: CWE     Obstacle: Apps share usage data
  ---------------------------------------------------------- --------------- ---------------------------------

### Participants[¶](#Participants)

  Attacker   Motives   Capabilities (Value)
  ---------- --------- ---------------------------------------------
  Jimmy      Money     Knowledge/Methods(Medium), Software(Medium)

### Collaboration[¶](#Collaboration)

  --------- ---------------
  Target    Personal Data
  Exploit   Device API
  --------- ---------------

### Implementation[¶](#Implementation)

![](Linkability_through_findServicesObstacleModel.jpg)

Jimmy creates a legitimate application which uses various unimportant
APIs, inluding the discovery API. Through the discovery API he is able
to retrieve identifiers for webinos services hosted in the user's
personal zone. These are persistent. Jimmy combines these identifies
with records about the user's activity on the application and sells them
to an online analytics firm who combines this information with other
instances of these service identifiers.

### Obstacles[¶](#Obstacles)

  Obstacle                                             Category        Definition
  ---------------------------------------------------- --------------- ------------------------------------------------------------------------------------------------------------------------------------------------------
  Application has user identifier without permission   Vulnerability   One application is installed and is able to obtain a user identifier without requesting access to an API for this.
  Apps share usage data                                Vulnerability   The two application share usage data, either directly or through an intermediary analytics service
  findService API reveals permanent user identifier    Vulnerability   The output of the findServices API is an effective user identifier.
  Independent apps have common identifier for user     Vulnerability   Two or more independent applications have been installed in the personal zone and have the same user identifier.
  User identity tracked between applications           Vulnerability   An application is able to successfully re-identify a user of a different application despite them restricting access to personally-identifying APIs.

Identity theft with webinos messaging[¶](#Identity-theft-with-webinos-messaging)
--------------------------------------------------------------------------------

### Intent[¶](#Intent)

Ethan attempts to steal usernames and passwords of webinos users in
order to then phish their friends by sending them scam emails.

### Motivation[¶](#Motivation)

  Security Goal     Value    Description
  ----------------- -------- -------------------------------
  Confidentiality   Medium   The loss of email credentials

### Structure[¶](#Structure)

  ----------------------------------------------- --------------- ---------------------------------------
  Attack: Mobile Phishing (aka MobPhishing)       Origin: CAPEC   Obstacle: SMS intercepted and relayed
  Exploit: Insufficiently Protected Credentials   Origin: CWE     Obstacle: None
  ----------------------------------------------- --------------- ---------------------------------------

### Participants[¶](#Participants)

  Attacker   Motives                 Capabilities (Value)
  ---------- ----------------------- -----------------------------------------------------------------
  Ethan      System resource theft   Knowledge/Methods(Medium), Software(Medium), Technology(Medium)

### Collaboration[¶](#Collaboration)

  --------- ------------------
  Target    Application Data
  Exploit   Access Request
  --------- ------------------

### Implementation[¶](#Implementation)

![](Identity_theft_with_webinos_messagingObstacleModel.jpg)

Ethan obtains user account details and uses malware to defeat 2-factor
authentication

### Obstacles[¶](#Obstacles)

  Obstacle                                                          Category        Definition
  ----------------------------------------------------------------- --------------- -----------------------------------------------------------------------------------------------------------------------------------------------------------------
  Attacker obtains user password                                    Vulnerability   The attacker gains the user's login password. This may be through the password recovery system, compromise of a re-used password on another site, or otherwise.
  Bad trust decisions                                               Vulnerability   The user makes a bad decision to trust a piece of malware. This could be because they have insufficent information available to make a better decision.
  Malware granted permission to access messaging API                Vulnerability   The user grants a piece of malware inappropriately high permissions
  Malware installed                                                 Vulnerability   A piece of malicious software is installed by the end user
  Messaging API misused                                             Vulnerability   Malware is given access to the messaging API which is then used to send messages and receive presumed-private messages
  Online email account details compromised                          Vulnerability   The attacker gains knowledge of the user's account details which are sufficient for him to log-in and impersonate them
  Permission prompt click-through                                   Vulnerability   Users click 'ok' to all permission prompts and therefore do not realise they are granting inappropriate permission
  Second factor of authentication (SMS or email code) compromised   Vulnerability   The attacker gains credentials provided by the second authentication factor (an SMS containing a short token, for example)
  SMS intercepted and relayed                                       Vulnerability   SMS messages are intercepted by malware with a subscription to the messaging API. The authentication token is then forwarded to the attacker
  Webinos account is misused to phish contact                       Vulnerability   An attacker uses their ability to log in to the user's email account to impersonate them and send phishing emails to their contacts.

Request footprinting[¶](#Request-footprinting)
----------------------------------------------

### Intent[¶](#Intent)

Glean an understanding of what resources are available on a device by
eavesdropping on requests.

### Motivation[¶](#Motivation)

  Security Goal     Value   Description
  ----------------- ------- ---------------------------------------------------------------------------------------
  Confidentiality   Low     Ethan wants to get a better understanding of what resources are under policy control.

### Structure[¶](#Structure)

  --------------------------------- --------------- -------------------------------------------------
  Attack: Network Eavesdropping     Origin: OWASP   Obstacle: Eavesdrop request enforcement channel
  Exploit: Missing XML Validation   Origin: OASIS   Obstacle: Missing XML document validation
  --------------------------------- --------------- -------------------------------------------------

### Participants[¶](#Participants)

  Attacker   Motives                 Capabilities (Value)
  ---------- ----------------------- -----------------------------------------------------------------
  Ethan      System resource theft   Knowledge/Methods(Medium), Software(Medium), Technology(Medium)

### Collaboration[¶](#Collaboration)

  --------- ------------------
  Target    Application Data
  Exploit   Application Data
  --------- ------------------

### Implementation[¶](#Implementation)

![](Request_footprintingObstacleModel.jpg)

Ethan eavesdrop on traffic to and from the policy manager to find
possible policy management vulnerabilities.

### Obstacles[¶](#Obstacles)

  Obstacle                                Category                 Definition
  --------------------------------------- ------------------------ -----------------------------------------------------------
  Eavesdrop access requests               Confidentiality Threat   Eavesdrop access requests
  Eavesdrop Context Database              Confidentiality Threat   Eavesdrop use of policy management in Context Database
  Eavesdrop Context Manager               Confidentiality Threat   Eavesdrop use of policy management in context manager
  Eavesdrop Policy Manager                Confidentiality Threat   Eavesdrop software making use of the Policy Manager
  Eavesdrop request enforcement channel   Confidentiality Threat   Eavesdrop access request enforcement channel.
  Eavesdrop RPC Call Log                  Confidentiality Threat   Eavesdrop logged use of policy management in RPC call log


