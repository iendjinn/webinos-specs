Evented rule-based adaptation of the DOM[¶](#Evented-rule-based-adaptation-of-the-DOM)
======================================================================================

<div class="uml">package App
  class "Meta-data"
  class "App Rules"
  class "Content"
end package

package "WRT" 
  class "Processor"
  class "Renderer"
end package

package "PZP" 
  class "AdaptationEngine"
  class "Platform Rules"
  class "DeviceStatus API"
end package

App - WRT
WRT - PZP

AdaptationEngine -- "Platform Rules"
AdaptationEngine -- "DeviceStatus API"</div>

An application is launched[¶](#An-application-is-launched)
----------------------------------------------------------

![](app-start-adaptation.png)

<div class="uml">"Adaptation Engine"->"App": fetchRules
"Adaptation Engine"->"Adaptation Engine": storeApplicationRules
"Adaptation Engine"->"Adaptation Engine": analyzeRules
"Adaptation Engine"->"WRT": injectListener
"Adaptation Engine"->"DeviceStatus API": fetchProperties
"Adaptation Engine"->"Adaptation Engine": selectRules
"Adaptation Engine"->"WRT": injectAdaptation
"WRT"->"WRT": adapt
"Adaptation Engine"->"DeviceStatus API": watchPropertyChange</div>

When an application is launched, the adaptation engine will fetch the
application's specific adaptation rules and store it in a separate
rulebase. It will then analyze the rules and make a distinction between
"static" and "dynamic" rules. Static rules are based on device
characteristics that can be considered static. E.g. screen size, light
intensity. Dynamic rules are based on changing properties, e.g. the
light goes below a certain threshold.\
It will then inject a listener into the WRT with the application that
will be able to accept adaptation rules fired by the devicestatus API.\
In a first step it will perform the adaptation based on static rules.
For this the adaptation engine fetches properties from the devicestatus
API, selects the appropriate rules and injects them in the WRT. The WRT
adapts the application based on these rules then.\
It will also register itself for all relevant property changes with the
devicestatus API.

A watched property has changed[¶](#A-watched-property-has-changed)
------------------------------------------------------------------

<div clas="uml">"DeviceStatus API"->"Adaptation Engine": propertyChanged
"Adaptation Engine"->"Adaptation Engine": selectRules
"Adaptation Engine"->"WRT": fireAdaptationRule
"WRT"->"Application": adapt</div>

When a property has changed, the devicestatus API will fire the
registered callback in the adaptation engine. The adaptation engine will
check it's own and the application's rulebase, fetch all the relevant
rules and adapt them to a format the WRT can process.

Background[¶](#Background)
==========================

Adaptation Rules[¶](#Adaptation-Rules)
--------------------------------------

The adaptation rules comply with the Event Condition Action (ECA)
format. Such a rule traditionally consisted of three parts:

-   The event part specifies the signal that triggers the invocation of
    the rule.
-   The condition part is a logical test that, if satisfied or evaluates
    to true, causes the action to be carried out.
-   The action part consists of updates or invocations on the resource
    that needs adaptation.

The Serenoa project defines a ECA meta model for UI adaptation rules.

<div class="uml">ruleModel "1..*" *-- "0..*" ext_model_ref
ruleModel "1*" *-- "1..*" rule
rule "0..*" o- "0..*" rule
rule "0..*" o-- "1" event
rule "0..*" *-- "0..1" condition
rule "0..*" o-- "1..*" action

condition o- condition
condition <|-- expression
condition <|-- entityReference
condition <|-- constant

event <|-- simple_event
event <|-- complex_event
complex_event "2..*" o-- "0..*" event
agent "0..1" --o "0..*" simple_event

action <|-- create
action <|-- read
action <|-- update
action <|-- delete
action <|-- if
action <|-- while
action <|-- foreach
action <|-- for
action <|-- block
action <|--invokeFunction</div>

**TODO** more detailed description of meta model. Check what can be
adopted/what not... (can be a sub-set)

Adaptation Framework[¶](#Adaptation-Framework)
----------------------------------------------

-   The AdaptationManager filters all events (E) from the app's ECA
    rules
-   AdaptationManager registers for each of these events via Event API
-   When an event is intercepted, condition matching (C) is done by the
    RuleEngine (via Context API data)
-   **TODO** Link action results from RuleEngine to the DOM

<div class="uml">package App #DDDDDD
  class "Adaptation Rules"
  class "DOM"
end package

package "Webinos APIs" 
  class "Context API"
  class "Event API"
end package

"Event API" <- AdaptationManager : addListener
"Event API" -> AdaptationManager : notify

AdaptationManager -- RuleEngine

AdaptationManager - QueryEngine

"Adaptation Rules" - QueryEngine
"Context API" - QueryEngine</div>

To check[¶](#To-check)
----------------------

-   Is Event API suited for this ?
-   How can we let the AdaptationManager access the App's DOM

