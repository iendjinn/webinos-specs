PZH key storage[¶](#PZH-key-storage)
====================================

-   [PZH key storage](#PZH-key-storage)
    -   [Overview](#Overview)
    -   [The Threats and Attacks.](#The-Threats-and-Attacks)
        -   [Attack Trees](#Attack-Trees)
        -   [Compromising the PZH](#Compromising-the-PZH)
        -   [Attacker personas to
            consider.](#Attacker-personas-to-consider)
    -   [CA key constraints](#CA-key-constraints)
    -   [Potential Solutions](#Potential-Solutions)
        -   [Storing CA keys unprotected](#Storing-CA-keys-unprotected)
        -   [Slight improvement: separating CA keys and CRL signing
            keys](#Slight-improvement-separating-CA-keys-and-CRL-signing-keys)
        -   [Storing CA keys on a different host to the PZH Farm and web
            server](#Storing-CA-keys-on-a-different-host-to-the-PZH-Farm-and-web-server)
        -   [Storing CA keys in trusted
            hardware](#Storing-CA-keys-in-trusted-hardware)
        -   [Storing CA keys encrypted using a user-held
            password.](#Storing-CA-keys-encrypted-using-a-user-held-password)
        -   [Storing keys in the OS KeyStore mechanism (E.g. Gnome
            Keyring)](#Storing-keys-in-the-OS-KeyStore-mechanism-Eg-Gnome-Keyring)

Overview[¶](#Overview)
----------------------

The PZH Farm holds CA keys for each personal zone hub it hosts. Keys
must be stored and protected from theft or misuse. This page documents
suggestions for a PZH Farm deployment profile for how keys could be
stored and protected. This suggestion would be non-normative, but is of
interest to anyone deploying a PZH Farm.

The Threats and Attacks.[¶](#The-Threats-and-Attacks)
-----------------------------------------------------

The PZH CA keys can be misused in the following ways:

-   To create a new, malicious device within the user's personal zone
    and potentially access all of the user's data and resources
-   To create a malicious device and impersonate the end user
-   To create a new, fake personal zone for the user as a means of
    impersonation and targetting attacks on the user's friends and
    contacts
-   To revoke devices as a denial or service (or attack on reputation)
    on the end user

It is important to differentiate the *use* of the PZH Key and
*posession* of the PZH Key. Use is bad - it could sign an arbitrary
certificate - but theft is worse. Use can be identified through logging
and auditing. Theft cannot.

The threat of insider attack (e.g. a malicious employee at the PZH Farm
provider) is not considered. This is a much harder threat to mitigate.

### Attack Trees[¶](#Attack-Trees)

    TODO.

### Compromising the PZH[¶](#Compromising-the-PZH)

Is there any point in protecting the PZH CA keys more rigorously than
the PZH Farm itself? If an attacker can compromise the PZH, they can
intercept all traffic and probably steal all user data anyway.

Points:

-   Compromising the PZH will give attackers access to any data stored
    on the PZH, as well as the ability to request access to data on the
    users' devices. The full impact of this attack will depend on the
    user's awareness (expected low), policies (which can be modified by
    the compromised PZH, but will they be updated on PZPs?), and any
    intrusion detection system we develop.
-   Compromising a PZH just provides a window of access, and therefore
    the attacker would have to frequently revisit the compromised PZH or
    install malware to maintain their access to the system. This could
    potentially be recovered from if detected, and ought to be easier to
    detect. Theft of keys is a one-shot event that is hard to recover
    from unless detected, and then causes a lot of difficulties for all
    users.

In summary: it's probably not worth spending **too much** effort on
protecting the keys compared to the platform, but they definitely
**are** more important and we should consider how they might be
protected.

### Attacker personas to consider.[¶](#Attacker-personas-to-consider)

-   Frankie might attempt to compromise the PZH Farm. Probably just to
    cause mischief, or as a targeted attack on a particular person he
    knows. He's most likely to try and use well-known system
    vulnerabilities based on scripts he has found online, or guess the
    password of a user to get to their web interface.
-   Ethan is capable of exploiting the PZH farm. He's most interested in
    finding user data and installing malware. He is worried about being
    caught, so stealing keys and then leaving the host might be
    attractive to him. He may want to install a botnet on the host
    itself, or use stolen keys to try and remotely install software on
    all the devices belonging to users of that PZH Farm. As the PZH wont
    hold any credit card details (we assume) it is not, in itself, a
    particularly interesting attack beyond follow-on attacks on the
    larger network.
-   Gary might want to compromise a PZH hosted at a company in order to
    make the company look bad. Theft of user data and keys would make
    this attack better. He's not necessarily that careful, so some kind
    of intrusion detection would help catch him. However, he probably
    does have privileged access to every system, so isolation and access
    conrol wont.
-   Harold, David and Irwin seem relatively unlikely attackers at the
    moment.

CA key constraints[¶](#CA-key-constraints)
------------------------------------------

The CA keys must be accessible from the PZH in order to add new or
revoke devices from the personal zone. Availability and performance is
not that important - they will be used very rarely - but they must be
available on demand. Of particular importance is their ability to sign
CRLs and revoke devices.

Potential Solutions[¶](#Potential-Solutions)
--------------------------------------------

### Storing CA keys unprotected[¶](#Storing-CA-keys-unprotected)

The most simple solution would be what we have now - no protection is
provided for the CA keys. They are stored on the PZH server in plain
text, and we rely on the security of the platform to prevent
unauthorised access.

**Advantages**\
No work needed. Easy to

**Disadvantages**\
Theft and misuse of keys possible for any successful remote attacker.

### Slight improvement: separating CA keys and CRL signing keys[¶](#Slight-improvement-separating-CA-keys-and-CRL-signing-keys)

One improvement would be to separate the CA key from the CRL signing
key. While CRL signing keys can be misused to perform denial of service
attacks, this is not as valuable an attack (potentially) and arguably of
less interest to attackers. Furthermore, a malicious CRL could be
deleted relatively easily. CRL keys are also arguably more important to
have available on the PZH Farm, as they are needed to revoke devices
when lost or stolen, which is a considerable threat.

Therefore, CRL keys could be left relatively unprotected and CA keys
could be better protected with less impact on other mitigations.

The only disadvantage is that it requires some extra work on the
implementation.

### Storing CA keys on a different host to the PZH Farm and web server[¶](#Storing-CA-keys-on-a-different-host-to-the-PZH-Farm-and-web-server)

While the CA key must be available to the PZH Farm, it does not
necessarily have to be hosted there. For example, a separate internal
server could offer an internal "sign(keyid, certificate)" function,
returning a signed certificate using the requested keyid. This means
that compromising the PZH Farm would allow an attacker to create signed
certificates, but would not allow theft of the CA key, as it would
reside on a different platform (in theory - this relies on the other
platform being better protected. This might be the case as the second
platform could have a much better protected OS and minimal TCB). The
separate platform could also be rate-limited, preventing too many
certificates being issued too often, as an intrusion detection
mechanism. It would also be able to log the results in a protected
manner.

**Advantages**\
Protects against theft, assuming the second host is better protected.
Might provide logging and intrusion detection

**Disadvantages**\
Requires an additional host. Does not prevent misuse.

### Storing CA keys in trusted hardware[¶](#Storing-CA-keys-in-trusted-hardware)

Possibly the best solution is to use a TPM on the host to store CA keys.
Because TPM keys cannot leave the TPM, they are inaccessible even if the
platform is completely compromised. However, they can still offer a
similar "sign(keyid, data)" function, making the keys useful.

**Advantages**\
Requires no additional host server, keys are very well protected. Also
mitigates some insider attack problems. Could be combined with malware
identification.

**Disadvantages**\
Requires some work on backup and recovery. Mandates a certain piece of
hardware. Slow. Does not prevent misuse or provide much logging.

### Storing CA keys encrypted using a user-held password.[¶](#Storing-CA-keys-encrypted-using-a-user-held-password)

If we introduced a password into the user experience of webinos, the CA
keys could be encrypted with this password. This means that a remote
attacker would need to do more work to compromise keys, as theft of keys
would still require decryption. Even if one password was compromised,
this would not result in loss of all CA keys.

**Advantages**\
Protects each key individually. Requires no new hardware or separate
hosts. The password could be reused for other things, such as local
storage.

**Disadvantages**\
Requires users to have (and remember) a password. It also requires a
recovery mechanism in case the password is lost. Passwords provide
relatively weak protection from offline attacks, and passwords are
commonly weak. Breaks our current model and principles of not creating
new authenticators.

### Storing keys in the OS KeyStore mechanism (E.g. Gnome Keyring)[¶](#Storing-keys-in-the-OS-KeyStore-mechanism-Eg-Gnome-Keyring)

OS-provided key storage could be used. This might provide more
protection for keys.

**Advantages**\
We already have most of the code. Requires no new software/hardware.

**Disadvantages**\
Dubious usefulness. Keystores are generally unlocked by users, but the
PZH Farm is a server without a local user. How is the keystore
protected? This doesn't seem to make much sense. Even if this added
user-separation to the key storage (e.g. requiring root access)
privilege escalation is trivial in most systems, and it would need the
PZH Farm to run as root.

