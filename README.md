# fraud-moving-sellers-op

Official Documentation: [Fury Docs](https://furydocs.io/fraud-moving-sellers-op/)

![technology Java](https://img.shields.io/badge/technology-Java-green.svg)
![melicov](https://img.shields.io/badge/coverage-91.49%25-green.svg)

# Contents
* [Description](#description)
* [Coding Guideline](#coding-guideline)
* [Changelog](#changelog)
* [Dependency Management](#dependency-management)
* [Spring Boot App model for Java 17](#spring-boot-app-model-for-java-17)
  * [Usage](#usage)
    * [Scope](#scope)
    * [Web Server](#web-server)
    * [Main](#main)
    * [Error Handling](#error-handling)
    * [API Documentation](#api-documentation)
  * [Release Process](#release-process)
    * [Usage](#usage)
    * [Questions](#questions)
  * [About this Application](#about-this-application)



# Description

This application deals with the automation of a task that was previously done manually every day, including weekends.

It is a query that is used to update tables of different teams in order to maintain or track sellers in their different industries.

As soon as the application finishes executing the task, an e-mail is sent informing the business team regarding the changes that have occurred, explaining whether it is an automatic or manual process.


# Coding Guideline
For better development, please follow our [Coding Guideline](CODING_GUIDELINES.md).


# Changelog
To known the documented record of all the changes that this application undergoes, access the [Changelog](docs/CHANGELOG.md).

# Dependency Management

The proposed method for managing dependencies is `maven` and its configuration file is `pom.xml`. 


# Spring Boot App model for Java 17

We provide a basic model for JDK 17 / Spring based web applications.

Please address any questions and comments to [Fury Issue Tracker](https://github.com/mercadolibre/fury/issues).

## Usage

### SCOPE

The suffix of each Fury **SCOPE** is used to know which properties file to use, it is identified from the last '-' of the name of the scope.

If you want to run the application from your development IDE, you need to configure the environment variable **SCOPE=local** in the app luncher.

The properties of **application.yml** are always loaded and at the same time they are complemented with **application-<SCOPE_SUFFIX>.yml** properties. If a property is in both files, the one that is configured in **application-<SCOPE_SUFFIX>.yml** has preference over the property of **application.yml**.

For example, for the **SCOPE** 'items-loader-test' the **SCOPE_SUFFIX** would be 'test' and the loaded property files will be **application.yml** and **application-test.yml**

### Web Server

Each Spring Boot web application includes an embedded web server. For servlet stack applications, Its supports three web Servers:
* Tomcat (maven dependency: `spring-boot-starter-tomcat`)
* Jetty (maven dependency: `spring-boot-starter-jetty`)
* Undertow (maven dependency: `spring-boot-starter-undertow`)

This project is configured with Jetty, but to exchange WebServer, it is enough to configure the dependencies mentioned above in the pom.xml file.

### Main

The main class for this app is Application, where Spring context is initialized and SCOPE_SUFFIX is generated.

### Error Handling

We also provide basic handling for exceptions in ControllerExceptionHandler class.

## Api Documentation

This project uses Springfox to automate the generation of machine and human readable specifications for JSON APIs written using Spring. Springfox works by examining an application, once, at runtime to infer API semantics based on spring configurations, class structure and various compile time java Annotations.

You can change this configuration in SpringfoxConfig class.

## [Release Process](https://release-process.furycloud.io/#/)

### Usage

1. Specify the correct tag for your app in your `Dockerfile` and `Dockerfile.runtime`, according to the desired Java runtime version.

```
# Dockerfile
FROM hub.furycloud.io/mercadolibre/java:17-mini
```

You can find all available tags for your `Dockerfile` [here](https://github.com/mercadolibre/fury_java-mini#supported-tags)

```
# Dockerfile.runtime
FROM hub.furycloud.io/mercadolibre/java:17-runtime-mini
```

You can find all available tags for your `Dockerfile.runtime` [here](https://github.com/mercadolibre/fury_java-mini-runtime#supported-tags)

2. Start coding!

### Questions

[Release Process Issue Tracker](https://github.com/mercadolibre/fury_release-process/issues)

## About this Application

### Important: Environment Variables!

When running the application locally or during integration tests, it is necessary to define an environment variable:

```
APPLICATION=fraud-moving-sellers-op
```

This is because of the [Configuration Service SDK](https://github.com/mercadolibre/fury_configuration-service-sdk/blob/master/README.md#atention).
