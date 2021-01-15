---
layout: page
title: Use Web Components
---

#### Overview

This guide will explain how web components are integrated in your project. 

* How the Javascript files are loaded.
* How you can connect your java code with web components
* How you can write wrapper class for better abstraction

#### How To Load The Javascript Files

Javascript file ar integrated via webjar. All *.js files of all dependencies that are webjars are included in the the view pages. For an example of how to build a webjar of your web components see the ui5-webjar or the vaadin-webjar project.

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

A better and more comfortable and clean way for using web components in your java code is to write wrapper classes for each component. 

~~~~

/**
 * Java wrapper for UI5 web component ui5-carousel
 */
public class Ui5Carousel extends UiComponent {

    private boolean cyclic;

    /**
     * default constructor
     */
    public Ui5Carousel() {
        super("ui5-carousel");
    }

    /**
     * sets arrows-placement attribute of ui5-carousel
     *
     * @param placement va
     */
    public void setArrowsPlacement(ArrowsPlacement placement) {
        getElement().setAttribute("arrows-placement", placement.getAttributeText());
    }

    ...
~~~~

This is an example of the wrapper fpr ui5-carousel web component. The user of that component don't need to know the tag name and you can e.g. put list of possible values in enum.

Because of the stateless behavior of CloudUi you control the your web component only over static attributes and event handler. You cannot call any methods of the underlying javascript classes. So sometimes it might be necessary to wrap the original web component in a wrapper. An Example for that is the Vaadin notification component.


#### Limitations

So far you can't load Javascript from project local files. They have to be embedded via webjars. 