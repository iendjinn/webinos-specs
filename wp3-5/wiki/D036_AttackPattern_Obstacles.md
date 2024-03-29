Attack Pattern Obstacles[¶](#Attack-Pattern-Obstacles)
======================================================

Application DoS[¶](#Application-DoS)
------------------------------------

### Obstacles[¶](#Obstacles)

  ---------------------------------------------------------- --------------- -----------------------------------------------------------------------------------------------------------------------------------------------------
  Obstacle                                                   Category        Definition
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
  ---------------------------------------------------------- --------------- -----------------------------------------------------------------------------------------------------------------------------------------------------

Capture Hidden Analytics[¶](#Capture-Hidden-Analytics)
------------------------------------------------------

### Obstacles[¶](#Obstacles)

  ---------- ---------- ------------
  Obstacle   Category   Definition
  ---------- ---------- ------------

Control cloud-based PZH[¶](#Control-cloud-based-PZH)
----------------------------------------------------

### Obstacles[¶](#Obstacles)

  ---------- ---------- ------------
  Obstacle   Category   Definition
  ---------- ---------- ------------

Device availability loss[¶](#Device-availability-loss)
------------------------------------------------------

### Obstacles[¶](#Obstacles)

  -------------------------------------------- --------------- ----------------------------------------------------------------------------------------------------------
  Obstacle                                     Category        Definition
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
  -------------------------------------------- --------------- ----------------------------------------------------------------------------------------------------------

Loss of personal zone administration access[¶](#Loss-of-personal-zone-administration-access)
--------------------------------------------------------------------------------------------

### Obstacles[¶](#Obstacles)

  ------------------------------------ --------------- -----------------------------------------------------------------------------------------
  Obstacle                             Category        Definition
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
  ------------------------------------ --------------- -----------------------------------------------------------------------------------------

Exploit network bandwidth[¶](#Exploit-network-bandwidth)
--------------------------------------------------------

### Obstacles[¶](#Obstacles)

  --------------------------------------- ----------------------- ----------------------------------------------------------
  Obstacle                                Category                Definition
  Post spoofed message                    Accountability Threat   Post spoofed message
  Spoof network settings message          Accountability Threat   Spoof network settings message sent to network provider.
  Spoof network settings message origin   Integrity Threat        Spoof network settings message origin.
  --------------------------------------- ----------------------- ----------------------------------------------------------

Man In The webinos Browser[¶](#Man-In-The-webinos-Browser)
----------------------------------------------------------

### Obstacles[¶](#Obstacles)

  ------------------------------------- --------------- ----------------------------------------------------------------------------------
  Obstacle                              Category        Definition
  Application data intercepted          Vulnerability   Application data from webinos widgets is intercepted in the widget renderer
  Application data readable             Vulnerability   Application data from webinos widgets is readable outside of the widget renderer
  Malicious plugin installed            Vulnerability   The user installs (or suffers from a driveby download) a malicious plugin
  Malicious plugin is running           Vulnerability   Malware in the form of a malicious widget renderer plugin is running
  Malicious plugin not detected         Vulnerability   Malware plugin not detected.
  Widget renderer supports extensions   Vulnerability   The widget renderer supports plugins or extensions
  ------------------------------------- --------------- ----------------------------------------------------------------------------------

Overlay network facilitated relay attack[¶](#Overlay-network-facilitated-relay-attack)
--------------------------------------------------------------------------------------

### Obstacles[¶](#Obstacles)

  ---------------------------------------- ----------------------- --------------------------------------------------------------------------------------------------------
  Obstacle                                 Category                Definition
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
  ---------------------------------------- ----------------------- --------------------------------------------------------------------------------------------------------

Policy evasion through Browser APIs[¶](#Policy-evasion-through-Browser-APIs)
----------------------------------------------------------------------------

### Obstacles[¶](#Obstacles)

  ----------------------- ----------------------- -----------------------
  Obstacle                Category                Definition

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
  ----------------------- ----------------------- -----------------------

PZH Pharming[¶](#PZH-Pharming)
------------------------------

### Obstacles[¶](#Obstacles)

  -------------------------------------------- --------------- ----------------------------------------------------------------------------------------------------------------------------------------------
  Obstacle                                     Category        Definition
  PZH Admin page spoofed by attacker           Vulnerability   The user's PZH admin page is impersonated by another webpage
  PZH Admin URL displayed without prominence   Vulnerability   The PZH admin URL bar is not visible or easy to miss
  PZH Admin URL not well known                 Vulnerability   The user does not know the correct URL
  PZH Admin URL too complicated                Vulnerability   The PZH admin URL is complicated and easy to misread
  PZH Credentials stolen                       Vulnerability   The user types their PZH administration page credentials into an attacker's webpage
  User clicks on link within application       Vulnerability   A malicious application offers a link to the user's PZH admin page, which is in fact directed to a malicious webpage hosted by the attacker.
  User does not check PZH admin URL            Vulnerability   The user does not check that the PZH admin page URL is what it should be
  -------------------------------------------- --------------- ----------------------------------------------------------------------------------------------------------------------------------------------

Steal In-Car Data[¶](#Steal-In-Car-Data)
----------------------------------------

### Obstacles[¶](#Obstacles)

  ---------------------------------------- ----------------------- --------------------------------------------------------------------------------------------------------
  Obstacle                                 Category                Definition
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
  ---------------------------------------- ----------------------- --------------------------------------------------------------------------------------------------------

Steal webinos Session[¶](#Steal-webinos-Session)
------------------------------------------------

### Obstacles[¶](#Obstacles)

  ---------------------------------------- ----------------------- --------------------------------------------------------------------------------------------------------
  Obstacle                                 Category                Definition
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
  ---------------------------------------- ----------------------- --------------------------------------------------------------------------------------------------------

Test footprinting[¶](#Test-footprinting)
----------------------------------------

### Obstacles[¶](#Obstacles)

  ---------- ---------- ------------
  Obstacle   Category   Definition
  ---------- ---------- ------------

Exploiting transitive permissions[¶](#Exploiting-transitive-permissions)
------------------------------------------------------------------------

### Obstacles[¶](#Obstacles)

  --------------------------------------------------------- --------------- --------------------------------------------------------------------------------------------------------------------------------------------------
  Obstacle                                                  Category        Definition
  Malicious App misuses communication interface             Vulnerability   A malicious application is able to communicate arbitrarily with a trusted application
  Trusted App allows unrestricted postMessage               Vulnerability   The trusted application is part hosted and allows arbitrary postMessages from other origins
  Trusted App allows unrestricted XHR                       Vulnerability   The trusted application is part hosted and allows arbitrary XHR from other origins
  Trusted App exposes communication interface               Vulnerability   A trusted app exposes communication interface to other applications
  Trusted App given API permissions                         Vulnerability   A trusted app is installed and given permission to access several APIs with access to personal data
  Trusted App uses unauthenticated webinos event messages   Vulnerability   The trusted application will receive and process event messages from other apps without verifying the authenticity of the other applications
  Trusted App vulnerable to content injection               Vulnerability   The trusted application is part hosted and vulnerable to a content injection attack, allowing another site to abuse the permissions of that site
  Unauthorised API access by application                    Vulnerability   A webinos application is able to access an API despite restrictions imposed by the policy system through calling another, trusted application
  --------------------------------------------------------- --------------- --------------------------------------------------------------------------------------------------------------------------------------------------

Linkability through findServices[¶](#Linkability-through-findServices)
----------------------------------------------------------------------

### Obstacles[¶](#Obstacles)

  ------------------------------------------------------- --------------- ------------------------------------------------------------------------------------------------------------------------------------------------------
  Obstacle                                                Category        Definition
  App 1 installed with access to findServices for API A   Vulnerability   One application is installed and is granted access to findServices for an API
  App 2 installed with access to findServices for API A   Vulnerability   A second application is installed and is granted access to findServices for an API
  Apps share usage data                                   Vulnerability   The two application share usage data, either directly or through an intermediary analytics service
  Multiple apps installed                                 Vulnerability   Two or more independent applications have been installed in the personal zone.
  User identity tracked between applications              Vulnerability   An application is able to successfully re-identify a user of a different application despite them restricting access to personally-identifying APIs.
  ------------------------------------------------------- --------------- ------------------------------------------------------------------------------------------------------------------------------------------------------

Identity theft with webinos messaging[¶](#Identity-theft-with-webinos-messaging)
--------------------------------------------------------------------------------

### Obstacles[¶](#Obstacles)

  ----------------------------------------------------------------- --------------- -----------------------------------------------------------------------------------------------------------------------------------------------------------------
  Obstacle                                                          Category        Definition
  Attacker obtains user password                                    Vulnerability   The attacker gains the user's login password. This may be through the password recovery system, compromise of a re-used password on another site, or otherwise.
  Bad trust decisions                                               Vulnerability   The user makes a bad decision to trust a piece of malware. This could be because they have insufficent information available to make a better decision.
  Malware granted permission to access messsaging API               Vulnerability   The user grants a piece of malware inappropriately high permissions
  Malware installed                                                 Vulnerability   A piece of malicious software is installed by the end user
  Messaging API misused                                             Vulnerability   Malware is given access to the messaging API which is then used to send messages and receive presumed-private messages
  Online email account details compromised                          Vulnerability   The attacker gains knowledge of the user's account details which are sufficient for him to log-in and impersonate them
  Permission prompt click-through                                   Vulnerability   Users click 'ok' to all permission prompts and therefore do not realise they are granting inappropriate permission
  Second factor of authentication (SMS or email code) compromised   Vulnerability   The attacker gains credentials provided by the second authentication factor (an SMS containing a short token, for example)
  SMS intercepted and relayed                                       Vulnerability   SMS messages are intercepted by malware with a subscription to the messaging API. The authentication token is then forwarded to the attacker
  Webinos account is misused to phish contact                       Vulnerability   An attacker uses their ability to log in to the user's email account to impersonate them and send phishing emails to their contacts.
  ----------------------------------------------------------------- --------------- -----------------------------------------------------------------------------------------------------------------------------------------------------------------

Request footprinting[¶](#Request-footprinting)
----------------------------------------------

### Obstacles[¶](#Obstacles)

  --------------------------------------- ------------------------ -----------------------------------------------------------
  Obstacle                                Category                 Definition
  Eavesdrop access requests               Confidentiality Threat   Eavesdrop access requests
  Eavesdrop Context Database              Confidentiality Threat   Eavesdrop use of policy management in Context Database
  Eavesdrop Context Manager               Confidentiality Threat   Eavesdrop use of policy management in context manager
  Eavesdrop Policy Manager                Confidentiality Threat   Eavesdrop software making use of the Policy Manager
  Eavesdrop request enforcement channel   Confidentiality Threat   Eavesdrop access request enforcement channel.
  Eavesdrop RPC Call Log                  Confidentiality Threat   Eavesdrop logged use of policy management in RPC call log
  --------------------------------------- ------------------------ -----------------------------------------------------------


