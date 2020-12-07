---
layout: page
title: "Home"
---



### My Idea

I like the idea of programming the frontend in java, like you can do with [vaadin flow](https://vaadin.com). Unfortunaly vaadin apps are not stateless. So they did not scale very well. Deep inside there is gwt also in flow. 

How would look like a portal if it was invented nowadays? 

This is a first POC of my ideas: 

Build a cloud native ui framework for [quarkus](https://quarkus.io) but not limited to. Influenced by web components and the idea of ui mircoservices.
It should be stateless, light weight and easy to integrate with quarkus, also build on vanilla browser technologies without GWT or Javascript frameworks. 

### Get Started

This is work in progress. See example.

#### Setup your project

1. checkout the core projects and build them with mvn clean install
1. start a new quarkus project on [code.quarkus.io](https://code.quarkus.io) 
1. Add the cloud-ui-extension to your project 

~~~
      <dependency>
         <groupId>net.moewes</groupId>
         <artifactId>cloud-ui-quarkus-extension</artifactId>
         <version>0.1.0-SNAPSHOT</version>
      </dependency>
~~~

#### Create your first view:

~~~
@CloudUiView("/myview")
public class MyView extends Div {

  public MyView() {

    H1 title = new H1("MyView");
    add(title);
    
  }
}
~~~~

Start server with
~~~
 ``mvn compile quarkus:dev``
~~~

Open Browser [http://localhost:8080/myview](http://localhost:8080/myview)


## Documentation

Work in progress. See Example App so far.






