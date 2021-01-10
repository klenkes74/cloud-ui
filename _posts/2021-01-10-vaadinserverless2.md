---
layout: page
title: "Vaadin, Java and Serverless - Part 2"
description: "Does it work? With CloudUi it does!"
---

#### Vaadin, Java and Serverless - Part 2

##### How it is done

I started a new project with the quarkus-azure-functions-http extension as it is described in [this guide](https://quarkus.io/guides/azure-functions-http) on quarkus.io.

The next step was to add CloudUi and the CloudUi Vaadin component library to the pom.xml.

~~~~

...
<dependency>
      <groupId>net.moewes</groupId>
      <artifactId>cloud-ui-quarkus-extension</artifactId>
      <version>0.1.0</version>
    </dependency>
    <dependency>
      <groupId>net.moewes</groupId>
      <artifactId>cloud-ui-vaadin</artifactId>
      <version>0.1.0-SNAPSHOT</version>
</dependency>
...
~~~~

After that I was able to add my view (inspired from the simple getting started example).

~~~~~

@CloudUiView("/vaadinserverless")
public class MyVaadinView extends VerticalLayout {

  public MyVaadinView() {

    TextField nameField = new TextField();
    nameField.setLabel("Your Name:");
    nameField.setRequired(true);

    add(nameField);

    Button button = new Button("Say Hello");
    add(button);

    button.addEventListener("click", event -> {
      String name = nameField.getValue() == null ? "unknown" : nameField.getValue();
      Notification notification = new Notification("Hello " + name, 2000);
      add(notification);
      notification.open();
    });
  }
}

~~~~

##### Test it local

mvn compile quarkus:dev

open localhost:8080/api/vaadinserverless in your browser

##### Deploy it to azure

You need to have azure acount to do so.
As described in the quarkus guide deploy it with the following command in your terminal:

~~~~

mvn clean install 

az login 

mvn azure-functions:deploy
~~~~

Due a bug in the quarkus-azure-functions-http I had to add some tweaks:

* Change the entrypoint in function.json to a modified method
* Implement a Function class to work around that bug

[See it in action](http://cloudui.azurewebsites.net/api/vaadinserverless)

The working code is in [GitHub](https://github.com/moewes/cloudui-vaadin-serverless)

Of course you need to change some parameters in pom.xml to make it work:

~~~~
    <!-- Replace the following paramters with your own valid values -->
    <functionAppName>cloudui</functionAppName>
    <functionAppRegion>germanywestcentral</functionAppRegion>
    <functionResourceGroup>net.moewes.azure-test</functionResourceGroup>
    <function>quarkus</function>
~~~~





