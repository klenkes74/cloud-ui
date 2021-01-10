---
layout: page
title: "Vaadin, Java and Serverless"
description: "Does it work? With CloudUi it does!"
---

#### Vaadin, Java and  Serverless

##### Does it work? With CloudUi it does!

Modern web uis are nowadays state of the art. A lot of people develop them with several popular javascript libraries, i.e. angular, react or vue just to name a few.

On the other hand many backends are written in java. So some people wish to UI and business logic in one language. There are many advantages and disadvantages of the different approaches that I don't want to discuss in this post.

Vaadin flow is an interesting approach for those who like to develop UIs in Java and also what to get a modern HTML 5 UI.

I've brought successfully some projects to life with vaadin flow. The Vaadin flow frameworks works quite well. But for me there some buts:

* vaadin flow isn't stateless - so you can't scale your ui servers in a cloud native environment like kubernetes.
* the build process has become really slow, especially since they don't use the bower webjars any more
* it has limitations when you try to realize ui-microservices
* it is not easy to integrate with quarkus, here is also the new build process a big problem

So I started the project CloudUi as a proof of concept. It should be stateless, integrate well with quarkus, with the same ease of java ui development as flow.

So let’s the flow samples and check if it works serverless:

[Try the first simple example](http://cloudui.azurewebsites.net/api/vaadinserverless)

In my next post I will show it is done!



