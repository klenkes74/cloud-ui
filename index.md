# Welcome to CloudUi

## Idea

I like the idea of programming the frontend in java, like you can do with [vaadin flow](https://vaadin.com). Unfortunaly vaadin apps are not stateless. So they did not scale very well. Deep inside there is gwt also in flow. 

How would look like a portal if it was invented nowadays? 

This is a first POC of my Ideas: 

Build a cloud native ui framework for [quarkus](https://quarkus.io) but not limited to. Influenced by web components and the idea of ui mircoservices.
It should be stateless, light weight and easy to integrate with quarkus, also build on vanilla browser technologies without GWT or Javascript frameworks. 

## Getting Started

1. checkout the core projects and build them with mvn clean install
1. start a new quarkus project on [code.quarkus.io](https://code.quarkus.io) 
1. Add the cloud-ui-extension to your project 

``
      <dependency>
         <groupId>net.moewes</groupId>
         <artifactId>cloud-ui-quarkus-extension</artifactId>
         <version>0.1.0-SNAPSHOT</version>
      </dependency>
``
    

## Documentation

## Projects

### Core Projects

* [CloudUi Quarkus Extension](https://github.com/moewes/cloud-ui-quarkus)
* [CloudUi Core](https://github.com/moewes/cloud-ui-core)
* [CloudUi Client](https://github.com/moewes/cloud-ui-client)

### Examples
* [CloudUi Example App](https://github.com/moewes/cloud-ui-example)

### Component Libraries
* [CloudUi Ui5 Webjar](https://github.com/moewes/ui5-webjar)


