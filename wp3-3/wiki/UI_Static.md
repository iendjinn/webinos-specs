Static diagrams[¶](#Static-diagrams)
====================================

The adaptation is regulated and executed by two main components. The WRT
is linked to the webinos bootstrap component (which is injected at
start-up time). This component contains an *Adaptation Client* which is
bootstrapped at application launch and will execute all the UI
adaptations. The second component is the *Adaptation Manager*, which
resides in the PZP. The Adaptation Manager aggregates all the rules,
analyzes the rules and stores them in an Adaptation Rule Engine,
registers itself with various services, fetches properties and fires
adaptation rules by sending them to the Adaptation Client.

![](UI_Adaptation.svg)

As the figure above demonstrates, the Application is the packaged
application as explained in the section "webinos Applications and Widget
Runtime specification". The application contains its content and various
metadata. Newly defined here are the application rules, which can be
defined by application developers who want to adapt their application to
the running context and context changes. The metadata will also contain
two settings:

-   A setting which can disable the adaptation process completely
-   and one that will only disable the generic platform adaptation rules
    contained in the Adaptation Manager.

