---
layout: page
title: "New Example App: Number guessing Game"
description: "Not finished yet! This is work in progress"
---

### What it schould do

User can start a game at localhost:8080/start. First the user can input her or his name, the number range and how many guesses are allowed in maximum.

On a second view the user can input her or his guess until the maximum number of guesses is reached or she or he guess the right number. In case of a wrong guess a hint is schown whether the number is higher or lower the last guess.

When the game is over (right guess or maximum number of guesses reached) a result view is shown with the possibility to start again.

support for multiuser environment is out of the scope. To make things simple we assume there ist only one person who use the game in a local environment.

### Setup project on code.quarkus.io

### Add CloudUi Extension

Add the following dependency to your pom.xml file:

~~~
  <dependency>
      <groupId>net.moewes</groupId>
      <artifactId>cloud-ui-quarkus-extension</artifactId>
      <version>0.1.0-SNAPSHOT</version>
    </dependency>
~~~

[Setup Development Environment](../../../guides/setupDevEnvironment.html)

### First View

~~~


~~~

### Our Game Bean


~~~~
~~~~

### Our Guessing View

~~~~
~~~~

### 