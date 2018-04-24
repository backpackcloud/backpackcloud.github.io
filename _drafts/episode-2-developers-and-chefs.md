---
layout: post
title:  "Episode 2 - Developers and Chefs"
tags:
  - development
  - automation
  - cooking
---

There is something wrong here. This is not the same plate I ordered last week. The food is not bad, but it doesn't taste like the fantastic meal I had the other day. The sauce was made with different ingredients and the potato lacks the crispy bacon. Consistency is one of the most important things in the kitchen and the need of a manual process doubles the challenge.

Manual processes can blow things on IT. While chefs needs to follow a recipe to assure consistency on every meal, developers don't. Developers need to create the recipe. Following the recipe is for computers. In the IT world, the less we touch something on the pipeline, the more consistent will be the outcome. Not automating the pipeline means taking a great risk.

The use of a voting software for the elections in Brazil is controversial. The Superior Electoral Court organizes a hacking challenge in a heavily controlled environment. In the paper ["The Return of Software Vulnerabilities in the Brazilian Voting Machine"](https://www.researchgate.net/publication/323470546_The_Return_of_Software_Vulnerabilities_in_the_Brazilian_Voting_Machine), the authors blew the voting machine and one of the reason caught my attention: a failure on the manual process of signing two libraries.

Signing a library is a tedious task, prone to errors, great candidate for an automation. The devil is in the detail. We need to make sure all the details are covered.

There was a time I was fighting my command line to sign some artifacts in order to publish them. Good thing the repository rejects any upload without proper signature.

I'm not a fan of doing something twice. I usually spend more time to do something again because I'll try to automate it. It's my nature as a lazy creative developer. I'm always concerned about being consistent... and have more time to do things that matter. That's why I started to write build images.

How can we assure consistency if we're building software using unpredictable environments? A container is something consistent by definition. Why don't use them to consistently build software? That's the idea behind the [Source-to-Image](https://github.com/openshift/source-to-image) (S2I) project.