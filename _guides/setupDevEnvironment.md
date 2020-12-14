---
layout: page
title: Setup Development Environment
description: How to resolve dependencies
---

### Setup Development Environment (How to resolve dependencies?)

CloudUi libraries ar currently not published to maven central. They use GitHub packages instead. To use CloudUi in your own project or to compile the examples you need a way to resolve the dependencies. There are two ways to approach that.

1. check out the dependend projects an build them with maven
1. Use GitHub packages

#### Use GitHub packages

##### Add the repository for every used library to your global setting.xml (USER_HOME\.m2\settings.xml):

~~~~

<repositories>
    <repository>
        <id>github</id>
        <name>GitHub CloudUi Quarkus Extension</name>
        <url>https://maven.pkg.github.com/moewes/cloud-ui-quarkus</url>
        <releases><enabled>true</enabled></releases>
        <snapshots><enabled>true</enabled></snapshots>
    </repository>
</repositories>

~~~~

##### Add the authentication to the Package Registry to your global settings.xml (USER_HOME\.m2\settings.xml):

~~~~

<servers>
    <server>
        <id>github</id>
        <username>YOUR_GITHUB_USERNAME</username>
        <password>YOUR_AUTH_TOKEN</password>
    </server>
</servers>
~~~~


Replace the YOUR_AUTH_TOKEN with a generated GitHub personal access token:
GitHub > Settings > Developer Settings > Personal access tokens > Generate new token:
The token needs at least the read:packages scope.

#### Build dependencies with maven

##### create new directory e.g. cloud-ui (optional)

~~~~

mkdir cloud-ui-repos
cd cloud-ui-repos
~~~~

##### checkout and build project cloud-ui-client

~~~~

git clone https://github.com/moewes/cloud-ui-client.git
cd cloud-ui-client
mvn install
cd ..
~~~~

##### checkout and build project cloud-ui-core

~~~~

git clone https://github.com/moewes/cloud-ui-core.git
cd cloud-ui-core
mvn install
cd ..
~~~~

##### checkout and build project cloud-ui-quarkus-extension

~~~~

git clone https://github.com/moewes/cloud-ui-quarkus.git
cd cloud-ui-quarkus
mvn install
cd ..
~~~~

##### optional checkout and build ui5 components

Web components webjar:
~~~~

git clone https://github.com/moewes/ui5-webjar.git
cd ui5-webjar
mvn install
cd ..
~~~~

Java Library:
~~~~

git clone https://github.com/moewes/cloud-ui-ui5.git
cd cloud-ui-ui5
mvn install
cd ..
~~~~

