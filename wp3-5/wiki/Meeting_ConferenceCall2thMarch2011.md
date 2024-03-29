Conference Call 25th March 2011[¶](#Conference-Call-25th-March-2011)
====================================================================

Agenda[¶](#Agenda)
------------------

### Current Status[¶](#Current-Status)

-   3.1 has begun to make decisions and produce plans and output, there
    is plenty of material now on the wiki
    -   In 3.5 we've been quiet, but there is a structure for the
        deliverable and we're beginning to see some of the issues
    -   It is now time to crack on with outlining the security
        architecture
    -   We don't have that much time: less than a month of real time
        before the May meeting, then another month before we need to
        have something ready to review and edit.

<!-- -->

-   I am aware of the following activities which definitely need to be
    reflected in the Security Architecture
    -   Policy Management
    -   User management
    -   Security APIs

<!-- -->

-   However, there are equally important security issues occurring in
    all the different sections of 3.1 and 3.2, and our challenge is to
    keep track of them and make sure they remain consistent.

### Plans and work allocation[¶](#Plans-and-work-allocation)

-   We need to take out inputs: the requirements, 3.1, 2.7 and identify
    the key security concerns.
    -   I propose doing this by [mirroring the 3.1
        work](mirroring%20the%203.1%20work.html) and extracting relevent
        requirements, threats / risks, and mitigations
    -   This is easily done in parallel: Each partner is responsible for
        the areas they are working on
    -   This should compliment work on 2.8 - the asset modelling. We're
        looking top-down, while 2.8 works bottom-up. Output from 2.8
        should help us prioritise later on.
    -   On this page I would like to see:
        -   a list of all the assets and components (e.g. logical parts
            of webinos) currently present in this area. This might be
            drawn from the [Environment Models in
            T2.7](/wp2-7/wiki/COU_Environments)
        -   a list of the known security *and privacy* concerns. E.g.
            "avoid unauthorised access to private data when doing X, Y
            or Z", "require user authentication"
        -   a list of mitigations / strategies for avoiding problems.
            E.g. "Using a transport session", etc.
        -   a list of
            [requirements](/wp2-2/wiki)
            relevent to this area
        -   a list of missing requirements
        -   Examples of any security policies required (or being
            specified)

<!-- -->

-   We can then work on producing a first iteration of this deliverable
    before the WP3 meeting at the beginning of May. Therefore, I would
    like this work completed by the 11th April.
-   I hope to condense and summarise the main results and put them into
    the [Scope\_Discussion](.html)
-   *agenda item*: allocation of effort to this work initially. See
    [Links\_To\_Tasks](.html) page.
-   Separately to this, we (Oxford, Polito?, those with more effort?)
    will be looking at issues that do not map obviously to 3.1 areas.

### Other issues[¶](#Other-issues)

-   Issue raised by Sven: [specific privacy and security requirements on
    identity
    issues](http://dev.webinos.org/redmine/boards/7/topics/13?r=16#message-16)
-   Issue raised by Cesare: [Privileged
    applications](http://dev.webinos.org/redmine/boards/7/topics/13?r=19#message-19)
-   Authentication mechanisms: update from the IDM group, but further
    thoughts on how to manage multiple identity systems, multi-factor
    authentication, etc, would be beneficial.
    -   *agenda item*: can someone take this on?

<!-- -->

-   Inter-process communication and access control. How do applications
    on the **same** device communicate, and how do we specify
    permissions? Improvements on the Android model sought.
-   Intercept points in the policy architecture
-   Privacy issues - evaluation work needed.
-   Structure and isolation of webinos applications - creation of a
    "secure execution model"
    -   *agenda item*: Oxford quite happy to look into this, but will
        depend on platform assumptions (e.g. the OS we're supporting,
        etc). Can anyone else be involved?

<!-- -->

-   Thought to keep in mind: we have the opportunity to ask T2.7 to do
    an experiment for us on security and privacy expectations. If one
    springs to mind, let me know.
-   Draft deliverable structure - feedback? Volunteers needed to have a
    look and even start filling in the [deliverable
    template](deliverable%20template.html). Cloud security models in
    particular?
    -   *agenda item*: can I have an action on someone to have a look at
        this?

<!-- -->

-   Regular conference calls on T3.5: how often and when?

### Deadlines[¶](#Deadlines)

-   Work described above: 11th April
-   First deliverable iteration: 20th April

Minutes[¶](#Minutes)
--------------------

### Attendance[¶](#Attendance)

John Lyle, Oxford\
Nick Allott\
Simon, BMW\
Sven, DOCOMO\
Andrea, Polito\
Hans, Ambiesense\
Ziran, Samsung

### Actions[¶](#Actions)

-   *All 3.5 partners* to extra security issues from 3.1 and 3.2 areas
    to the [Links\_To\_Tasks](.html) page
-   Andrea (and possibly Sven) to have a look at the OWASP threats and
    create a page on our current solutions to them
-   Nick to spend some time looking at how we can specify policies for
    company data and work/personal interaction - Might be worth doing so
    on this [Policy Management
    page](/wp3-1/wiki/Policy_Elements)
-   John to get in touch with Sony Ericsson, W3C and TIS
-   John to look into secure execution environment and isolation,
    possibly with help from Sony Ericsson. Plan to clearly identify
    layers and make recommendations.

Unassigned:

-   Looking into inter-application communication and policies, plus
    links to the events area
-   Example privileged application policies

