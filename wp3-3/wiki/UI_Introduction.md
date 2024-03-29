UI Adaptation - Introduction[¶](#UI-Adaptation-Introduction)
============================================================

UI adaptation is a process of transforming the UI of an application
according to the device capabilities, which can be:

-   different screen resolutions, as depicted below\
    ![](resolutions2sm.png)
-   different input methods: keyboard, mouse, tv remote, in-car
    controller knob
-   different output methods: screen, voice
-   different hardware resources (e.g. camera) that need their specific
    UI components

The transformation itself should be based upon a shared code and a set
of rules, meaning it should conform to the "write once, run anywhere"
principle. It would help not only the developers, but also the end-users
to receive an app, that is best suited to the device on which it runs,
providing an equally positive experience. And because you never know
what future will bring, the solution has to be flexible and ready for
extensions.

Since webinos is a cross-platform application delivery environment
across a wide range of devices, UI adaptation is needed.

------------------------------------------------------------------------
