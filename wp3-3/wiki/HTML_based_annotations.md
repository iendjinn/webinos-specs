HTML based annotations[¶](#HTML-based-annotations)
==================================================

The adaptation to the user interface for an application is done
client-side within the widget runtime in webinos. Webinos provides a set
of adaption rules to allow the automatic adaption to the user interface
for smartphones, tablets, PCs, in-car headunits and TVs.

In order to allow the automatic adaption the developer has to annotate
the relevant DOM elements in the HTML page with data-\* attributes. The
widget runtime injects the adpation engine and the predefined rules into
the application at runtime.

Besides the predefined rules, the developer can write custom rules for
the adaption. As context provider for the adaption, the developer can
draw upon on the available webinos services. The predefined adaptation
rules are making use of the Webinos Core Management API and are based on
jQuery mobile.

Shall we include a flag in the application manifest to allow content
adaptation? If the flag is set to true, the code for the adaption engine
and the predefined rules is injected into the application.

Components[¶](#Components)
--------------------------

<div class="uml">package "Widget Runtime" #DDDDDD

	package "ContentAdapation"
		class AdaptationEngine
		class Rule
	end package


	class RenderingEngine{
		void injectAdaptionEngine()
		void executeApp()
	}
  class Application

end package

package "PersonalZoneProxy" #DDDDDD
	class API

end package

AdaptationEngine "1" *-- "many" Rule
RenderingEngine -- Application : "excute App"
Rule "1"-->"*" API:  queries
AdaptationEngine -->  Application </div>

General Approach[¶](#General-Approach)
--------------------------------------

For packaged apps (link to Widget spece) the adaptation engine
(javascript and css files) is injected by widget runtime. For hosted
applications the adapatation engine needs to be embedded into Web
application by the developer. There a three diffrent rule types

-   Application based rules: The rules are defined by the developers.
    The developer can use as a context provider all the APIs provided by
    webinos and the rendering engine.
-   Widget-based adaption rules: The widget-based adoption rules

### Application specific rules[¶](#Application-specific-rules)

Application/developer specific adaptation rules need to be registered at
the adaptation engine at rendr

How to register rules to adaptation engine?

### UI-Element adaption: data-\* attributes[¶](#UI-Element-adaption-data--attributes)

When the DOM tree has been loaded into the rendering engine, the
adaptation engine parses the DOM tree for objectes containing data-\*
attributes and matching a specific rule. The adpatation engine applies
the rule to the object.

    //example rule

[Predefined Rules for UI-widgets](.html)[¶](#Predefined-Rules-for-UI-widgets)
-----------------------------------------------------------------------------
