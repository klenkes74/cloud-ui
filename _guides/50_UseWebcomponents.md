---
layout: page
title: Use Web Components
---

#### Overview

tbd

#### How To Load The Javascript Files

tbd

#### Use UiComponent 

Create an instance of the web component with the UiComponent Class.

~~~~

UiComponent myComponent = new UiComponent("my-component");
~~~~

You can user the setAttribute-Method to set attributes of the HTMLElement and the setInnerHtml method or the add method to set the content of your web component.

For compoment wich have a value you need to set the hasInput attribute to true. Othervise the value is not transferd back to the Server.

~~~~


component.getElement().setHasInput(true).
~~~~


#### Make a Java Wrapper Class

tbd

#### Limitations

So far you can't load Javascript from project local files. They have to be embedded via webjars. 