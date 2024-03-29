Cross-Device Policy Synchronisation[¶](#Cross-Device-Policy-Synchronisation)
============================================================================

How do devices synchronise policies for the same applications? How do
interactions between devices work?

Back-link to the [Policy Management main
page](Policy%20Management%20main%20page.html).

I assume that we will use a combination of SAML 2.0 to send security
assertions around and XACML 3.0 to write the assertions. Interestingly,
XACML supports delegation.

Example use cases[¶](#Example-use-cases)
----------------------------------------

### Installing an app ('A') on device 'D', granting it permissions, and then wanting to allow it to use device 'E'[¶](#Installing-an-app-A-on-device-D-granting-it-permissions-and-then-wanting-to-allow-it-to-use-device-E)

-   Assume device 'D' and 'E' are used only by the user Justin.
-   Justin "installs" 'A' on 'D'.
-   At end of install process, after granting the application some
    permissions, Justin is prompted "This application can be used on
    multiple devices. Install on [list of user devices and tick box]?"
-   Justin selects that the application should be installed on device
    'E' as well.
-   Prompt: "Give application permission to access the same resources? /
    Customise permissions / Ask me later?"
-   Justin clicks "give same resources"
-   Webinos runtime creates a message to device 'E' containing
    instructions for doing this.
    -   Name of application, permissions granted on *this* device
    -   Justin's credentials/signature ? Signature by device in current
        state?

<!-- -->

-   Message queued to be sent on the overlay network to the other
    device, using a secure transport session. This may happen
    immediately if possible (e.g. if device 'D' is a home server) or may
    wait for a proximity event, or may be queued on a cloud service
    waiting for the user to interact with device 'D' in the future.

Issues:

-   What credentials need to be sent on this policy update? I think
    webinos identity management probably needs to allow a "signature in
    current state" function to encapsulate the state in which an
    instruction was formed (e.g. "user logged in on device D" state)
-   How to stop malicious update messages? Do we rely on this being
    authorised on the other platform by the user?
-   How does the "Same resources" work if the available resource are
    different. E.g. location information on Device 'D' might be
    different from location sensors on device 'E'. This implies some
    tagging of similar functionality.
-   How will the policy update message be structured?

### Using device 'D' to remove permission for app 'A' to access resource 'R' on all devices (Device 'D' and 'E')[¶](#Using-device-D-to-remove-permission-for-app-A-to-access-resource-R-on-all-devices-Device-D-and-E)

-   Peter has been using app 'A' and decides he doesn't trust it after
    being told by a friend that it sends data to advertisers.
-   He is using device 'D', as this is his main device
-   He navigates to the policy management area (or maybe he right-clicks
    on the application icon) and selects "remove".
-   He is asked whether he wants it to be removed across all of his
    devices (a list of his local devices might be selected) and he
    clicks on all of them.
-   Webinos runtime generates an update message to each device in his
    cloud, including device 'E', in a secure manner:
    -   "Remove app", app name
    -   user credentials, device credentials
    -   \^\^ all signed

<!-- -->

-   These are sent when the device is able to connect to other devices
    and when these devices are capable of authenticating themselves
-   Depending on the device security policies, the deletion may happen
    automatically, or the app might be isolated and require local
    permission to delete?

Issues:

-   Same as the previous use case
-   Seems to be a clear requirement for a "Trusted message router" in
    the overlay network. which can provide a publish/subscribe for
    authenticated communication
-   Seems also the be a clear requirement for attesting user status.
    Ideally, in combination with an attestation of device integrity.

### Using device 'D' to authorise app 'A' to access resource 'P' on device 'E' (E and D owned by the same user)[¶](#Using-device-D-to-authorise-app-A-to-access-resource-P-on-device-E-E-and-D-owned-by-the-same-user)

### Using device 'D' to authorise app 'A' to access resource 'P' on device 'E' (E and D owned by different users)[¶](#Using-device-D-to-authorise-app-A-to-access-resource-P-on-device-E-E-and-D-owned-by-different-users)

-   Helen is using app 'A' and wants to use it to access her friend
    Gloria's photos on device 'D'.
-   She selects to discover other devices, and finds Gloria's device 'D'
-   She requests access to photos on 'D'.
-   Gloria's device prompts Gloria to allow this and present's Alice's
    device details, as well as the history of communication with this
    device.
-   Gloria approves the communication
-   Gloria's runtime adds a temporary permission for the photo app
    (resource 'P') on Gloria's phone

Issues:

-   Will protocol-level permissions complicate matters? E.g. permissions
    in bluetooth or whatever protocol might make granting permissions in
    webinos rather tedious.
-   Unforgable device identities would make presenting the history of
    previous interaction easier and more trustworthy.

### Updating labels on stored user data - marking some as 'private' on device 'D' and having the same data on device 'E' automatically tagged.[¶](#Updating-labels-on-stored-user-data-marking-some-as-private-on-device-D-and-having-the-same-data-on-device-E-automatically-tagged)

-   Gloria decides to make sure her personal data is being protected
    appropriately
-   She looks at her webinos device to see what data about her is known
-   Some data is marked as "private" and other data is not.
-   She notes that her "place of work" is listed but not marked as
    private
-   She tags this data as "private" and therefore all policies apply to
    it that apply to other private data.
-   She tells webinos to update this setting on all her devices
-   Webinos queues a policy update for device 'E':
    -   Update policy, data item, new XACML
    -   User credentials, device credentials
    -   \^\^ all signed

Issues

-   I'm assuming that the runtime manages a data store. Most of this
    data is private. Should all of it be private by default?
-   How would marking data as "private" modify application behaviour?

### Browsing application policies on all devices[¶](#Browsing-application-policies-on-all-devices)

### Registering device 'F' as being a trusted device with respect to device 'D' and device 'E'[¶](#Registering-device-F-as-being-a-trusted-device-with-respect-to-device-D-and-device-E)

-   Anna has just bought a new tablet PC ('F'), and would like it to
    automatically synchronise with other devices
-   She uses it to discover her mobile phone ('D'), a webinos device.
-   On discovery, she selects the mobile phone symbol and choses to join
    the "local webinos device cloud"
-   Untrusted message from tablet to phone:
    -   "device join", device ID

<!-- -->

-   This prompts her mobile phone to authenticate her
-   She enters her credentials into the phone
-   The phone adds this device to a "known" and "personal devices" set
-   The tablet PC downloads the relevant set of policies (as well as
    profile info - out of scope ) from the mobile phone and applies
    them. This includes the identity of other devices in the cloud.
    -   Should be a set of "policy update" messages?

Issues

-   Which policies are relevant to the new device?
-   Is there enough authentication here?
-   What stops a user registering someone else's device as a member of
    their own personal cloud?
-   Does there need to be more fine grained permissions than just a
    "join"?
-   Clear requirement for the definition of a personal device cloud
    membership concept

Related concerns[¶](#Related-concerns)
--------------------------------------

-   Automatic synchronisation of policies could have unexpected
    consequences?
-   I'm assuming policies are stored (cached) locally on each device,
    but that they are then communicated relatively freely. However, the
    policies should be protected in transit and at rest, are there
    privacy issues here?

