System Authentication[¶](#System-Authentication)
================================================

How does the user authenticate "the system"? including devices,
interfaces, etc.

More specifically - how does a user authenticate the personal zone hub
and farm interfaces?

Personal zone hub[¶](#Personal-zone-hub)
----------------------------------------

### Authentication[¶](#Authentication)

The PZH web interface is authenticated to users through SSL
certificates. This relies on a browser being able to interpret these
certificates, as well as the user recognising the URL of their PZH. It
also relies on the certificate matching this URL.

### Revocation[¶](#Revocation)

The PZH might be moved, and the original certificate ought to be
revoked.

    TODO: How do we do this?  Where's the OCSP server going to exist?

Webinos web runtime[¶](#Webinos-web-runtime)
--------------------------------------------

    TODO: How do users trust the webinos web runtime agent?
