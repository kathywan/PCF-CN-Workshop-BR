# Building a Spring Boot Application

In this lab we'll build and deploy a simple [Spring Boot](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle) application to Cloud Foundry whose sole purpose is to reply with
a standard greeting.

## Getting started

Let's go to https://start.spring.io to create a new Spring Boot project with the following details:

Group: io.pivotal

Artifact: cloud-native-spring

Dependencies:

- Spring Web Starter
- Spring Data JPA
- Rest Repositories
- Spring Boot Actuator
- Spring Boot DevTools
- Lombok
- H2

Open this project in your editor/IDE of choice.

## Add an Endpoint
Within your editor/IDE complete the following steps:

* Create
a new class named `GreetingController` in the same package.
* Add an `@RestController` annotation to the class
`io.pivotal.cloudnativespring.GreetingController` (i.e.,
**/cloud-native-spring/src/main/java/io/pivotal/cloudnativespring/GreetingController.java**).

Completed:

```java
package io.pivotal.controller;

import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.bind.annotation.GetMapping;

@RestController
public class GreetingController {
  @GetMapping("/hello")
  public String hello() {
    return "Hello World!";
  }
}
```

## Build the _cloud-native-spring_ application

Return to the Terminal session you opened previously and make sure your working directory is
set to be `cloud-native-spring/labs/my_work/cloud-native-spring`

First
we'll run tests
```bash
mvn test
```
Next we'll package the application as an
executable jar
```bash
mvn package
```

## Run the _cloud-native-spring_ application

Now we're ready to run the application . Run the application
with:
```bash
mvn spring-boot:run
```
You should see the application start up an
embedded Apache Tomcat server on port 8080 (review terminal output):

```bash
2018-08-22 17:40:18.193 INFO 92704 --- \[ main\]
o.s.b.w.embedded.tomcat.TomcatWebServer : Tomcat started on port(s):
8080 (http) with context path '' 2018-08-22 17:40:18.199 INFO 92704 ---
\[ main\] i.p.CloudNativeSpringUiApplication : Started
CloudNativeSpringUiApplication in 7.014 seconds (JVM running for 7.814)
```
Browse to http://localhost:8080/hello

Stop the _cloud-native-spring_
application. In the terminal window type **Ctrl + C**

## Deploy _cloud-native-spring_ to Pivotal Cloud Foundry

We've built and run the
application locally. Now we'll deploy it to Cloud Foundry.

Create an
application manifest in the root folder
*cloudnative-spring-workshop/labs/my_work/cloud-native-spring*

```bash
touch manifest.yml
```
Add application metadata, using a text editor (of choice)
```yaml
--- 
applications:
- name: cloud-native-spring
  random-route: true
  instances: 1
  path: ./target/cloud-native-spring-0.0.1-SNAPSHOT.jar
```

Push application into Cloud Foundry
```bash
cf push
```

Find the URL created for your app in the
health status report or issue the following command to see your running apps.

```bash
cf apps
```

Browse to your app's **/hello** endpoint

Check the
log output:

```bash
cf logs cloud-native-spring --recent
```
<b>Congratulations!</b>
You’ve just completed your first Spring Boot application.
