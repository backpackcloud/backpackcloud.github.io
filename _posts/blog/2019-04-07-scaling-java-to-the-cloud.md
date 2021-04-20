---
layout: post
title:  "Scaling Java to the Cloud"
tags:
  - java
  - cloud
  - scalability
  - quarkus
  - graalvm
categories: blog
intro: >
  Java is still widely used for classic workloads, but not that much for cloud workloads. On this episode, I had a moment to think about that when things got bad with the public transportation.
---

A couple of days ago I was planning to go out with my family by public transportation since we don't have a car. Just before we leave, my wife got a message from a friend warning us about a standstill that affected all the trains in our region. The busses were full of people trying to commute so we decided to do the errand on the next day. It's hard to scale a bus fleet. Like some web applications I've been seeing around.

Back in the days of classic workload, applications were mainly built to serve internal users and the number of devices connected to the Internet wasn't that expressive. I remember people being surprised because I was online almost every time after I bought my first Android device in 2010.

At that time, mobile Internet was responsible for only 3.81% of the total web traffic, according to StatCounter. In 2014, that number raised to about 25%. In 2015, Google announced a change on its page rank algorithm to promote responsive web pages. The online world was changing.

When the market perceived the massive adoption of smartphones, the need to support mobile devices became a must-have. APIs started to gain visibility as the perfect backend for the new workload, culminating in a new approach called API-first. With APIs, both web apps and mobile apps could use the same backend while changing only the UI.

However, exposing a resilient API is not an easy task since the load might be hard to predict. To balance resource usage and still be prepared for massive load periods, scaling fast is mandatory. On the other side, bootstrap and footprint are number one enemies of scalability. Being careless about them is like going number two.

The Java Virtual Machine – JVM – was introduced in 1994, the computer's mesozoic era, when a cloud was something you saw up in the sky, containers were handled by cargo ships and Javascript wasn't born yet, (but still had 42000 frameworks). Over the years, the Java ecosystem got some shinny improvements, nice frameworks, competitive vendors, but ended up being too resource hungry for a healthy container diet.

So how can we beat the villains and make Java a feasible choice for container native applications?

Java was designed to be multiplatform and dynamic, the opposite of what is need for running in the cloud. Containers are Linux, so being multiplatform doesn't matter. Containers should be immutable, so being dynamic also doesn't matter. The things that made Java a top platform for classic workloads are now preventing it to be a top one for cloud workloads. It's time to do some refactoring.

The ability of loading classes dynamically doesn't seems to be a great deal since containers should be immutable. The same happens with newer versions. If you need to deploy a new version of your web app just build another image and deploy a new container. The scenario now is more static, a great opportunity for introducing ahead-of-time – AOT – compilation.

AOT compilation analyses the code in order to do optimisations at compile time. Since the behaviour will be the same (remember, no dynamic stuff happening now) there's no need for just-in-time compilations happening at runtime, reducing both bootstrap time and memory usage. Of course that requires more resources to compile the code.

And what about the target platform? Basically, every container will be deployed on a Linux host so a native executable seems to be the best choice. Having a compiler to generate native binaries instead of a jar file to run on a JVM is a huge improvement, at the cost of even more resources.

Ok, it seems we just moved the workload to another phase. But how many times the application will be built on the pipeline? And how many application containers will be deployed after each build? It's easy to see the advantages of having a not-so-fast build stage producing a highly scalable container image that can go from a few to thousands of instances in a couple of seconds.

[GraalVM][graalvm] was designed to address those needs. It creates a native executable of a Java program to run on a VM that's also compiled to a native executable, the SubstrateVM. The result is a native binary that performs orders of magnitude higher than a traditional Java program... at a cost.

Some tricks like Reflection and static initialisers have [little to no support][graalvm_limitations], which requires new implementations for common frameworks or even new alternatives to solve old problems. Developers should learn not only how to deal with those problems but also how to rewrite implementations in order to use GraalVM at its maximum. New strategies for development are now possible like almost instant reload and tests that runs so fast that mocks are no longer needed. With new implementations targeting GraalVM and a new development toolset that does the heavy lifting of dealing with GraalVM it's possible to create a productive stack for cloud native applications.

That's what the project [Quarkus][quarkus] aims for! A Kubernetes Native Java stack that makes Java worth to be used in the cloud.

Quarkus supports hot reload and provides support for widely used [frameworks][quarkus_extensions] such as Hibernate, Vert.x, Kafka, Camel and also supports the awesome [Kotlin] language. It deals with GraalVM to make sure the application binary is created smoothly. It can also generate jar files so developers don't need to wait for a native compilation in order to test locally. And it's [Open Source][quarkus_code], of course!

There was a time when I had to choose between creating applications fast or creating fast applications. Now I want to create fast applications fast. That's why now I'm riding with Quarkus... heading to the cloud... fearless about standstills.

[graalvm]: <https://www.graalvm.org/>
[graalvm_limitations]: <https://github.com/oracle/graal/blob/master/substratevm/LIMITATIONS.md>
[quarkus]: <https://quarkus.io/>
[quarkus_extensions]: <https://quarkus.io/extensions/>
[quarkus_code]: <https://github.com/quarkusio/quarkus>
[kotlin]: <https://kotlinlang.org/>
