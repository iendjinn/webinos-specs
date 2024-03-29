Policy Structure[¶](#Policy-Structure)
======================================

As decided in the [call on 3rd April
2013](https://docs.google.com/document/d/1b3V3QRsNfZDtceppFWpjZIb8yYixgwqgCjWNkyGfpho/edit?usp=sharing),
webinos policies will have the following structure.

Root policy file[¶](#Root-policy-file)
--------------------------------------

The root policy file will never be edited and is used just to pull in
the other policies.

It uses two combining rules: the "Deny-unless-permit" rule requires the
PDP to reply with a 'deny' result if there are any 'not applicable'
results returned from the inner policy. The "Deny-overrides" combining
rule means that any one policy saying "deny" will override the others.
This means that manufacturer policies will override users, which is an
important requirement.

Note that the "Deny-unless-permit" policy needs to be changed to
accommodate Prompt effects as well as Allow, Deny and Not Applicable.
Because no existing combining rule exists, we suggest defining our own,
called "Deny-if-not-applicable" or "Deny-unless-permit-or-prompt".

policy.xml:\

     1 <!DOCTYPE doc [
     2     <!ENTITY manufacturer SYSTEM "manufacturer.xacml">
     3     <!ENTITY user SYSTEM "user.xacml">
     4     <!ENTITY app SYSTEM "app.xacml">
     5 ]>
     6 <policy-set combining-algorithm="Deny-unless-permit-or-prompt">
     7     <policy-set combining-algorithm="Deny-overrides">
     8         &manufacturer;
     9         &user;
    10         &app;
    11     </policy-set>
    12 </policy-set>

As discussed in Turin meeting (June 20th 2013) an alternative proposal
for root policy is the following:

     1 <!DOCTYPE doc [
     2     <!ENTITY manufacturer SYSTEM "manufacturer.xacml">
     3     <!ENTITY user SYSTEM "user.xacml">
     4     <!ENTITY app SYSTEM "app.xacml">
     5 ]>
     6 <policy-set combining-algorithm="Deny-unless-permit-or-prompt">
     7     &manufacturer;
     8     <policy-set combining-algorithm="First-maching-target">
     9         &app;
    10         &user;
    11     </policy-set>
    12 </policy-set>

This way the manufacturer will be combined (using deny-overrides) with
application policy or with user policy (in case application policy does
not exists or returns inapplicable or undetermined).

The "deny-unless-permit-or-prompt" combining algorithm should behave in
a similar way to the "deny-overrides" combining algorithm defined in
<http://www.webinos.org/content/html/D033/Policy.htm>. The exception
being that the "deny-unless-permit-or-prompt" algorithm returns deny if
the result is undetermined. This differers from the XACML 3.0
"deny-unless-permit" definition in that we weight towards *deny* where
as the "deny-unless-permit" is weighted towards *permit*.

If we adopt this approach, the definition of
"deny-unless-permit-or-prompt" becomes:

-   If any child evaluates to "deny", then the overall result is "deny".
-   Otherwise, if any child is "undetermined", then the overall result
    is "deny".
-   Otherwise, if any child evaluates to "prompt-oneshot", then the
    overall result is "prompt-oneshot".
-   Otherwise, if any child evaluates to "prompt-session", then the
    overall result is "prompt-session".
-   Otherwise, if any child evaluates to "prompt-blanket", then the
    overall result is "prompt-blanket".
-   Otherwise, if any child evaluates to "permit", then the overall
    result is "permit".
-   Otherwise, the overall result is "deny".

An alternate definition which weights towards "permit" would be:

-   if any child evaluates to "permit", then the overall result is
    "permit".
-   Otherwise, if any child evaluates to "prompt-blanket", then the
    overall result is "prompt-blanket".
-   Otherwise, if any child evaluates to "prompt-session", then the
    overall result is "prompt-session".
-   Otherwise, if any child evaluates to "prompt-oneshot", then the
    overall result is "prompt-oneshot".
-   Otherwise, the overall result is "deny".

The first definition should be adopted as the algorithm as this
definition supports the goal that the manufactures policy should be able
to override the users policy to restrict access. If the first definition
is used we have the following comparison between
"deny-unless-permit-or-prompt" and "deny-overrides":

Algorithm results (AL = allow, DE = deny, PR = prompt, UN =
undetermined, IN = inapplicable)

  --------- --------- ------------------------------ ----------------
  Input 1   Input 2   Deny-unless-permit-or-prompt   Deny-overrides
  AL        AL        AL                             AL
  AL        DE        DE                             DE
  AL        PR        PR                             PR
  AL        UN        DE                             UN
  AL        IN        AL                             AL
  DE        AL        DE                             DE
  DE        DE        DE                             DE
  DE        PR        DE                             DE
  DE        UN        DE                             DE
  DE        IN        DE                             DE
  PR        AL        PR                             PR
  PR        DE        DE                             DE
  PR        PR        PR                             PR
  PR        UN        DE                             UN
  PR        IN        PR                             PR
  UN        AL        DE                             UN
  UN        DE        DE                             UN
  UN        PR        DE                             UN
  UN        UN        DE                             UN
  UN        IN        DE                             UN
  IN        AL        AL                             AL
  IN        DE        DE                             DE
  IN        PR        PR                             PR
  IN        UN        DE                             UN
  IN        IN        DE                             IN
  --------- --------- ------------------------------ ----------------

Manufacturer policies[¶](#Manufacturer-policies)
------------------------------------------------

We did not decide on the exact structure of manufacturer policies. They
must be write-protected on the platform. They must also have a root
policy set.

User policies[¶](#User-policies)
--------------------------------

These are edited by the policy editor application and may be split
further into other sets.

We did not decide on the exact structure of user policies or combining
rules. These are likely to contain rules about users, devices and
services, such as "Alice can access Bob's geolocation service".

Application policies[¶](#Application-policies)
----------------------------------------------

These are generated at install time and consolidated into one policy
set. These define the least-privilege restrictions on an application,
such that applications can only access resources they ask for.

We did not decide on the exact structure of user policies or combining
rules. A "first applicable" or "only one applicable" rule may be best.

It could be that this policy file simply references individual policy
files for each application, or it could be that this policy file
contains policies for each application.

