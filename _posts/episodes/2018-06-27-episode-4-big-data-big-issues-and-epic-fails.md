---
layout: post
title:  "Episode 4 - Big Data, Big Issues and Epic Fails"
tags:
  - big data
  - complex event processing
  - real-time
categories: episodes
intro: >
  Big Data is changing the world, no one can deny that. Smartphone sensors came to add even more data to process. This episode shows a great Big Data application, some issues caused by trusting user input data and an epic fail that allowed me to cause some trouble.
image: waze.jpg
---

"Look! I'm almost a king!" Anderson told me. I didn't understand why and asked him to explain his madness. He then told me about Waze, a collaborative GPS application for smartphones. The idea is awesome: using the GPS sensors for getting an overview about the traffic so drivers could be warned about possible traffic jams and other issues on the road. I made fun of him, telling I could be a king before he does.

Waze is one of the best examples of how Big Data can change the world. You have tons of data to process and need to translate that into meaningful information so users can make better decisions. A lot of people explain Big Data using the classic 3 V's: Volume, Velocity and Variety. Volume is about the amount of data, Velocity is about how fast the data is processed and Variety is about the types of the data. It's a good start, but there is also a big V that sometimes is not considered: the Value. It doesn't matter if there's 50 yottabytes processed in 12 yoctoseconds from 42 different sources; if that doesn't add value to the business, it shouldn't being done. Waze has a great value because it provides, quoting its own website, "real–time help from other drivers". But there's one thing that keeps bothering me: the real-time term.

There's a lot of """""""""""real-time""""""""""" applications out there (feel free to add more quotes) but, as Big Data only makes sense if there's **value** on the outcome, **real** real-time applications need a time constraint as a deadline. This deadline has a strong relation to the value of the application: how the value is impacted by missing or not the deadline is what classifies the application. The deadline can be missed by a lot of factors, so it's important to use real-time operating systems at least. I have my doubts if Waze is really a real-time system because it depends on smartphones and there is no evidence of a time constraint. Maybe it's just an online system, but that's not a good definition for marketing purposes. Regardless, Waze adds value because the tons of data processed from the drivers helps them to complete their journeys.

Now another problem raises: how to be sure the incoming data is real? The Complex Event Processing aims to solve that by analyzing data from multiple sources to deliver a conclusion about the event. This can prevent frauds in online transactions, for example, and could be used to determine if the information coming from a driver is real. Sometimes it's simple to detect, like a driver rushing at 500 km/h or the same driver reporting a location 2000 km far from the last one reported 5 min ago. The funny thing is: I did those inputs and Waze processed them without checking.

First, I loaded a GPS mock app for rooted devices on my Android phone. Then I started to "travel" the world sitting on my (un)comfortable chair at work. I did a lot of international travels, changing the country one after the other. Then I had a better idea: travel at blazing fast speeds on jammed roads. It was awesome! Waze grabbed my 2500 km/h speed and used it to compute the average speed and then removed the red lines over the roads. Then it routed more drivers to those roads because it thought they weren't jammed anymore. Yes, I caused the chaos!

After one week messing up with Waze, I scored 5th on the weekly scoreboard and became a King! Anderson cried aloud for a moment while I laughed at his face. Months later, I published on my blog the step-by-step to do the trick. Few days after the post, Google sent me an email banning me from the platform because I was "reporting too much".

Turns out the Complex Event Processing used by Waze was different from what I thought.