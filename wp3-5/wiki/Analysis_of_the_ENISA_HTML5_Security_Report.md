Analysis of the ENISA HTML5 Security Report[¶](#Analysis-of-the-ENISA-HTML5-Security-Report)
============================================================================================

The report is linked here -
<http://www.enisa.europa.eu/act/application-security/web-security/a-security-analysis-of-next-generation-web-standards/at_download/fullReport>

The following sections cover threats and recommendations relevant to
webinos

Threat: GEOLOC-SECURE-3.Cache Polling[¶](#Threat-GEOLOC-SECURE-3Cache-Polling)
------------------------------------------------------------------------------

### Details[¶](#Details)

> The use of the geo-location cache API allows the explicit retrieval of
> the latest geo-location entry from a cache, according to the freshness
> criteria specified in the query. While this feature reduces the
> power-intensive geo-location queries, it also allows an attacker to
> retrieve a previous location of the end-user, as well as timing
> information on that particular location. The specification does not
> provide upper limits on the lifetime of geo-location cache entries.

### Mitigation in webinos[¶](#Mitigation-in-webinos)

...

Recommendation: Controlling Functionality[¶](#Recommendation-Controlling-Functionality)
---------------------------------------------------------------------------------------

### Details[¶](#Details)

> current restrictive systems (i.e. the sandbox attribute
> [HTML5ATTR-SECURE-2] or the Widget Access Request Policy
> [WARP-SECURE-1.Coarse-Grained Approach]) are very coarse-grained and
> only offer the option of enabling or disabling a certain
> functionality. It is currently impossible to integrate third-party
> functionality into a web application (e.g. in a mashup scenario) while
> applying the least-privilege security principle. In such a scenario,
> either access to all security-sensitive APIs is given while relying on
> the same-origin policy and user-consent mechanisms, or scripts are
> completely disabled.

> One approach is the use of additional fine-grained policies. Such
> policies are typically enforced at the client-side, but are often
> provided by the server. There are several types of policies available,
> either in the form of additional response headers page (e.g. Content
> Security Policy [27] and X-Frame-Options [26]) or embedded in the
> page. The latter can be achieved by using an inline reference monitor
> technique (e.g. ConScript^[19](#fn19)^, Safe JavaScript
> Wrappers[20,21], WebJail^[22](#fn22)^) or by ensuring the safety of
> the language, based on the capability security model (e.g. Caja [23]).

Essentially, it should be easy to integrate untrusted external content
into your HTML5 page with fine-grained security policies.

### How webinos will react[¶](#How-webinos-will-react)

...

Recommendation: Permission System Design[¶](#Recommendation-Permission-System-Design)
-------------------------------------------------------------------------------------

### Details[¶](#Details)

> Several specifications include a permission system, without any
> consistency between these

systems. This is troublesome, since some systems are fairly weak
compared to other\
systems. One good example is the Geo-location API versus the System
Information API,\
where the latter is much more extended (e.g. it requires permission for
a pair of origins for\
a framed document and distinguishes between one-shot vs. monitoring
permissions).

### How webinos will react[¶](#How-webinos-will-react)

...

Recommendation: User Interfaces[¶](#Recommendation-User-Interfaces)
-------------------------------------------------------------------

### Details[¶](#Details)

> The specifications do not include much detail about the user
> interfaces for giving permissions and managing permissions. Typically,
> they require that the origin of the document is displayed. One major
> missing item is the nature of the permission (one-shot vs watching
> process) as well as the actual document requesting it (e.g. is it
> sandboxed or framed? is it visible?). For managing permissions, the
> specifications typically state that it should be clear and easily
> usable. This is very vague and is not even a strong requirement
> (should instead of must).

> One recommendation is to extend the specifications to include more UI
> requirements. At least all the aspects of the requested permission
> should be present. For managing the permissions, the specifications
> should describe how it should happen (not what it should look like).
> For example, they could state that "A user must be able to get an
> overview of all assigned permissions, grouped per origin".

> A second recommendation is to include these UI requirements into the
> abovementioned separate permission specification, which is then
> referenced from all other specifications requiring a permission
> system. This ensures consistency and facilitates improvements or
> extensions of the permission system.

### How webinos will react[¶](#How-webinos-will-react)

...

Recommendation: End User Policing[¶](#Recommendation-End-User-Policing)
-----------------------------------------------------------------------

### Details[¶](#Details)

> Several specifications depend on the end user to ensure security,
> typically by means of a permission system. With the rapid development
> of new APIs offering new functionality, this approach is reaching its
> limits. Typical web users are unable to assess the ramifications of
> granting certain permissions to certain origins. Additionally,
> involving the user too often might quickly lead to blindly approving
> permissions.

> A first recommendation is to require an awareness indicator, so the
> user knows when a site is using a granted permission (e.g. when a site
> is locating the user). Currently, this is only included as a
> suggestion in the Geo-location API and is missing from other APIs,
> such as the System Information API.

> A second recommendation is to offer the users a way to select
> predefined security profiles or to create a security profile (e.g. by
> means of a wizard, which could explain the ramifications of sharing
> your location and then provide the option to allow this or not.). Once
> a security profile is chosen, it is used to determine the appropriate
> actions when a site requests permission for an action.

### How webinos will react[¶](#How-webinos-will-react)

...

