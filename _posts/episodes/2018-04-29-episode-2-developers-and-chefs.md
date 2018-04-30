---
layout: post
title:  "Episode 2 - Developers and Chefs"
tags:
  - development
  - automation
  - consistency
excerpt: >
  Releasing software is like serving food: you need to have consistency. In this episode, I had a moment to think about it while having dinner at the hotel.
image: devchef.jpg
---

Something is wrong here. This is not the same plate I ordered last week. The food is not bad, but it doesn't taste like the fantastic meal I had the other day. The sauce was made with different ingredients and the potato lacks the crispy bacon. Consistency is one of the most important things in the kitchen and since cooking is a manual process, the challenge is even harder.

Manual processes can blow things on IT. While chefs needs to follow a recipe to assure consistency on every meal, developers don't. Developers need to create the recipe. Following the recipe is for computers. In the IT world, the less we touch something on the pipeline, the more consistent will be the outcome. Not automating the pipeline means taking a great risk.

The use of a voting software for the elections in Brazil is controversial. The Superior Electoral Court organizes a hacking challenge in a heavily controlled environment. In the paper ["The Return of Software Vulnerabilities in the Brazilian Voting Machine"](https://www.researchgate.net/publication/323470546_The_Return_of_Software_Vulnerabilities_in_the_Brazilian_Voting_Machine), the authors blew the voting machine and one of the reason caught my attention: a failure on the manual process of signing two libraries.

Signing a library is a tedious task, prone to errors; a great candidate for an automation. The devil is in the detail. We need to make sure all the details are covered.

There was a time I was fighting my command line to sign some artifacts in order to publish them. Fortunately I was backed by the repository, which rejects any upload without proper signature. The second time I tried an upload, I stopped to write an automation to sign the artifacts.

I'm not a fan of doing something twice. If I need to do it one more time, I'll try to automate it. It's my nature as a lazy creative developer. I'm always concerned about being consistent... and have more time to do things that matter. That's why I started to write build images.

How can we assure consistency if we're building software using unpredictable environments? A container is something consistent by definition. So why don't use them to consistently build software? That's the idea behind the [Source-to-Image](https://github.com/openshift/source-to-image) (S2I) project.

S2I injects the source code into a build container, then it builds the source and produces a container image ready to run. The idea is powerful and simple, but it's focused on images as the result. Since I make tools, S2I can be helpful, but it's not the abstraction I was seeking for this endeavour.

Solving problems is tricky. Use the wrong abstraction and you'd end up hammering a screw. To use pipelines in OpenShift, for example, you have to use [Jenkins](https://jenkins.io). I really don't like Jenkins, it's not the best abstraction. You need 3rd party plugins to make it worth. It's like turning a hammer into a screwdriver.

Then my friend Daniel told me about [GitLab CI/CD](https://about.gitlab.com/features/gitlab-ci-cd/). It has the same idea of S2I and has its own Domain Specific Language (DSL) for defining pipelines. After a few moments of playing with GitLab CI/CD, I found a nice place for it inside my Backpack Cloud.

My first defined pipeline was for a Java project. The classic build/test/release pipeline. GitLab supports variables on projects, which removes some configurations from the DSL file. The pipeline was really interesting... until the second Java project arrived.

I didn't want to repeat myself defining the same boring command for the pipeline steps, so I changed the build image to be my own custom image with some helpers. That allowed me to define steps as a simple `build` command, or even `release`. Everything I needed was already inside the image or defined as a variable inside the organization's settings in GitLab. Beautiful!

When a Golang project arrived at my GitLab, I did the same approach and created another build image. The same thing for my Ruby projects and so on. Now I have a lot of recipes to bake my gourmet tools.

I'm really wondering if the chef followed the recipe. I'd better eat this before it gets cold.