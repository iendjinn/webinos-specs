TV Control API[¶](#TV-Control-API)
==================================

JavaScript interfaces[¶](#JavaScript-interfaces)
------------------------------------------------

Refer to the [documentation created from the web
IDL](http://dev.webinos.org/specifications/draft/tv.html).

EVERYTHING BELOW IS OUTDATED![¶](#EVERYTHING-BELOW-IS-OUTDATED)
===============================================================

Introduction[¶](#Introduction)
------------------------------

This API has the following goals:

-   Provide functionality to access the channel list and information
    like type and name of a channel.
-   Switch between channels.
-   Stop/start the broadcast.
-   Access to the current parental rating of the broadcast.

This API builds on two existing approaches and merges both. The basis
for this API is the HTML5 video element interface (HTMLVideoElement).
The here specified interface HTMLTVElement extends the video element and
provides the functionality necessary to achieve the mentioned goals on
top of it. This added functionality is based on the Open IPTV Forum
Release 2 Volume 5 Specification for Declarative Application
Environment.

Example for a HTMLTVElement in HTML:\

    1 
    2 <video width="640" height="480" controls>
    3   <source src="tv">
    4 </video>
    5 

Events[¶](#Events)
------------------

Handlers for the following event can be registered.

  ----------------------- --------------------------------------------------------------------------------------------------------------------------------------------
  **Event**               **Description**
  ParentalRatingChanged   Event fires when the current showing broadcast has a different rating compared to the previous parental rating of the preceding broadcast.
  ----------------------- --------------------------------------------------------------------------------------------------------------------------------------------


