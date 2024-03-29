New proposed Webinos APIs[¶](#New-proposed-Webinos-APIs)
========================================================

Add APIs that are proposed to be included in task 3.4, phase 2 of
webinos API specifications. State high level requirements on the
proposed API and consider if there are existing APIs that fulfill what
we need.

Actuator API[¶](#Actuator-API)
------------------------------

**Description:**\
**Rationale (requirement, architectural reference,etc):** See [Actuator
API scenarios and use cases](.html)\
**Responsible:** Andre Paul / Fraunhofer\
**Notes:** An Actuator API draft has already been created by Louay
Bassbouss from Fraunhofer. Widl is here:
</t3-2/repository/revisions/b94e99c812f79b514248532db53192843cec1a0e/entry/sources/widl/actuators.widl>

**Following table includes some potential actuator types to be supported
by the API. Considering smart home scenarios switch and thermostat are
probably the most important ones.**

  ----------------------------------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **High level Requirements**                                 **Notes**
  Provide high level API for switching states of actuators.   In contrast to the sensor API the actuator API should allow to influence the state of a device instead of just reading out sensor information. For each actuator implementation there should be a sensor implementation for also reading values/the current state
  Progress updates                                            Because changing the state of an actuator can take some time the API should provide the possibility to receive updates while changing the state of an actuator.
  Generic API                                                 Like the Sensor API the Actuator API should be generic in order to support future extensions with additional actuator types
  Possible Actuator: Switch                                   A switch commonly only has one input which represents the state of the switch such as ON/OFF, TRUE/FALSE, 0/1 etc.
  Possible Actuator: Thermostat                               Setting a target temperature, having min and max values.
  Possible Actuator: Linear motor                             Setting speed and direction of the linear motor
  Possible Actuator: Vibrating motor                          Setting the intensity of the vibration motor
  Possible Actuator: Rotational motor                         Setting the speed and direction of a rotational motor (e.g., in Hz (cylces per second)
  Possible Actuator: Servo motor                              Setting the desired angle of the servo motor
  Possible Actuator: Swivel motor                             Setting three dimensions for a swivel and getting min max values
  ----------------------------------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

(note that the following table is only filled in if there already exist
one or more APIs that are candidates for use by webinos)

  -------------- -------------- -------------- -------------- --------------
  **Candidate    **Short        **Implementati **Gaps**       **Notes**
  existing API** Description**  on                            
                                Status**                      

                                                              
  -------------- -------------- -------------- -------------- --------------

**Decision:**

Bluetooth API[¶](#Bluetooth-API)
--------------------------------

**Description:**\
**Rationale (requirement, architectural reference,etc):**\
**Responsible:** Ziran Sun/Samsung\
**Notes:** Based on Pulse meter demo? Note that W3C Device API WG has
started to discuss use cases for a Bluetooth API,
<http://lists.w3.org/Archives/Public/public-device-apis/2012Apr/0030.html>.

  ------------------------------------ ------------------------------------
  **High level Requirements**          **Notes**
                                       
                                       
  ------------------------------------ ------------------------------------

  --------------------------------------- ----------------------------------------------------------------------------- --------------------------- ----------------------------------------------------------- -----------------------
  **Candidate existing API**              **Short Description**                                                         **Implementation Status**   **Gaps**                                                    **Notes**
  BTfindservice(serviceType, callback)    To find Bluetooth devices that support specified service type                 Linux                       Split into scan, pairing devices APIs                       webinos Implemenation
  BTbindservice(service, callback)        To connect with the found Bluetooth device and see all visible file folders   Linux                       OPP profile implementation - need to make the API clearer   webinos Implemenation
  BTlistfile(folder, callback)            To list available files/folders in the connected Bluetooth device             Linux                       OPP profile implementation - need to make the API clearer   webinos Implemenation
  BTtransferfile(filename, callback)      To get specific file from the Bluetooth device                                Linux                       OPP profile implementation - need to make the API clearer   webinos Implemenation
  HRMfindservice(serviceType, callback)   To connect to a HRM and fetch heart beat data                                 Android                     SPP profile implementation - need to make the API clearer   webinos Implemenation
  --------------------------------------- ----------------------------------------------------------------------------- --------------------------- ----------------------------------------------------------- -----------------------

**Decision:** Current approach (May 3rd 2012) is that a low level
Bluetooth API will not be specified by Webinos. Instead new sensor types
for which we have use cases will be added to the Webinos Sensor API. It
is the implementation of the Sensor API that accesses the different
sensors using the relevant low level protocols, e.g. Bluetooth.

Media Capture and Streams (aka getUserMedia API)[¶](#Media-Capture-and-Streams-aka-getUserMedia-API)
----------------------------------------------------------------------------------------------------

**Description:** Getting access to local devices that can generate
multimedia streams\
**Rationale (requirement, architectural reference,etc):** See
[getUserMedia API/PeerConnection API scenarios and use cases](.html)\
**Responsible:** Anders Isberg / Sony Mobile and Martin Lasak /
Fraunhofer\
**Notes:**

  ------------------------------------ ------------------------------------
  **High level Requirements**          **Notes**
                                       
                                       
  ------------------------------------ ------------------------------------

  -------------- -------------- -------------- -------------- --------------
  **Candidate    **Short        **Implementati **Gaps**       **Notes**
  existing API** Description**  on                            
                                Status**                      

  [W3C           Access to the  As of 26th,    Comments by    
  getusermedia]( LocalMediaStre April          Nick Allott:\  
  http://dev.w3. am             available      a) We need to  
  org/2011/webrt object by      browser        be able to     
  c/editor/getus calling the    implementation remotely       
  ermedia.html)  getUserMedia   s              invoke\        
                 API, this      exists for     b) It needs to 
                 object may be  Google Chrome  be calleable   
                 then consumed  (Canary,       from service   
                 by the         20.0.1117.0)   context – not  
                 video/audio    navigator.webk just browser   
                 tag or used by itGetUserMedia context (ie    
                 the            ,              form pzp)\     
                 PeerConnection Opera (Labs,   c) The design  
                 API to be      12.00 alpha)   is created to  
                 consumed       navigator.getU be used from   
                 remotely.      serMedia       browser        
                                               security       
                                               context . We   
                                               need to dilute 
                                               the UI         
                                               requirements   
                                               on             
                                               notification   
                                               from native or 
                                               service        
                                               context use\   
                                               d) Are there   
                                               any issues     
                                               with cross     
                                               device content 
                                               stream         
                                               compatibility  
                                               /negotiation   
                                               –that aren’t   
                                               covered\       
                                               e) Is there a  
                                               use case for   
                                               accessing the  
                                               binary data    
                                               stream direct? 
                                               Can this be    
                                               done out of    
                                               the box?       
  -------------- -------------- -------------- -------------- --------------

**Decision:**

PeerConnection API[¶](#PeerConnection-API)
------------------------------------------

**Description:** A PeerConnection allows two users to communicate
directly, browser-to-browser. Communications are coordinated via a
signaling channel provided by script in the page via the server, e.g.
using XMLHttpRequest (or WebSockets)\
**Rationale (requirement, architectural reference,etc): *Assume same
scenarios and use cases as for getUserMedia API*\
\*Responsible:** Anders Isberg / Sony Mobile and Martin Lasak /
Fraunhofer\
**Notes:** Needed to remotely access media streams.

  ------------------------------------ ------------------------------------
  **High level Requirements**          **Notes**
                                       
                                       
  ------------------------------------ ------------------------------------

  -------------- -------------- -------------- -------------- --------------
  **Candidate    **Short        **Implementati **Gaps**       **Notes**
  existing API** Description**  on                            
                                Status**                      

  [W3C WebRTC    A set of APIs  As of June 5                  Comments
  1.0: Real-time to represent   this API is                   Anders Isberg:
  Communication  streaming      supported by                  Should webinos
  Between        media,         at least                      provide server
  Browsers](http including      Chrome 19                     support for
  ://www.w3.org/ audio and                                    the signalling
  TR/webrtc/)    video, in                                    path. In
                 JavaScript, to                               addition, to
                 allow media to                               be able to do
                 be sent over                                 NAT traversal
                 the network to                               STUN server
                 another                                      must be
                 browser or                                   included in
                 device                                       the
                 implementing                                 architecture.
                 the                                          
                 appropriate                                  
                 set of                                       
                 real-time                                    
                 protocols, and                               
                 media received                               
                 from another                                 
                 browser or                                   
                 device to be                                 
                 processed and                                
                 displayed                                    
                 locally.                                     
  -------------- -------------- -------------- -------------- --------------

**Decision:**

oAuth API[¶](#oAuth-API)
------------------------

**Description:** provides server-side authentication, in order to allow
using third-party external services.\
**Rationale (requirement, architectural reference,etc):** Fulfill
missing functionality. Issue brought up while developing applications on
the top of webinos framework. See [oAuth API scenarios and use
cases](/wp2-4/wiki/Proposed_Update_OAuth_support)\
**Responsible:** Paolo Vergori / ISMB\
**Notes:** based on the undocumented oAuth api that has been implemented
as a server-side authentication mechanism against Twitter.
Authentication against other could also be hosted as needed.

  --------------------------------------------------------------------------------------------------------------------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **High level Requirements**                                                                                                             **Notes**
  Get session token from Twitter with oAuth protocol v1.0a.                                                                               This is done now by providing consumer\_key, consumer\_secret, access\_token, access\_token\_secret to the api as parameters. It would be better to design the api to get access to the consumer\_key and consumer\_secret (application pair of keys that MUST BE securely stored) and get the other two from redirect the user to Twitter and authenticate him there. Hence, users keys shouldn't be stored, now, since this isn't secure nor scalable.
  Specify Twitter ad-hoc functionalities, such as getTimeline, getMentions, postMessage, sendDirectMessage, getFollowers and getFrineds   These functions needs to be embedded server-side on a webinos module, just if the aim is to control all the communication to the tird-party service. From a design perspective, it would be useful to transfer the session\_token, therefore the session handling, to the application and allow it to deal with the webservice.
  --------------------------------------------------------------------------------------------------------------------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

[oAuth investigation](.html)

**Decision:** This will not be a task 3.4 API as it will be implemented
on a server as a service. The task 3.3 delivery will contain informative
text on the oAuth API.

Telephone API[¶](#Telephone-API)
--------------------------------

**Description:**\
**Rationale (requirement, architectural reference,etc):** See [Telephone
API scenarios and use cases](.html)\
**Responsible:** Nick Allott / Impleo\
**Notes:**

  ------------------------------------ ------------------------------------
  **High level Requirements**          **Notes**
                                       
                                       
  ------------------------------------ ------------------------------------

(note that the following table is only filled in if there already exist
one or more APIs that are candidates for use by webinos)

  -------------- -------------- -------------- -------------- --------------
  **Candidate    **Short        **Implementati **Gaps**       **Notes**
  existing API** Description**  on                            
                                Status**                      

                                                              
  -------------- -------------- -------------- -------------- --------------

**Decision:** This will not be part of the task 3.4 delivery. Instead it
will be added later based on work in the W3C System Applications WG.

Privacy aware Location and Proximity API[¶](#Privacy-aware-Location-and-Proximity-API)
--------------------------------------------------------------------------------------

**Description:** Enable location aware apps to determine location and
proximity in an abstract way that does not 'leak' too much information\
**Rationale (requirement, architectural reference,etc):** Physical
proximity is determined through the discovery API. Location is
determined through the GeoLocation API. The combination of these allows
location-aware apps to function
(</wp2-4/wiki/WOS-UC-TA7-004>).
However, according to the webinos white paper we strive to protect the
privacy of webinos users. For this, not only policies are required, but
also a more 'need to know' approach.\
**Responsible:** Victor Klos / TNO\
**Notes:**

  ------------------------------------------------------------------------------------------ ---------------------------------------------------------------------------
  **High level Requirements**                                                                **Notes**
  be able to query another party on location and receiving an abstract response              Like location is 'HOME' or 'WORK'
  be able to query another party on proximity by having the caller supply his own location   Are we proximate, I am at (lat x/lon y)?
  support throttling per relevant policy                                                     Making sure a users' actual location isn't queried by sending 1M requests
  ------------------------------------------------------------------------------------------ ---------------------------------------------------------------------------

**Decision:** There will not be a separate "Privacy aware Location and
Proximity API". Instead this functionality be added to the Context API.

Tethering API[¶](#Tethering-API)
--------------------------------

**Description:** Easily sharing mobile internet connectivity to somebody
who is near you\
**Rationale (requirement, architectural reference,etc):** One of the
scenario's is about local, hub-less connectivity. In many cases, one of
the participants in that scenario may actually have connectivity to the
greater internet and would possibly be willing to share that. See
[Tethering API scenarios and use cases](.html)\
**Responsible:** Victor Klos / TNO\
**Notes:**

  ------------------------------------ ------------------------------------
  **High level Requirements**          **Notes**

  allow someone access to ones         
  tethering device capability without  
  exchanging credentials, SSID etc     
  manually                             
  ------------------------------------ ------------------------------------

**Decision:** WITHDRAWN, see link in rationale

Secure Elements API[¶](#Secure-Elements-API)
--------------------------------------------

**Description:** Provide a means for applications to invoke functions on
contact or contactless smart cards via a lightweight implementation of
the APDU protocol.

**Rationale (requirement, architectural reference,etc):** See [Secure
Elements API scenarios and use cases](.html)\
**Responsible:** Dave Raggett, W3C\
**Notes:** This would provide valuable implementation experience into
standardization work in the W3C System Applications and NFC Working
Groups.

  ----------------------------------- -----------------------------------------------------------------
  **High level Requirements**         **Notes**
  iteration through terminals         there could be multiple named secure elements
  format commands                     convenience functions for assembling APDU command messages
  send command and process response   response should be handled asynchronously
  access response                     convenience functions for accessing response status and payload
  ----------------------------------- -----------------------------------------------------------------

(note that the following table is only filled in if there already exist
one or more APIs that are candidates for use by webinos)

  ------------------------------ ------------------------------- --------------------------- ------------------------------- ---------------------------------------
  **Candidate existing API**     **Short Description**           **Implementation Status**   **Gaps**                        **Notes**
  [Secure Elements API](.html)   inspired by existing Java API   to be implemented           best used with Web Crypto API   can be implemented on top of Java API
  ------------------------------ ------------------------------- --------------------------- ------------------------------- ---------------------------------------

**Decision:** This

Webinos Core API[¶](#Webinos-Core-API)
--------------------------------------

**Description: Webinos Core API provides information about the connected
pzp and pzh information.\
\*Rationale (requirement, architectural ): [Core Management API and Use
Cases](.html)\
\*Responsible: Habib Virji, Samsung\
\*Notes: This API will be enhanced to include Webinos details, the
details it will include are the PZP name, the PZH name, the application
identifier and the connection status of the PZP with the PZH and the
peer devices.**\
**Decision:** There will not be a separate "Webinos Personal Zone API".
Instead this functionality be added to the Webinos Core API.

Web Notifications API[¶](#Web-Notifications-API)
------------------------------------------------

**Description:** API to show small notifications to the user in order to
notify that "something" that could be of interest to the user happened\
**Rationale (requirement, architectural reference,etc):** During the
first phase of the project this functionality was implemented in the
webinos Widget API. W3C developed a specific API for this so that we
should consider to change our specifications to use the W3C one.\
**Responsible:** André Paul, Fraunhofer FOKUS\
**Notes:**

  ----------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------
  **High level Requirements**   **Notes**
  Display notification          An application want's to notify that something happened to the user (new eMail, task completed, etc)
  Discard notification          The user should be able to discard the notification
  Accept notification           The user should be able to accept the notification (for example in order to activate the notifying application so that more details can be shown)
  Close a shown notification    An application should be able to close a shown notification, for example in order to update the notification with a newer one
  ----------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------

(note that the following table is only filled in if there already exist
one or more APIs that are candidates for use by webinos)

  -------------- -------------- -------------- -------------- --------------
  **Candidate    **Short        **Implementati **Gaps**       **Notes**
  existing API** Description**  on                            
                                Status**                      

  webinos        API that       no             only text, no  
  Widgets API    provides       implementation HTML-Notificat 
                 access to      s              ions           
                 applications                                 
                 meta data and                                
                 in addition                                  
                 profides a                                   
                 simple notify                                
                 and                                          
                 cancelNotify                                 
                 function                                     

  W3C Web        dedicated API                 only text, no  
  Notifications  that allows                   HTML-Notificat 
                 web sites to                  ions           
                 show native                   (but text      
                 small                         could be       
                 notifications                 interpreted as 
                 to the user                   markup by the  
                                               implementation 
                                               ,              
                                               HTML support   
                                               may be later)  
  -------------- -------------- -------------- -------------- --------------

**Decision:**

Template API[¶](#Template-API)
------------------------------

**Description:**\
**Rationale (requirement, architectural reference,etc):** See [Template
API scenarios and use cases](.html)\
**Responsible:**\
**Notes:**

  ------------------------------------ ------------------------------------
  **High level Requirements**          **Notes**
                                       
                                       
  ------------------------------------ ------------------------------------

(note that the following table is only filled in if there already exist
one or more APIs that are candidates for use by webinos)

  -------------- -------------- -------------- -------------- --------------
  **Candidate    **Short        **Implementati **Gaps**       **Notes**
  existing API** Description**  on                            
                                Status**                      

                                                              
  -------------- -------------- -------------- -------------- --------------

**Decision:**

